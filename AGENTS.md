# CypherAir OpenSSL arm64e Carry Guide

This checkout is the CypherAir OpenSSL fork used by the Apple `arm64e`
dependency chain.

## Repo Identity

- Local path: `/Users/tianren/coding/openssl`
- Remote repository: `cypherair/openssl`
- Upstream repository: `openssl/openssl`
- Local upstream-tracking branch: `master`
- Local downstream branches of interest:
  - `carry/apple-arm64e-targets`
  - `prep/apple-arm64e-targets`

## Related Forks

- App experiment worktree:
  - `/Users/tianren/coding/cypherair-apple-arm64e-unified-experiment`
- Rust fork:
  - `/Users/tianren/coding/rust`
  - branch `codex/arm64e-darwin-ptrauth-spike`
- OpenSSL glue fork:
  - `/Users/tianren/coding/openssl-src-rs`
  - branch `carry/apple-arm64e-openssl-fork`
- Related but currently unconfirmed in the active arm64e chain:
  - `/Users/tianren/coding/rust-openssl`

## Current Role

This repo carries the OpenSSL-side target definitions that the CypherAir Apple
`arm64e` chain depends on.

Important config targets include:

- `darwin64-arm64e`
- `ios64e-cross`

Current downstream strategy:

- Darwin `arm64e` uses `darwin64-arm64e`
- iOS / tvOS / visionOS `arm64e` reuse `ios64e-cross`
  while the caller chooses the correct Apple SDK via `xcrun` / `CC`

Detailed arm64e progress belongs in [ARM64E_STATUS.md](ARM64E_STATUS.md).
Update that file whenever the carry/prep split, target definitions, or chain
dependencies change.

## Working Rules

- If a change is required for the active dependency chain, land it on the
  `carry` branch.
- If the same change is clean enough for an upstream-shaped line, replay it
  onto `prep`.
- Keep comments explicit when a config target is reused across iOS / tvOS /
  visionOS through SDK override instead of through separate OpenSSL-native
  target names.
- Do not describe `prep` as the same thing as `carry`; each branch has a
  different purpose and should stay documented separately.
