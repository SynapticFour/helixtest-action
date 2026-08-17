# Changelog

## [Unreleased]

### Changed

- Default HelixTest binary pin **v0.1.2** (official DRS/Beacon schemas).
- Docs: GHCR auth-on lives in HelixTest against `ferrum:edge`, not tag `v0.3.1-edge`.

### Added

- Composite action that downloads HelixTest release binaries (sha256-checked) and runs `--mode ferrum` or `ferrum+infra`. Does not start servers. Not GA4GH certification.
