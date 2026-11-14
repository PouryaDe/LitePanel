---
name: release-and-verify
description: >-
  Use this skill when validating changes, building the static vpn-lite binary,
  running a local smoke test, or preparing/triggering a GitHub release on PouryaDe/LitePanel.
---

# Build, Verify & Release

## 1. Static Checks & Race Tests
Run the same checks as `.github/workflows/ci.yml`:
```bash
go vet ./...
go test -race ./...
CGO_ENABLED=0 go build -trimpath -o /tmp/vpn-lite .
```

## 2. Local Panel Smoke Test (No VPN Daemons Required)
```bash
D="-data /tmp/vl/d -conf /tmp/vl/c -run /tmp/vl/r -log /tmp/vl/l"
./vpn-lite setup $D -user admin -pass adminpass1 -port 18999 -no-tls
./vpn-lite serve $D -no-daemons
```
This runs the full HTTP panel, embedded UI (`web/index.html`, `web/agency.js`), and agency store locally without needing OpenVPN, xl2tpd, ocserv, or nftables.

## 3. Versioning & GitHub Releases
- Repository: `PouryaDe/LitePanel` (`update.go` `releaseRepo` and `install.sh` `REPO` both target `PouryaDe/LitePanel` by default).
- `.github/workflows/release.yml` runs on tag push `v*` or `workflow_dispatch` with input `version` (e.g. `v0.3.2`).
- It runs `go vet ./... && go test -race ./...`, builds static Linux binaries `vpn-lite-linux-amd64` and `vpn-lite-linux-arm64` with `-ldflags "-s -w -X main.version=${VERSION}"`, generates `SHA256SUMS`, and publishes a GitHub Release.
- Verify that `install.sh` and `update.go` asset naming (`vpn-lite-linux-$ARCH` + `SHA256SUMS`) remains synchronized with `release.yml`.
