# Graph Report - VPN Lite  (2026-11-15)

## Corpus Check
- 52 files · ~69,580 words
- Verdict: corpus is large enough that graph structure adds value.
- Unclassified: 2 file(s) not represented in the graph (top: (none) 1, .db 1)

## Summary
- 823 nodes · 2794 edges · 27 communities (20 shown, 7 thin omitted)
- Extraction: 83% EXTRACTED · 17% INFERRED · 0% AMBIGUOUS · INFERRED: 485 edges (avg confidence: 0.85)
- Token cost: 0 input · 0 output

## Community Hubs (Navigation)
- Agency HTTP & Bot API
- Agency Tests & Helpers
- Agency Store & Ledger
- Daemon Reconcile & Audit Tests
- Config Hashing & TLS Reload
- Session Enforcement & Shaper
- Agency Frontend UI
- Server Installer & Menu
- HTTP Auth & MSCHAP Crypto
- Embedded RADIUS Server
- Core Bot & Panel API
- Specs & Core Modules
- HTTP Gzip & Response Buffer
- CLI Setup & Panel Importer
- ACME Certs & Event Log
- Account & Inbound JSON Model
- OpenVPN Management Socket
- OpenVPN PKI & Certificates
- Engine & IranDirect Routing
- SQLite Minimal Reader
- Docs & Legacy DB Migration
- Telegram Backup & Alerts
- No-Daemons Stub Interface
- Architecture Rules & Invariants
- Release Workflow & Checklist
- CI & Pre-Push Verification
- Go Module Root

## God Nodes (most connected - your core abstractions)
1. `ok()` - 92 edges
2. `fail()` - 73 edges
3. `API` - 64 edges
4. `nowMs()` - 50 edges
5. `AgencyStore` - 47 edges
6. `agentOf()` - 43 edges
7. `itoa()` - 37 edges
8. `clientIP()` - 28 edges
9. `actorOf()` - 27 edges
10. `testStore()` - 27 edges

## Surprising Connections (you probably didn't know these)
- `Core Development Rules (Locks, Fingerprints, Bot API)` --semantically_similar_to--> `Antigravity Rule: Project Architecture & Invariants`  [INFERRED] [semantically similar]
  GUIDE-FA.md → .agents/rules/project-architecture.md
- `Zero-Downtime Old Panel Migration Guide` --conceptually_related_to--> `main()`  [INFERRED]
  README.md → main.go
- `Cascade (Waterfall) Pricing & Append-Only Ledger Spec` --references--> `LedgerEntry`  [EXTRACTED]
  AGENCY-SPEC.md → agency.go
- `Antigravity Workflow: Pre-Push Verify` --conceptually_related_to--> `CI Workflow (go vet, go test -race, static build)`  [INFERRED]
  .agents/workflows/verify.md → .github/workflows/ci.yml
- `statusOf()` --calls--> `ownerFrozen()`  [INFERRED]
  ui.go → agency.go

## Import Cycles
- None detected.

## Hyperedges (group relationships)
- **LitePanel Core Architecture & Rules** — readme_litepanel_overview, guide_fa_invariants, agency_spec_cascade_model, agents_rules_project_architecture [INFERRED 0.85]

## Communities (27 total, 7 thin omitted)

### Community 0 - "Agency HTTP & Bot API"
Cohesion: 0.05
Nodes (63): actorOf(), agAllowed(), agCtxOf(), agentOf(), agentPublic(), agMaxDevices(), agOwnsCustomer(), agSubtree() (+55 more)

### Community 1 - "Agency Tests & Helpers"
Cohesion: 0.09
Nodes (56): agencyEnv(), allPerms(), bal(), botAdd(), mkAgent(), newTClient(), TestAgencyAPIKeyAndImpersonate(), TestAgencyBackupRoundTrip() (+48 more)

### Community 2 - "Agency Store & Ledger"
Cohesion: 0.06
Nodes (28): containsStr(), defaultAgencySettings(), discount(), AgencyStore, agStatus(), OpenAgency(), ownerFrozen(), hashPass() (+20 more)

### Community 3 - "Daemon Reconcile & Audit Tests"
Cohesion: 0.08
Nodes (36): Store, portsOf(), TestPppOptionsDoNotRestartXl2tpd(), Store, intSetting(), strSetting(), Engine, TestIranDirectRoutes() (+28 more)

### Community 4 - "Config Hashing & TLS Reload"
Cohesion: 0.06
Nodes (15): TestOcservTimersReloadNotRestart(), fingerprint(), writeIfChanged(), containsFold(), Engine, migrateOcservHash(), ocservRestartPart(), writeRadiusClient() (+7 more)

### Community 5 - "Session Enforcement & Shaper"
Cohesion: 0.08
Nodes (12): Store, deadAfterMs(), Store, protoFamily(), burstFor(), isSharedDev(), minorOf(), newShaper() (+4 more)

### Community 6 - "Agency Frontend UI"
Cohesion: 0.13
Nodes (35): agBulkCreate(), agentModal(), agentMoveModal(), agentSel(), balBox(), banModal(), copyBtn(), custModal() (+27 more)

