# Changelog

## [Unreleased]

### Changed

- Default HelixTest binary pin **v0.1.3** (same as the HelixTest suite / Ferrum `VERSIONS.lock` tag). Release assets exist for linux-gnu x86_64/aarch64 and darwin aarch64.
- Docs: GHCR auth-on lives in HelixTest against `ferrum:edge`, not tag `v0.3.1-edge`.
- Historical default was **v0.1.2** (DRS/Beacon schema cut). Do not treat older README screenshots as the current default.

### Added

- Composite action that downloads HelixTest release binaries (sha256-checked) and runs `--mode ferrum` or `ferrum+infra`. Does not start servers. Not GA4GH certification.
