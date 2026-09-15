# Changelog — `armature-aws`

All notable changes to this crate will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this crate adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

Earlier changes are recorded in the workspace [`CHANGELOG.md`](../CHANGELOG.md).

## [Unreleased]

## [0.2.2] - 2026-09-15

### Changed

- AWS SDK dependencies bumped: `aws-config` 1.8→1.12, `aws-credential-types` 1.2→1.3, `aws-types` 1.3→1.6, and every optional `aws-sdk-*` client to one release short of its newest (e.g. `aws-sdk-s3` 1.122→1.146). Newer `aws-sdk-*` releases require `aws-smithy-types` 1.7, whose reshaped `Document::Object` does not compile against the `aws-smithy-json` 0.63 that `aws-config` 1.12 still depends on. These crates are re-exported, so dependents must allow these minimums.
- A direct `aws-smithy-types >=1.6.3, <1.7` requirement keeps a fresh resolve on the SDK releases held back above; without it the resolver picks `aws-sdk-*`/`aws-runtime` releases that need `aws-smithy-types` 1.7 and fail to build against `aws-config` 1.12.
- AWS SDK dependencies no longer enable their default features, dropping the SDK's legacy hyper-0.14 client and its `h2 0.3` (RUSTSEC-2026-0258); the hyper-1 `default-https-client` and `rt-tokio` (plus `sigv4a`/`http-1x` where the SDK enabled them by default) are kept.
- The MSRV CI job also checks `--all-features`, so the optional AWS SDK dependencies are built on the MSRV toolchain.

