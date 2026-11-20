Prefix: OXSH
Next: 4

# Open work
### OXSH-1 · P3 · Cover server command line behavior

- **Area:** CLI verification
- **Where:** oxish/src/bin/oxish-server.rs, AGENTS.md
- **Problem:** The server command line flags and exit statuses have no identified boundary test; changes to argument validation and startup diagnostics can regress without focused coverage.
- **Recommendation:** Add process-level tests for supported and invalid argument combinations, with a negative control for a real contract.
- **Fix with:** test-audit
- **Effort:** M

### OXSH-2 · P3 · Benchmark SSH and Git transfer workloads

- **Area:** Performance · workloads
- **Where:** oxish/src/session/connections.rs, oxish/src/git.rs
- **Problem:** There is no repository benchmark harness for SSH session traffic or Git transfers, so changes on those paths lack a repeatable performance workload.
- **Recommendation:** Define representative small and large SSH and Git workloads with edit and change entry points and measure them on suitable hardware.
- **Fix with:** refactor-benchmarks
- **Effort:** M

### OXSH-3 · P3 · Tag releases cannot resolve the patched graviola

- **Area:** CI · release
- **Where:** .github/workflows/release.yml (cargo-dist generated); dist-workspace.toml
- **Problem:** Cargo.toml patches graviola to ../graviola (ssh-build vendor/graviola). The cargo-dist release workflow checks out only this repository, so plan and build jobs fail on a tag push the same way pull-request jobs did before the ci.yml fix. The pull_request trigger was removed because the fork has never tagged a release here; oxish binaries ship through laputa-systems/ssh-build.
- **Recommendation:** If this fork should publish its own releases, add the pinned ssh-build checkout and link to the dist jobs through dist configuration (or allow-dirty for ci) and regenerate; otherwise delete the dist release workflow.
- **Fix with:** build-repos
- **Effort:** S

