# OpenSSL arm64e Status

Snapshot date: 2026-07-16

## Repo Identity

- Local path: `/Users/tianren/coding/openssl`
- Git form: standalone repository
- Local upstream-tracking branch: `master`
- Local downstream branches:
  - `carry/apple-arm64e-targets`
  - `prep/apple-arm64e-targets`
- Remote repository: `cypherair/openssl`
- Upstream repository: `openssl/openssl`

## Role In The arm64e Chain

This repo is where the OpenSSL-side Apple `arm64e` target definitions live for
the current CypherAir app chain. The other forks depend on this repo to
make the OpenSSL build system understand the relevant Apple `arm64e` targets.

## Current Progress

- The carry line now includes the official upstream `openssl-3.6.3` release
  (`aae016bfd52fcad2bc9657c2c782cfdf73b1ed5f`), which contains the June 2026
  OpenSSL security fixes, while retaining the CypherAir Apple arm64e targets.
- The arm64e Poly1305 assembly path now signs its selected block and emit
  callbacks before storing them. This matches the compiler ABI's
  zero-discriminator function-pointer signing and prevents `EXC_ARM_PAC_FAIL`
  in Poly1305 and ChaCha20-Poly1305 operations.
- The necessary downstream branch lines already exist.
- The `prep` branch is the cleaner upstream-prep line.
- The `carry` branch is the long-lived downstream support line and should be
  treated as such.
- The current arm64e app chain still depends on this fork, even if no new
  local edits are immediately planned.

## Current Meaning Of The Branches

- `carry/apple-arm64e-targets`
  - downstream support branch
  - expected to stay explicit about current CypherAir chain requirements
- `prep/apple-arm64e-targets`
  - cleaner branch for future upstream shaping
  - should stay easier to explain and review than the carry line

## Related Forks And Paths

- App repository:
  - `/Users/tianren/coding/cypherair-main`
  - canonical branch: `main`
- Rust fork:
  - `/Users/tianren/coding/rust`
  - branch `carry/cypherair-arm64e-toolchain-stable-1.97`
- openssl-src-rs fork:
  - `/Users/tianren/coding/openssl-src-rs`
  - branch `carry/apple-arm64e-openssl-fork`

## Upstreaming Posture

- `prep` is the upstream-facing line.
- `carry` is the branch that keeps the current app chain working.
- Do not assume that the carry branch is a simple fast-forwardable "ahead of
  upstream" branch; it is a downstream support line with its own history.

## Update Rules

Update this file whenever any of the following changes:

- the local or remote branch names
- the role split between `carry` and `prep`
- the target-definition strategy for Darwin vs iOS/tvOS/visionOS
- the dependency relationship with `openssl-src-rs`
- the upstreaming strategy for the OpenSSL-side work
