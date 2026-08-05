# voxletra organization handbook

> Shared operating defaults for repositories maintained under **voxletra**. Repository-local policy may strengthen these rules but should not silently weaken them.

## Mission

voxletra maintains voice, audio, language, and text-processing software. This `.github` repository is the canonical home for shared policy, reusable templates, community health files, and planning links.

## Repository contract

Each active repository must document purpose, ownership, maturity, supported languages and platforms, development and test commands, authoritative model and data formats, release and rollback procedures, compatibility policy, and GitHub Project/Linear links. Language and audio components should also document input assumptions, sampling and encoding, normalization, locale behavior, model provenance, confidence and error limits, accessibility, privacy, retention, and offline or degraded modes.

## Change workflow

1. Anchor work in an issue, Linear item, or documented maintenance objective.
2. Keep branches and pull requests focused.
3. Explain motivation, scope, data and user impact, validation, compatibility, migration, and rollback.
4. Test locale, accent, noise, empty, malformed, long-input, accessibility, privacy, and resource-pressure paths as relevant.
5. Resolve conflicts semantically by reconstructing both sides' intent.
6. Prefer squash merges for focused work unless commit structure materially improves auditability.

## Evidence, security, and documentation

Pull requests should include reproducible commands, licensed and sanitized fixtures, expected and observed results, quality metrics and limitations, negative-path coverage, documentation updates, and CI or local-equivalent evidence. Never commit credentials, private recordings, copyrighted datasets without authorization, production identities, or sensitive logs. Follow `SECURITY.md` for private reporting. Keep examples sanitized, model and dataset provenance explicit, links current, and important privacy, accessibility, compatibility, and operational decisions recorded.

## Planning ownership

GitHub owns code, reviews, checks, releases, and delivery evidence. Linear owns priority, dependencies, sequencing, and cross-project planning. The organization GitHub Project is the cross-repository execution view; see `PROJECTS.md` for routing details.

## Organization health

- [ ] Profiles, descriptions, topics, and READMEs are current.
- [ ] Community health files and reusable issue/PR guidance are present.
- [ ] Locale, encoding, model/dataset provenance, quality limits, privacy, and retention are documented.
- [ ] Required checks cover representative inputs, accessibility, compatibility, performance, and supply-chain risk.
- [ ] Stale repositories are archived or clearly marked.
- [ ] GitHub Project and Linear links resolve and reflect completed work.
