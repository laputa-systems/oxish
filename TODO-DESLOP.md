Prefix: DSLP
Next: 8

Deslop campaign backlog ([plan](https://github.com/laputa-systems/stuff/blob/main/docs/campaigns/deslop.md), tier E). One agent works this file with the `deslop` skill: take the lowest-numbered open ticket whose area does not start with `Needs owner ·`. After DSLP-5, work the open P1 and P2 findings, then fill in `## Report` below.

## Report

Not started.

## Tickets

### DSLP-5 · P2 · Dead code: tools and debloat

- **Area:** deslop · dead code
- **Where:** whole repository (our changes)
- **Problem:** No dead-code scan has run.
- **Recommendation:** Run the deslop Dead code step. Accept: tools clean or allowlisted with reasons; walk-backs filed as Needs owner tickets.
- **Fix with:** deslop
- **Effort:** M

### DSLP-7 · P3 · Cover server command line behavior

- **Area:** CLI verification
- **Where:** oxish/src/bin/oxish-server.rs, AGENTS.md
- **Problem:** The server command line flags and exit statuses have no identified boundary test; changes to argument validation and startup diagnostics can regress without focused coverage.
- **Recommendation:** Add process-level tests for supported and invalid argument combinations, with a negative control for a real contract.
- **Fix with:** test-audit
- **Effort:** M

