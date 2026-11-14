# Graph Report - VPN Lite  (2026-11-15)

## Corpus Check
- 48 files · ~69,580 words
- Verdict: corpus is large enough that graph structure adds value.
- Unclassified: 3 file(s) not represented in the graph (top: (none) 2, .db 1)

## Summary
- 890 nodes · 2852 edges · 37 communities (31 shown, 6 thin omitted)
- Extraction: 83% EXTRACTED · 17% INFERRED · 0% AMBIGUOUS · INFERRED: 482 edges (avg confidence: 0.85)
- Token cost: 0 input · 0 output

## Graph Freshness
- Built from commit: `3ba35a86`
- Run `git rev-parse HEAD` and compare to check if the graph is stale.
- Run `graphify update .` after code changes (no API cost).

## Community Hubs (Navigation)
- net/http.Request
- testing.T
- AgencyStore
- Inbound
- certs.go
- Session
- agency.js
- install.sh
- mschap.go
- radius.go
- ui.go
- Reseller / Agency Module Development
- agency_test.go
- main.go
- go_pkg_time
- model.go
- shaper.go
- ۱) مدل داده
- go_pkg_strings
- sqlitelite.go
- store.go
- Store
- audit_test.go
- LitePanel (vpn-lite) Architecture & Invariants
- Build, Verify & Release
- verify.md
- vpnlite
- LitePanel (vpn-lite)
- مشخصات کامل «بخش نمایندگی» + «قانون رعایت کاربر»
- راهنمای کامل توسعه‌ی پنل VPN Lite (نسخه‌ی v0.3.1)
- قانون رعایت کاربر (سقف اتصال همزمان)
- Adding a Feature to LitePanel
- ۴) نقشه‌ی فایل‌ها
- ۲) مدل پول («آبشاری»)
- VPN Protocols, RADIUS & Enforcement
- CI Workflow (go vet, go test -race, static build)
- GitHub Release Workflow (linux amd64/arm64 + SHA256SUMS)

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
- `statusOf()` --calls--> `ownerFrozen()`  [INFERRED]
  ui.go → agency.go
- `agencyEnv()` --calls--> `OpenAgency()`  [INFERRED]
  agency_test.go → agency.go
- `TestAgencyConcurrentSalesNeverOverspend()` --calls--> `OpenAgency()`  [INFERRED]
  agency_test.go → agency.go
- `serve()` --calls--> `OpenAgency()`  [INFERRED]
  main.go → agency.go
- `runCore()` --calls--> `h()`  [INFERRED]
  agency_http.go → mschap_test.go

## Import Cycles
- None detected.

## Communities (37 total, 6 thin omitted)

### Community 0 - "net/http.Request"
Cohesion: 0.05
Nodes (69): actorOf(), agAllowed(), agCtxOf(), agentOf(), agentPublic(), agMaxDevices(), agOwnsCustomer(), agSubtree() (+61 more)

### Community 1 - "testing.T"
Cohesion: 0.17
Nodes (27): jsonDecode(), TestTrafficSavedLazily(), seed(), TestAccountChangesNeverDisconnect(), TestBackupRestoreAndImport(), TestBotAPIContract(), TestDefaultPolicyRejectsNewConnectionWhenFull(), TestImportFromOldPanel() (+19 more)

### Community 2 - "AgencyStore"
Cohesion: 0.06
Nodes (29): containsStr(), defaultAgencySettings(), discount(), AgencyStore, agStatus(), newAPIKey(), OpenAgency(), Activity (+21 more)

### Community 3 - "Inbound"
Cohesion: 0.07
Nodes (35): portsOf(), TestPppOptionsDoNotRestartXl2tpd(), intSetting(), strSetting(), Engine, TestIranDirectRoutes(), ciscoPlainRoutes(), iranLargest() (+27 more)

### Community 4 - "certs.go"
Cohesion: 0.08
Nodes (18): TestOcservTimersReloadNotRestart(), cloneSettings(), genCerts(), Store, pemOf(), fingerprint(), writeIfChanged(), Engine (+10 more)

### Community 5 - "Session"
Cohesion: 0.11
Nodes (8): ownerFrozen(), Store, deadAfterMs(), Store, protoFamily(), AuthResult, Session, SessionTable