### Community 7 - "Server Installer & Menu"
Cohesion: 0.22
Nodes (30): ask(), ask_login(), confirm(), die(), do_cert(), do_diag(), do_domain(), do_install() (+22 more)

### Community 8 - "HTTP Auth & MSCHAP Crypto"
Cohesion: 0.14
Nodes (13): withAgent(), writeJSON(), challengeResponse(), desKey(), md4(), mschapv1Verify(), mschapv2Verify(), ntHash() (+5 more)

### Community 9 - "Embedded RADIUS Server"
Cohesion: 0.15
Nodes (10): Antigravity Skill: vpn-protocol-and-enforcement, Store, msVSA(), octets(), papDecrypt(), protoOfNAS(), u32attr(), radAttr (+2 more)

### Community 10 - "Core Bot & Panel API"
Cohesion: 0.13
Nodes (11): Antigravity Skill: add-panel-feature, hasAnyPrefix(), readSys(), download(), latestRelease(), selfUpdate(), accountRow, envelope (+3 more)

### Community 11 - "Specs & Core Modules"
Cohesion: 0.14
Nodes (4): newAPIKey(), Antigravity Skill: agency-reseller-development, AgentPricing, PlanPrice

### Community 12 - "HTTP Gzip & Response Buffer"
Cohesion: 0.15
Nodes (5): bufferMW(), gzipMW(), blockingWriter, bufWriter, gzWriter

### Community 13 - "CLI Setup & Panel Importer"
Cohesion: 0.18
Nodes (11): importCmd(), info(), main(), parseDirs(), serve(), setup(), dirOf(), makePanelCert() (+3 more)

### Community 14 - "ACME Certs & Event Log"
Cohesion: 0.19
Nodes (5): anyLocalIP(), leStatus(), applyNft(), nftRuleset(), TestNftRuleset()

### Community 15 - "Account & Inbound JSON Model"
Cohesion: 0.21
Nodes (7): Account, Store, clientJSON, inboundJSON, inboundView, sellSpec, trafficJSON

### Community 17 - "OpenVPN PKI & Certificates"
Cohesion: 0.24
Nodes (5): cloneSettings(), genCerts(), pemOf(), selfSignedPEM(), certBundle

### Community 18 - "Engine & IranDirect Routing"
Cohesion: 0.22
Nodes (6): NewEngine(), writeLogrotate(), Iranian IPv4 CIDR Bypass List (iran-ipv4.txt), killPPP(), pppDevByPeer(), killOcserv()

### Community 19 - "SQLite Minimal Reader"
Cohesion: 0.25
Nodes (7): isSQLite(), parseRecord(), sqlColumns(), sqliteTables(), varint(), sqDB, sqTable

### Community 20 - "Docs & Legacy DB Migration"
Cohesion: 0.27
Nodes (9): Persian Developer Guide & File Map (GUIDE-FA), asInt(), asStr(), stateFromVpnUiDB(), LitePanel (vpn-lite) Overview & Installation, Account, Admin, GlobalSettings (+1 more)

## Knowledge Gaps
- **19 isolated node(s):** `agCtxKey`, `apiLogEntry`, `repRow`, `repAgent`, `Store` (+14 more)
  These have ≤1 connection - possible missing edges or undocumented components. (Counts symbols only; 73 node(s) total have ≤1 connection when file, concept and rationale nodes are included.)
- **7 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `nowMs()` connect `Agency HTTP & Bot API` to `Agency Tests & Helpers`, `Agency Store & Ledger`, `Daemon Reconcile & Audit Tests`, `Config Hashing & TLS Reload`, `Session Enforcement & Shaper`, `Embedded RADIUS Server`, `Core Bot & Panel API`, `OpenVPN Management Socket`, `Docs & Legacy DB Migration`?**
  _High betweenness centrality (0.111) - this node is a cross-community bridge._
- **Are the 70 inferred relationships involving `ok()` (e.g. with `TestReplyIsSentAfterLocksAreReleased()` and `.agActivity()`) actually correct?**
  _`ok()` has 70 INFERRED edges - model-reasoned connections that need verification._
- **What connects `agCtxKey`, `apiLogEntry`, `repRow` to the rest of the system?**
  _19 weakly-connected nodes found - possible documentation gaps or missing edges._
- **Should `Agency HTTP & Bot API` be split into smaller, more focused modules?**
  _Cohesion score 0.05381727158948686 - nodes in this community are weakly interconnected._
- **Why does `AgencyStore` connect `Agency Store & Ledger` to `Specs & Core Modules`, `Config Hashing & TLS Reload`?**
  _High betweenness centrality (0.048) - this node is a cross-community bridge._
- **Are the 59 inferred relationships involving `fail()` (e.g. with `.adminBalance()` and `.agAddClient()`) actually correct?**
  _`fail()` has 59 INFERRED edges - model-reasoned connections that need verification._
- **Should `Agency Tests & Helpers` be split into smaller, more focused modules?**
  _Cohesion score 0.09441441441441441 - nodes in this community are weakly interconnected._