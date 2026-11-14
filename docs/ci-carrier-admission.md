# Cross-organization CI-carrier admission

This policy applies whenever a source repository cannot run its own GitHub Actions and a separate authorized private repository supplies runner minutes. It does **not** authorize copying private source to public repositories or bypassing source-organization review.

## Source identity and isolation

1. Identify the source repository, source PR, immutable commit SHA and the exact paths/bytes under test.
2. Mirror only the approved source Git blobs into a **private** test repository on a temporary branch. The receiving `GITHUB_TOKEN` must never require access to the source organization; do not copy secrets or tokens across organizations.
3. Verify each mirrored blob's Git SHA against its source Git SHA, fail on omission, change or unexpected extra paths. Preserve a manifest of the exact path → source blob pair.
4. Use SHA-pinned checkout and verify the executing `git rev-parse HEAD` equals the expected carrier PR head. Synthetic merge-ref execution is not source-head proof.
5. Record all actual job steps, exit codes, commands, test counts and the runner OS/toolchain. A workflow with no executed steps is **not** a passing test.

## Claim scope and merge hold

- A carrier check proves only the recorded tests on the recorded source bytes. Partial source snapshots do not prove full compilation, execution or multi-backend parity.
- Include explicit `NOT_EXECUTED` markers for untested targets. Pending, skipped, cancelled and admission-only jobs are never interpreted as pass.
- Carrier PRs are **temporary and non-promoting**; never merge a carrier PR to a production branch simply because its tests are green.
- Promotion must happen through the source repository PR, independent review, required native checks (or documented equivalence), exact-head verification and no unresolved review thread.
- Preserve temporary branches until evidence is captured and accepted. Cleanup requires explicit authorization and must not delete unsaved local work.

## Receipt example

```text
SOURCE_REPOSITORY=org/repo
SOURCE_PR=123
SOURCE_HEAD=<40 lowercase hex characters>
CARRIER_REPOSITORY=private-org/private-carrier
CARRIER_PR=456
CARRIER_HEAD=<40 lowercase hex characters>
SOURCE_BLOBS_VERIFIED=<integer>
TESTS_EXECUTED=<integer>
TESTS_FAILED=0
TARGETS_NOT_EXECUTED=<explicit list>
PROMOTION=NOT_AUTHORIZED
```

Do not paste private repo inventories, credentials, customer data or operational topology into a public carrier report.
