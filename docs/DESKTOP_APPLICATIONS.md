# Desktop application allocation

Verified **2026-08-05**.

Voxletra uses the paired native desktop application standard:

- Rust: [`voxletra/vxl-desktop.rs`](https://github.com/voxletra/vxl-desktop.rs) — **planned**, not yet verified as a published repository.
- Flutter: [`voxletra/vxl-flutter`](https://github.com/voxletra/vxl-flutter) — **live**.

The Rust URL is an allocation target, not proof that the remote exists. Do not mark it live until the repository, native targets, media integrations, tests, packaging, and supported-platform matrix are verified.

The live Flutter repository records the companion contract in [`COMPANION_DESKTOP.md`](https://github.com/voxletra/vxl-flutter/blob/main/COMPANION_DESKTOP.md), merged through [PR #4](https://github.com/voxletra/vxl-flutter/pull/4).

## Product boundary

Both implementations should support semantic parity for media import and capture, transcription, editing, timelines, search, export, local processing, long-running jobs, progress recovery, secure local storage, and per-platform media integration.

The Rust and Flutter implementations remain independently buildable, testable, releasable applications. Shared schemas, clients, fixtures, sample media, golden files, job-state models, and conformance tests should be versioned deliberately.

## Feature-delivery rule

Every desktop-facing change must inspect both implementations, define shared acceptance criteria, update both or record an explicit no-change rationale, and report Rust and Flutter status separately for every supported operating system.

## Project routing

- GitHub Project: [`voxletra-project` — Project 1](https://github.com/orgs/voxletra/projects/1)
- Linear project: `github.com/voxletra`
- Central registry: [`approved-private-registry`](private-registry://canonical/registry/desktop-applications.json)
- Portfolio rollout: [`DEN-2469`](https://linear.app/denman/issue/DEN-2469/roll-out-paired-rust-flutter-desktop-repositories-across-the-portfolio)

Repository creation, renames, transfers, archival, or platform-status changes must update this document, Linear, the central registry, and both companion repositories together.
