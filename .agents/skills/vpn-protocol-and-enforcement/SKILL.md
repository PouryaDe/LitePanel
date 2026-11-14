---
name: vpn-protocol-and-enforcement
description: >-
  Use this skill when modifying VPN protocol daemons (OpenVPN, L2TP/IPsec, Cisco/OpenConnect),
  the embedded RADIUS server, session enforcement, traffic shaping (tc), nftables, or IranDirect routing.
---

# VPN Protocols, RADIUS & Enforcement

## Architecture Overview
- **Orchestrator (`engine.go`)**: `Engine.Reconcile()` converges `OvpnManager`, `l2tpDaemons`, `ocservDaemons`, `reconcileIPsec()`, and `applyNft()`. Bursts of `ReloadInbound` collapse via a 400ms debounce in `reconcileLoop`.
- **OpenVPN (`ovpn.go`, `ovpnconf.go`)**: Runs one `openvpn` process per `(inbound, transport)` (`udp` / `tcp`). Authenticates asynchronously via `--management` socket (`management-client-auth`), tracks `bytecount`, and rebuilds sessions on panel restart via `status 3`.
- **L2TP / IPsec (`l2tp.go`)**: Runs one `xl2tpd` + `pppd` per inbound (`force userspace = yes` unless `kernelMode` is enabled; `ppp.options` + RADIUS client config are read per connection without restarting `xl2tpd`). strongSwan (`swanctl`) handles IKEv1 PSK on UDP 500/4500 in transport mode for UDP/1701.
- **Cisco / OpenConnect (`ocserv.go`)**: Runs `ocserv` with `auth = "radius[...,groupconfig=true]"` and `acct = "radius[...]"`. Keys in `ocservReloadable` (`keepalive =`, `dpd =`, `mobile-dpd =`) trigger `SIGHUP` (`reloadHash`) instead of a daemon restart (`hash2`).
- **Embedded RADIUS (`radius.go`, `radiusconf.go`, `mschap.go`)**: Listens on `127.0.0.1` (`1812`/`1813`), supports PAP, CHAP, and MS-CHAPv2, suppresses duplicate packets, and translates Interim/Stop accounting into `Sessions.Touch` + `Store.AddTraffic` + `Store.addInboundBytes`.
- **Enforcement (`enforce.go`)**:
  - `Authorize` / `AuthorizeFn` reserves the new `Session` inside `Sessions.mu` atomically with the device-cap check.
  - `looksDead(now)` treats silent sessions (`>15s` OpenVPN, `>150s` L2TP/Cisco, when `LastActive > 0`) as dead and replaces them on reconnect.
  - Respect `AllowMultiProto` / `SingleProto` (`protoFamily` groups `openvpn-udp` and `openvpn-tcp` into `"openvpn"`), `LimitStrategy` (`reject` vs `evict`), and `EvictGraceSec` (anti-ping-pong).
  - `EnforceLoop` runs every 10s to kick disabled, expired, over-quota, deleted, or `ownerFrozen` accounts.
- **Shaping & Plumbing (`shaper.go`, `nft.go`, `iranroutes.go`)**:
  - `Shaper` executes `tc` asynchronously on a single worker channel (`q`), using TBF/ingress policer on dedicated devices (`pppN`, `vcN`) and HTB classes + `u32` filters on shared `vl*` OpenVPN tun devices.
  - `nftRuleset` manages the isolated `table ip vpnlite` atomically (`masquerade` + TCP MSS clamping to 1240).

## Rules When Editing
1. Never introduce synchronous `exec` hooks into OpenVPN, pppd, or ocserv login paths.
2. When modifying daemon configs, verify whether changes belong in the restart fingerprint or reload-only path (`audit_test.go` explicitly tests `TestPppOptionsDoNotRestartXl2tpd` and `TestOcservTimersReloadNotRestart`).
3. Verify `go vet ./... && go test -race ./...` (especially `engine_test.go`, `audit_test.go`, `mschap_test.go`, `shaper_test.go`).
