## Verification

- Standalone builds require ssh-build's patched graviola at `../graviola` (vendor/graviola at ssh-build 569d0bd with its SSH ChaCha20-Poly1305 patch). CI does not currently provision it; see the backlog.
- `make test` runs workspace unit, integration, and documentation tests; `make lint` runs workspace Clippy on all targets and features. Ground on macOS arm64: cold test 164.44s, warm 92.96s including build-lock contention (main test binary 29.43s), lint 42.54s; 70 tests passed.
- SSH authentication and authorized key options: `oxish-proto` key option tests and `oxish::tests::verify_keys`.
- SSH wire negotiation and encryption: `oxish::tests::handshake_*` and `oxish-graviola` OpenSSH vector and tampering tests.
- Git command and access policy: `oxish::git::tests` and `oxish::tests::exec_git_*`.
- Host-key file format: `oxish::tests::host_keys_from_files_graviola` and `openssh_keygen_agrees`.
- Session state format: `oxish::tests::session_state_round_trip`.
- Server CLI flags and exit codes: none.
- Library consumers: ssh-build and xsh; validate affected consumer tests against the candidate for API changes.
- Performance workload: none; no benchmark suite is present. SSH and Git transfer paths are performance-sensitive.
