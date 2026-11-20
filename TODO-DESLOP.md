Prefix: DSLP
Next: 11

Deslop campaign backlog ([plan](https://github.com/laputa-systems/stuff/blob/main/docs/campaigns/deslop.md), tier E). One agent works this file with the `deslop` skill: take the lowest-numbered open ticket whose area does not start with `Needs owner ·`. After DSLP-5, work the open P1 and P2 findings, then fill in `## Report` below.

## Report

Scope: our changes against upstream `dd34280` (base `3c52aa2`), about 4k
diverged lines in `oxish/` and `oxish-graviola/`.

| Step | Commit | Result |
| --- | --- | --- |
| Ground | `6bdcc85` | Root `make test` / `make lint`, PR workflow entry points, AGENTS.md Verification. Standalone builds need ssh-build's patched graviola at `../graviola`. Warm `make test` 70 passed (about 57 s under a 4-core cap on a busy host); `make lint` about 25 to 42 s. |
| Diagnose | `20ffdb1` | `ultrareview` unavailable; a bounded manual review of fork authentication and Git authorization. Filed DSLP-7 (P3, CLI coverage). |
| Types | `9a56ceb` | Strict Clippy candidates measured. No defect witness, so none adopted. |
| CI | `314707e`, `e53498e` | Every CI job checks out laputa-systems/ssh-build at `7f4f515` and links its patched `vendor/graviola`. The cargo-deny container job keeps both checkouts inside the workspace. Fixes DSLP-6 and DSLP-10: clean CI checkouts could not resolve the patch. |
| Tests | `f7cd898` | Six hand-injected faults caught and restored: Git write authorization, missing key access, key-file symlink following, cipher nonce limit, ciphertext error handling, and forged or replayed signature rejection. Coverage and automated mutation are unavailable (tools not mirrored). |
| Dead code | `06efb66` | `cargo check --workspace --all-targets` has no warnings. Dependency scanners unavailable; no removal. |
| Bench | this commit | No benchmark harness. SSH session and Git transfer workloads are filed as DSLP-9 (P3). |

Needs environment: coverage, automated mutation, dependency scanners and a
benchmark workload.
Remaining tickets: DSLP-7 and DSLP-9 (P3).

## Tickets

### DSLP-7 · P3 · Cover server command line behavior

- **Area:** CLI verification
- **Where:** oxish/src/bin/oxish-server.rs, AGENTS.md
- **Problem:** The server command line flags and exit statuses have no identified boundary test; changes to argument validation and startup diagnostics can regress without focused coverage.
- **Recommendation:** Add process-level tests for supported and invalid argument combinations, with a negative control for a real contract.
- **Fix with:** test-audit
- **Effort:** M

### DSLP-9 · P3 · Benchmark SSH and Git transfer workloads

- **Area:** Performance · workloads
- **Where:** oxish/src/session/connections.rs, oxish/src/git.rs
- **Problem:** There is no repository benchmark harness for SSH session traffic or Git transfers, so changes on those paths lack a repeatable performance workload.
- **Recommendation:** Define representative small and large SSH and Git workloads with edit and change entry points and measure them on suitable hardware.
- **Fix with:** refactor-benchmarks
- **Effort:** M

