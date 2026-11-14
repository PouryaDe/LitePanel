---
name: add-panel-feature
description: >-
  Use this skill when adding new settings, account fields, HTTP API or UI routes,
  or frontend pages to LitePanel across Go backend files and embedded web assets.
---

# Adding a Feature to LitePanel

Follow these exact integration points so backend state, bot API compatibility, embedded UI, and tests stay consistent.

## 1. Global Settings Field
1. Add the field (with JSON tag) to `GlobalSettings` in `store.go`. Set any non-zero default in `OpenStore` if needed.
2. Read and write the field in `uiGetSettings` and `uiSetSettings` in `ui.go` (apply validation/defaults before saving under `st.mu`, then `st.touch()`).
3. If the setting affects daemon configs or enforcement, trigger `a.d.ReloadInbound(0)` or update atomic flags (e.g., `setIranDirect` in `main.go`/`ui.go`).
4. Add the control in `pSettings` inside `web/index.html` and add translations to both `T.fa` and `T.en`.

## 2. Account Field
1. Add the field to `Account` in `store.go`.
2. If the Telegram bot or `/panel/api/inbounds/...` needs it, add it to `clientJSON` and `(a *Account) client()` in `model.go`.
3. Handle parsing and updates in `addClient` and `updateClient` in `api.go` (and `agAddClient` / `agUpdateClient` in `agency_http.go` if resellers are allowed to set or view it).
4. Expose it in `accountRow` and `uiAccounts` in `ui.go`.
5. Update the account form/table in `web/index.html` (and `web/agency.js` if applicable).

## 3. HTTP Route
- **Bot/Core API (`/panel/api/inbounds/...`)**: Register in `(a *API) Handler()` in `api.go` using `g` / `po` (admin-only) or `ga` / `pa` (admin + reseller handler). Never break `{success, msg, obj}` responses.
- **Panel UI (`/panel/ui/...`)**: Register in `(a *API) uiRoutes(mux)` in `ui.go` using `u(...)` (admin-only) or `ua(..., adminFn, agentFn)`.
- **Agency (`/panel/agency/...`)**: Register in `(a *API) agencyRoutes(mux)` in `agency_http.go` with the appropriate role guard (`roleAny`, `roleAdmin`, `roleAgent`, or `roleManager`).

## 4. Frontend Page
- **Admin UI (`web/index.html`)**: Implement `async function pName(c)`, register it in `PAGES`, `ICON`, and `PAGEFN`, and add navigation labels in `T.fa` and `T.en`. Reuse helpers (`h`, `t`, `call`, `post`, `modal`, `field`, `toast`, `fmtB`, `fmtDate`, `expiryEditor`).
- **Reseller UI (`web/agency.js`)**: Register reseller/agency pages inside `agencySetup`.

## 5. Validation
1. Run `go vet ./... && go test -race ./...`.
2. Add or update unit/integration tests in `engine_test.go`, `agency_test.go`, or `audit_test.go`.
3. Update the knowledge graph with `graphify update .`.
