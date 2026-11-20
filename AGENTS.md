## Verification

- Standalone builds require ssh-build's patched graviola at `../graviola`. CI checks out `laputa-systems/ssh-build` at `7f4f5157018f3c8544653d8a784169aee3a3b945` and links its `vendor/graviola` there. To update the pin, verify the vendor includes the SSH ChaCha20-Poly1305 patch, update each checkout ref, refresh `Cargo.lock`, and run the workspace tests and lint.
- `make test` runs workspace unit, integration, and documentation tests; `make lint` runs workspace Clippy on all targets and features. Ground on macOS arm64: cold test 164.44s, warm 92.96s including build-lock contention (main test binary 29.43s), lint 42.54s; 70 tests passed.
- Test tiers: `oxish` has 51 unit and SSH/Git integration tests, `oxish-graviola` has 5 vector tests, and `oxish-proto` has 13 unit and 1 decode integration test. A subsequent warm run took 6.06s (main binary 4.86s). `test-pyramid`, coverage, and mutation tools are unavailable locally.
- Hand faults caught: bypassing Git write authorization; accepting keys without Git access; following authorized-key symlinks; allowing one extra cipher nonce; mapping cipher authentication failure to an invalid-length error; and accepting invalid signatures. All faults were restored; `git diff --exit-code -- oxish-proto/src/auth.rs` confirmed the temporary upstream edit was restored.
- SSH authentication and authorized key options: `oxish-proto` key option tests and `oxish::tests::verify_keys`.
- SSH wire negotiation and encryption: `oxish::tests::handshake_*` and `oxish-graviola` OpenSSH vector and tampering tests.
- Git command and access policy: `oxish::git::tests` and `oxish::tests::exec_git_*`.
- Host-key file format: `oxish::tests::host_keys_from_files_graviola` and `openssh_keygen_agrees`.
- Session state format: `oxish::tests::session_state_round_trip`.
- Server CLI flags and exit codes: none.
- Library consumers: ssh-build and xsh; validate affected consumer tests against the candidate for API changes.
- Performance workload: none; no benchmark suite is present. SSH and Git transfer paths are performance-sensitive.
