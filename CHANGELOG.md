# Changelog

[← Back to overview](README.md)

The notes below reflect the project's existing product documentation. This repository currently publishes its application code inside `k_backfire.zip`; the archive has not been independently unpacked or live-tested as part of this documentation-only update.

## 1.8.1 — documented radio hotfix

- Reduced repeated engine audio assignment during exhaust events by caching per-vehicle audio selection.
- Added logic intended to preserve the driver's radio station, including the OFF state, when changing engine audio.
- Retained the updated tablet interface and persistent power-toggle behavior.

**Verification:** the radio fix still needs testing on a live server with the exact ZIP distributed here.

## Earlier tablet updates — version not separately verified

- Updated the tablet frame, navigation and appearance options.
- Adjusted the ON/OFF workflow and persistence behavior across subsequent purchases.
- Improved layout handling for narrower screens.

For installation and upgrade instructions, see the [installation guide](docs/INSTALLATION.md). Avoid treating this changelog as proof of tests or performance benchmarks.
