# STATE.md — current state

> Rewritten, not appended, as the LAST act of every session. See `HISTORY.md`
> for the narrative.

## In flight

Nothing in flight as of 2026-08-27.

## Blocked

Nothing blocked. Zero open PRs.

## Current release

Latest published: `v1.0.0` (verify directly — `gh api
repos/Ubiquex/ubx-schema-azure/releases/tags/v1.0.0`). 604 members. Does NOT
carry a real `min_binary_version` yet — predates that field (UBI-194). A
pinned `[providers.azure]` resolution falls back to `ubiquex`'s own bootstrap
table (`schema_format 3 -> ubx-provider-dynamic 1.0.0`), confirmed working
correctly and logging visibly. Deliberately not forced to regenerate —
recommendation on record (UBI-194) is this repo tracks a fast-moving upstream
API and is near-certain to bump for real content reasons within a cycle or
two of its own weekly `hash-watch.yml` cron anyway, picking up
`min_binary_version` for free at that point.

## Before touching anything

- Never self-merge here. See `CLAUDE.md`.
- `hash-watch.yml` now builds against a real, tagged `ubx-provider-dynamic`
  release (fixed UBI-194) — a regeneration today would carry a real
  `min_binary_version` if it runs.
- A first, cold pinned resolution of this provider takes ~54-56s (UBI-195,
  real, not a hang) — see `CLAUDE.md`.