### Community 6 - "agency.js"
Cohesion: 0.13
Nodes (35): agBulkCreate(), agentModal(), agentMoveModal(), agentSel(), balBox(), banModal(), copyBtn(), custModal() (+27 more)

### Community 7 - "install.sh"
Cohesion: 0.22
Nodes (30): ask(), ask_login(), confirm(), die(), do_cert(), do_diag(), do_domain(), do_install() (+22 more)

### Community 8 - "mschap.go"
Cohesion: 0.06
Nodes (23): withAgent(), bufferMW(), gzipMW(), challengeResponse(), desKey(), md4(), mschapv1Verify(), mschapv2Verify() (+15 more)

### Community 9 - "radius.go"
Cohesion: 0.29
Nodes (8): papEnc(), radReq(), TestRadiusAccounting(), TestRadiusPAPAndMSCHAP(), msVSA(), parseRad(), u32attr(), radAttr

### Community 10 - "ui.go"
Cohesion: 0.13
Nodes (8): hasAnyPrefix(), readSys(), download(), latestRelease(), selfUpdate(), accountRow, sysInfo, Embedded Single-Page Admin UI (web/index.html)

### Community 11 - "Reseller / Agency Module Development"
Cohesion: 0.50
Nodes (3): Key Invariants, Required Verification, Reseller / Agency Module Development

### Community 12 - "agency_test.go"
Cohesion: 0.34
Nodes (16): agencyEnv(), allPerms(), bal(), botAdd(), mkAgent(), newTClient(), TestAgencyAPIKeyAndImpersonate(), TestAgencyBackupRoundTrip() (+8 more)

### Community 13 - "main.go"
Cohesion: 0.09
Nodes (11): importCmd(), info(), main(), parseDirs(), serve(), setup(), Store, OpenStore() (+3 more)

### Community 14 - "go_pkg_time"
Cohesion: 0.20
Nodes (3): applyNft(), nftRuleset(), TestNftRuleset()

### Community 15 - "model.go"
Cohesion: 0.14
Nodes (10): containsFold(), Account, Store, clientJSON, Event, eventLog, inboundJSON, inboundView (+2 more)

### Community 16 - "shaper.go"
Cohesion: 0.27
Nodes (5): burstFor(), isSharedDev(), minorOf(), newShaper(), shaper

### Community 17 - "۱) مدل داده"
Cohesion: 0.20
Nodes (10): تنظیمات نمایندگی, دسترسی‌ها (perms، همه بولی), ذخیره‌سازی, ردیف دفتر (LedgerEntry), قیمت‌گذاری نماینده (pricing), محدودیت‌ها (limits، ۰ = بدون محدودیت), مشتری (Customer), نماینده (Agent) (+2 more)

### Community 18 - "go_pkg_strings"
Cohesion: 0.15
Nodes (7): anyLocalIP(), NewEngine(), writeLogrotate(), Iranian IPv4 CIDR Bypass List (iran-ipv4.txt), killPPP(), pppDevByPeer(), killOcserv()

### Community 19 - "sqlitelite.go"
Cohesion: 0.25
Nodes (7): isSQLite(), parseRecord(), sqlColumns(), sqliteTables(), varint(), sqDB, sqTable

### Community 20 - "store.go"
Cohesion: 0.31
Nodes (7): asInt(), asStr(), stateFromVpnUiDB(), Account, Admin, GlobalSettings, State

### Community 22 - "audit_test.go"
Cohesion: 0.27
Nodes (8): resetSessions(), TestAccountKeysNormalized(), TestDaemonKeptOnRenderFailure(), TestDaemonReloadSendsHup(), TestDeadSessionIsReplaced(), TestInterimAfterRestartNotCountedTwice(), TestReplyIsSentAfterLocksAreReleased(), newDaemonSet()

### Community 24 - "Build, Verify & Release"
Cohesion: 0.40
Nodes (4): 1. Static Checks & Race Tests, 2. Local Panel Smoke Test (No VPN Daemons Required), 3. Versioning & GitHub Releases, Build, Verify & Release

### Community 27 - "LitePanel (vpn-lite)"
Cohesion: 0.22
Nodes (6): Design, Development, Files on server, Install (any Debian/Ubuntu server), LitePanel (vpn-lite), Move from the old panel (no downtime until you choose)

