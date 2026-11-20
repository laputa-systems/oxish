Prefix: DSLP
Next: 8

Deslop campaign backlog ([plan](https://github.com/laputa-systems/stuff/blob/main/docs/campaigns/deslop.md), tier E). One agent works this file with the `deslop` skill: take the lowest-numbered open ticket whose area does not start with `Needs owner ·`. After DSLP-5, work the open P1 and P2 findings, then fill in `## Report` below.

## Report

Not started.

## Tickets

### DSLP-3 · P2 · Types: strict profile and typing findings

- **Area:** deslop · types
- **Where:** type checker and lint configuration; Rust sources
- **Problem:** The strict-profile candidates in the deslop skill's tools reference have not been measured here.
- **Recommendation:** Run the deslop Types step. Accept: clean at the adopted profile, escape hatches not increased, witnesses recorded.
- **Fix with:** deslop
- **Effort:** M

### DSLP-4 · P2 · Tests: coverage, boundary gaps, mutation

- **Area:** deslop · tests
- **Where:** test suites and CI
- **Problem:** Coverage and mutation results are unmeasured; no deslop mutation lane exists.
- **Recommendation:** Run the deslop Tests step. Accept: no undispositioned survivor in critical code, the test cost budget holds, and the lane is green where the tools are mirrored.
- **Fix with:** deslop
- **Effort:** M

### DSLP-5 · P2 · Dead code: tools and debloat

- **Area:** deslop · dead code
- **Where:** whole repository (our changes)
- **Problem:** No dead-code scan has run.
- **Recommendation:** Run the deslop Dead code step. Accept: tools clean or allowlisted with reasons; walk-backs filed as Needs owner tickets.
- **Fix with:** deslop
- **Effort:** M

### DSLP-6 · P2 · Provide patched graviola to clean checkout CI

- **Area:** Needs owner · CI dependency
- **Where:** Cargo.toml, .github/workflows/ci.yml
- **Problem:** The workspace patches graviola to ../graviola, but CI checks out only oxish. Fork CI run 43700946648 failed with patch location /home/runner/work/oxish/graviola does not contain packages matching graviola; the local patched source is supplied separately by ssh-build. Clean checkout CI cannot build oxish-graviola.
- **Recommendation:** Decide how to supply the patched graviola source to standalone builds and CI; this pass is not authorized to change the patch mechanism.
- **Fix with:** none
- **Effort:** M

### DSLP-7 · P3 · Cover server command line behavior

- **Area:** CLI verification
- **Where:** oxish/src/bin/oxish-server.rs, AGENTS.md
- **Problem:** The server command line flags and exit statuses have no identified boundary test; changes to argument validation and startup diagnostics can regress without focused coverage.
- **Recommendation:** Add process-level tests for supported and invalid argument combinations, with a negative control for a real contract.
- **Fix with:** test-audit
- **Effort:** M

