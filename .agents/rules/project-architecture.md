---
trigger: always_on
description: Core architectural rules, lock ordering, compatibility guarantees, and Go 1.22 standard-library constraints for LitePanel (vpn-lite).
---

# LitePanel (vpn-lite) Architecture & Invariants

LitePanel (`module vpnlite`, Go 1.22, standard library only — zero external Go dependencies) is a single static binary VPN account panel for OpenVPN, L2TP (IPsec + plain), and Cisco/OpenConnect, with an embedded single-page admin/reseller UI (`web/index.html`, `web/agency.js`) and an embedded reseller/agency module (`agency.go`, `agency_http.go`).

Repository: `PouryaDe/LitePanel` (default branch `main`).

## Hard Constraints

1. **Go 1.22 & Standard Library Only**:
   - `go.mod` targets `go 1.22`. Do not introduce external Go module dependencies or Go >1.22 language/stdlib features (CI runs with `go-version-file: go.mod` and `CGO_ENABLED=0`).
2. **Never Hold Locks Across I/O or Subprocesses**:
   - Never perform network writes, disk writes, or `exec.Command` calls while holding `Store.mu`, `Ag.mu`, or `Sessions.mu`.
   - Copy the required snapshot under `RLock`/`Lock`, release the lock, then serialize JSON, talk to daemons, or write HTTP responses (see `viewInboundLocked` -> `render()` in `model.go` and `KickEmail` in `enforce.go`).
3. **Strict Lock Ordering**:
   - Always acquire `Store.mu` **before** `Ag.mu` (and `Sessions.mu` after `Store.mu`).
   - **NEVER** acquire `Store.mu` while already holding `Ag.mu` — doing so risks deadlocks.
4. **Zero-Downtime Daemon Supervision**:
   - VPN daemons (`openvpn`, `xl2tpd`, `ocserv`) run as independent processes and survive panel restarts.
   - `OvpnManager.Reconcile` (`ovpn.go`) and `daemonSet.apply` (`daemons.go`) gate restarts on config fingerprints (`hash` / `hash2`). Never alter daemon config templates carelessly in ways that change the restart fingerprint unless an actual restart is intended.
   - Prefer reloadable parameters (`ocservReloadable` via `SIGHUP` in `ocserv.go`; ppp `options` / `radius` client config read per new connection in `l2tp.go`; OpenVPN management socket in `ovpn.go`).
5. **Backward-Compatible Bot HTTP API**:
   - Do not change existing `/login` or `/panel/api/inbounds/...` route paths, query/form field names, or the `{success, msg, obj}` JSON envelope (`api.go`, `model.go`) — external Telegram bots depend on this exact contract.
6. **Accurate Accounting & Session Kills**:
   - Never double-count traffic deltas (`SessionTable.Touch` in `enforce.go`, `Store.addInboundBytes` in `store.go`).
   - Always disconnect sessions by exact session identity (`Session.ID`, management CID, `ppp` peer VIP lookup in `killPPP`, or `occtl` session ID in `killOcserv`), never by client IP alone.
7. **Append-Only Reseller Ledger & Default-Deny Routes**:
   - `agency/ledger.jsonl` is strictly append-only; never edit or delete entries (compensate errors with `reversal` or `refund` entries). Balances are always derived by summing ledger entries.
   - In cascade operations, debit the seller and all ancestors **before** mutating `Store`, and reverse immediately if the core operation fails.
   - New API/UI routes default to admin-only (`api(h, nil)` in `api.go`, `ui(h)` in `ui.go`). Reseller access requires an explicit scoped handler (`api(h, agent)` / `uiAgent(h, agent)` / `agencyRoutes` role).
8. **Code Comments & Verification**:
   - Keep code comments short, in English, explaining *why* rather than *what*.
   - Verify every code change with `go vet ./... && go test -race ./...` and add targeted tests for behavioral changes.
   - After modifying code files, run `graphify update .` to keep `graphify-out/` current.
