# Changelog

All notable changes to `Tamp.CycloneDx.V6` are recorded here. The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/); versions follow [SemVer](https://semver.org/spec/v2.0.0.html).

## [1.11.2] — Unreleased

### Added

- Package now ships XML documentation files (`.xml`) alongside the assembly, so consumers get IntelliSense and API docs. (Mirrors [tamp-build/tamp#3](https://github.com/tamp-build/tamp/pull/50).)

### Changed

- **TAM-254 / TAM-259 — Repository migration.** `Tamp.CycloneDx.V6` moved out of the main `tamp` monorepo into its own satellite repo (`tamp-build/tamp-cyclonedx`). Package ID, namespace, public API, and version line are unchanged — adopters see no break.
- Picked up at 1.11.2 from the prior main-repo release at 1.11.1. From here forward this wrapper's release cadence tracks `dotnet-CycloneDX` instead of the whole `tamp` framework's central version.

## [1.11.1] and earlier

Shipped from the main `tamp` monorepo. See [`tamp-build/tamp` CHANGELOG](https://github.com/tamp-build/tamp/blob/main/CHANGELOG.md) for the pre-migration history.
