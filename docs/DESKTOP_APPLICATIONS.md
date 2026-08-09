# Desktop application allocation

Verified **2026-08-06**.

Voxletra uses the paired desktop application standard:

- Rust: [`voxletra/vxl-desktop.rs`](https://github.com/voxletra/vxl-desktop.rs) — **planned**, not yet verified as a published repository.
- Flutter: [`voxletra/vxl-flutter`](https://github.com/voxletra/vxl-flutter) — **live**.

The Rust target must not be marked live until native builds, media integrations, tests, packaging, and platform support are verified.

## Why both Rust and Flutter remain active

The two applications remain first-class side-by-side implementations so the product can compare audio/media performance, waveform and timeline ergonomics, native file integration, accessibility, mobile reuse, developer velocity, packaging, and long-term maintenance with the same transcription features.

Every desktop-facing feature must inspect both repositories, share acceptance criteria and privacy-safe media fixtures, and normally update both. A one-sided change requires a documented no-change rationale and parity gap.

## Rust desktop kit: Rust + Qt through FFI

**Selected strategy:** Rust domain/core logic with Qt presentation and multimedia integration through a narrow typed FFI boundary, preferably CXX-Qt or an equivalently reviewed bridge.

**WebView policy:** prohibited.

Voxletra needs mature native audio/video APIs, waveforms, timelines, file dialogs, GPU surfaces, long-running media jobs, accessibility, and multi-window behavior. Qt supplies mature native multimedia and presentation while Rust owns transcription orchestration, local processing, validation, persistence, privacy, and concurrency.

FFI rules:

- expose narrow typed commands and value models;
- keep media-job state, credentials, storage, and validation in Rust;
- let Qt own presentation, native media devices, window events, and accessibility;
- avoid broad QObject exposure and untyped QVariant maps at security boundaries; and
- test ABI ownership, thread handoff, cancellation, and failure recovery.

The Rust repository must contain `docs/DESKTOP_TOOLKIT.md` covering the Qt/FFI version policy, multimedia boundary, deep links, tests, packaging, and Flutter companion.

## HTTPS-first deep linking

Canonical form:

```text
https://<verified-voxletra-owned-host>/open/<route>?<bounded-query>
```

Fallback scheme:

```text
voxletra://<route>?<bounded-query>
```

Routes belong in `vxl-interfaces` and must be shared by Rust, Flutter, clients, and browser fallback pages.

Required behavior:

- support cold start and already-running delivery;
- validate the exact host, route, media/job/transcript identifiers, action, and bounded query parameters before crossing FFI;
- never put private recordings, transcript text, media contents, credentials, bearer tokens, or storage keys in URLs;
- use short-lived, one-time, audience-bound codes for imports, shares, and authentication;
- require confirmation before importing external media or exporting sensitive content; and
- test macOS, Windows, Linux, Android, and iOS app/universal links plus browser fallback.

Qt receives OS URL/file-open events, but the shared Rust parser validates and authorizes routes before application state changes.

## Product boundary

Both implementations should support semantic parity for media import/capture, transcription, editing, timelines, search, export, local processing, long-running jobs, progress recovery, secure storage, deep links, and per-platform media integration.

Shared schemas, clients, route fixtures, sample media, golden files, job-state models, and conformance tests must be versioned deliberately.

## Repository-local documentation

The live Flutter repository records the companion contract in [`COMPANION_DESKTOP.md`](https://github.com/voxletra/vxl-flutter/blob/main/COMPANION_DESKTOP.md), introduced through [PR #4](https://github.com/voxletra/vxl-flutter/pull/4).

Central toolkit assignments: [`rust-desktop-strategies.md`](https://github.com/ORESoftware/project-registry/blob/main/docs/rust-desktop-strategies.md).

## Project routing

- GitHub Project: [`voxletra-project` — Project 1](https://github.com/orgs/voxletra/projects/1)
- Linear project: `github.com/voxletra`
- Central registry: [`approved-private-registry`](private-registry://canonical/registry/desktop-applications.json)
- Portfolio rollout: [`DEN-2469`](https://linear.app/denman/issue/DEN-2469/roll-out-paired-rust-flutter-desktop-repositories-across-the-portfolio)

Repository creation, toolkit/FFI changes, deep-link changes, renames, transfers, archival, or platform-status changes must update this document, Linear, the central registry/strategy, and both companion repositories together.
