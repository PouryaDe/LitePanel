---
name: verify
description: Run Go vet, race tests, static build check, and update the graphify knowledge graph before committing or pushing.
---

# Workflow: Verify Before Push

1. Run static analysis and race-detector tests:
   `go vet ./... && go test -race ./...`
2. Verify static Linux binary compilation:
   `CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -trimpath -o dist/vpn-lite-linux-amd64 .` (and clean up `dist/` afterwards).
3. Refresh the graphify knowledge graph if any Go or doc files changed:
   `graphify update .`
4. Review `git status` and `git diff` to ensure no unintended artifacts or secrets are staged.
