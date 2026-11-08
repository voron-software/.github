# Contributing

This guide applies to every voron-software repository that has no `CONTRIBUTING.md` of its own.

## Proposing a change

- Members push a branch to the repository. Everyone else opens the pull request from a fork.
- Open the pull request against `main`. Direct pushes to `main` are rejected.
- Pull requests are squash-merged, and the PR title becomes the commit subject on `main`. Merge commits and rebase merges are disabled.
- Write the PR title as a one-line summary of the change. Conventional prefixes such as `fix:`, `ci:` or `docs:` are common and Renovate always uses them, but no check enforces them.
- Resolve every review conversation before merging.

## Checks

Get CI green before asking for review. Rust repositories run these checks in CI:

```sh
cargo fmt --all --check
cargo clippy --workspace --all-targets --all-features -- -D warnings
cargo test --workspace --all-features
cargo deny check advisories bans licenses sources
```

- `rust-toolchain.toml` pins the toolchain and components where present, and rustup installs them on first use.
- Each repository's `.github/workflows/` is authoritative, and some repositories run additional jobs.
- Where a repository runs zizmor, changes under `.github/workflows/` must pass it.

## Documentation

Docs change with the code, in the same pull request. A missing doc change is reviewed like a missing test.

## Dependencies

- Renovate opens dependency PRs weekly and automerges them once CI passes. Security updates do not wait for the weekly schedule.
- Every repository extends the shared preset in [`renovate.json5`](https://github.com/voron-software/.github/blob/main/renovate.json5). Shared behaviour changes there, and repository-specific behaviour changes in the repository's `.github/renovate.json5`.
- When a dependency PR goes red, fix the code so the update passes. Never add Renovate rules that pin, ignore or disable a dependency to make the PR pass.

## License

Public repositories carry a `LICENSE` file that governs them.
