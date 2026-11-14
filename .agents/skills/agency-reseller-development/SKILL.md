---
name: agency-reseller-development
description: >-
  Use this skill when working on the reseller/agency module (agency.go, agency_http.go,
  web/agency.js), wallet ledger, cascade pricing, reseller RBAC, or reseller API keys.
---

# Reseller / Agency Module Development

Reference specification: `AGENCY-SPEC.md` (and implementation in `agency.go`, `agency_http.go`, `web/agency.js`).

## Key Invariants
1. **Lock Order**: Always take `Store.mu` before `Ag.mu` when both are needed. Never acquire `Store.mu` inside `Ag.mu`.
2. **Append-Only Financial Ledger**:
   - All balance changes append a `LedgerEntry` to `agency/ledger.jsonl` and `fsync`.
   - Balances (`ag.bal[agentID]`) are always reconstructed by replaying `ledger.jsonl` on startup (torn final lines from crashes are ignored).
   - Never edit or delete ledger rows; compensate errors with `reversal` or `refund`.
3. **Cascade Charging ("Waterfall")**:
   - When an agent sells or renews, charge the agent **and** every ancestor at their own configured/inherited price from their respective wallets before touching `Store`.
   - Parents cannot set a child's price lower than their own purchase price.
   - If the core `Store` operation fails after charging, immediately reverse all entries in that `Sale` group.
4. **Reseller Isolation & RBAC**:
   - Resellers authenticating via cookie (`A.<id>.<tokenVer>.<exp>.<sig>`) or API key (`vl_` + 48 hex chars via `X-API-Key` / `Authorization: Bearer`) may only see and act on their own accounts (or their subtree for management roles).
   - Never leak inbound private keys/certs (`caKey`, `serverKey`, `key`, `tlsCrypt`) in reseller inbound views.
   - On bot API identity lookups, resolve accounts within the caller's owned scope so shared passwords cannot cross into another reseller's account.
5. **Freeze Propagation**:
   - Freezing an agent (`Frozen = true`) rebuilds the `frozenOwners` atomic snapshot (`refreshFrozenLocked`), immediately blocking new logins and disconnecting live sessions in `EnforceLoop` without mutating individual account flags.

## Required Verification
Run `go vet ./... && go test -race ./...`, paying special attention to `agency_test.go` (`TestAgencyBotFlow`, `TestAgencyCascadeAndRefund`, `TestAgencyConcurrentSalesNeverOverspend`, `TestAgencyFreezeStopsAccounts`, `TestAgencyBackupRoundTrip`).