### Community 28 - "مشخصات کامل «بخش نمایندگی» + «قانون رعایت کاربر»"
Cohesion: 0.22
Nodes (9): API قدیمی برای نماینده, مسیرهای نمایندگی (`/panel/agency/...`), مشخصات کامل «بخش نمایندگی» + «قانون رعایت کاربر», ۰) اصول غیرقابل‌تغییر, ۳) ورود و نشست, ۴) محدوده‌ی دید و مسیرها, ۵) قواعد مدیریتی, ۶) همزمانی و ایمنی (+1 more)

### Community 29 - "راهنمای کامل توسعه‌ی پنل VPN Lite (نسخه‌ی v0.3.1)"
Cohesion: 0.22
Nodes (9): راهنمای کامل توسعه‌ی پنل VPN Lite (نسخه‌ی v0.3.1), ۱) پنل چیست, ۲) ساخت، تست، اجرا, ۳) مسیرها روی سرور, ۵) قواعدی که هنگام توسعه نباید شکسته شود, ۶) چطور یک چیز جدید اضافه کنیم, ۷) انتشار نسخه, ۸) تاریخچه‌ی کوتاه نسخه‌ها (+1 more)

### Community 30 - "قانون رعایت کاربر (سقف اتصال همزمان)"
Cohesion: 0.25
Nodes (8): اتصال مرده جای کاربر را نمی‌گیرد, بازبینی دوره‌ای, ترتیب بررسی هنگام ورود, سقف, قانون رعایت کاربر (سقف اتصال همزمان), وقتی سقف پر است (تنظیم سراسری `limitStrategy`), چیزهایی که باید در لاگ دیده شود, یک پروتکل در هر لحظه

### Community 31 - "Adding a Feature to LitePanel"
Cohesion: 0.29
Nodes (6): 1. Global Settings Field, 2. Account Field, 3. HTTP Route, 4. Frontend Page, 5. Validation, Adding a Feature to LitePanel

### Community 32 - "۴) نقشه‌ی فایل‌ها"
Cohesion: 0.40
Nodes (5): بقیه, نمایندگی, هسته, پروتکل‌ها, ۴) نقشه‌ی فایل‌ها

### Community 33 - "۲) مدل پول («آبشاری»)"
Cohesion: 0.50
Nodes (4): بازگشت وجه هنگام حذف, محاسبه‌ی قیمت, هزینه‌ی عملیات, ۲) مدل پول («آبشاری»)

### Community 34 - "VPN Protocols, RADIUS & Enforcement"
Cohesion: 0.50
Nodes (3): Architecture Overview, Rules When Editing, VPN Protocols, RADIUS & Enforcement

## Knowledge Gaps
- **71 isolated node(s):** `agCtxKey`, `apiLogEntry`, `repRow`, `repAgent`, `Store` (+66 more)
  These have ≤1 connection - possible missing edges or undocumented components. (Counts symbols only; 129 node(s) total have ≤1 connection when file, concept and rationale nodes are included.)
- **6 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `nowMs()` connect `net/http.Request` to `testing.T`, `AgencyStore`, `Inbound`, `Session`, `mschap.go`, `agency_test.go`, `model.go`, `store.go`, `audit_test.go`?**
  _High betweenness centrality (0.095) - this node is a cross-community bridge._
- **Are the 70 inferred relationships involving `ok()` (e.g. with `TestReplyIsSentAfterLocksAreReleased()` and `.agActivity()`) actually correct?**
  _`ok()` has 70 INFERRED edges - model-reasoned connections that need verification._
- **What connects `agCtxKey`, `apiLogEntry`, `repRow` to the rest of the system?**
  _71 weakly-connected nodes found - possible documentation gaps or missing edges._
- **Should `net/http.Request` be split into smaller, more focused modules?**
  _Cohesion score 0.050351228016202634 - nodes in this community are weakly interconnected._
- **Why does `AgencyStore` connect `AgencyStore` to `main.go`, `model.go`?**
  _High betweenness centrality (0.040) - this node is a cross-community bridge._
- **Are the 59 inferred relationships involving `fail()` (e.g. with `.adminBalance()` and `.agAddClient()`) actually correct?**
  _`fail()` has 59 INFERRED edges - model-reasoned connections that need verification._
- **Should `AgencyStore` be split into smaller, more focused modules?**
  _Cohesion score 0.061828952239911146 - nodes in this community are weakly interconnected._