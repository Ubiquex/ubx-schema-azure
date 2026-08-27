# HISTORY.md — narrative archive

> Consulted only when a session needs to know why a decision was made, not on
> every open. For what's current, read `STATE.md` instead.

This file is new as of UBI-183 (2026-08-27). Real history predating it lives
in `ubiquex`'s own `HISTORY.md` (search `UBI-182`, `UBI-193`, `UBI-194`,
`UBI-195`) and in this repo's own real `git log`/merged-PR history, which is
authoritative for what actually shipped and when.

## Real, known decisions worth carrying forward

**UBI-193: this repo could not exist until Azure's own cyclic ref graph was
handled.** Azure's real specs split themselves across shared files by
relative path, and — confirmed live, not assumed — that ref graph is
genuinely CYCLIC, not just deep. `ubx-provider-dynamic`'s own
`internal/openapi.Bundle` rewrites every external ref into a real, local,
network-free component (reference bundling, not value inlining) before a
snapshot is ever frozen. This repo is the first real group in this org
published only after that fix landed.

**First real published version was `1.0.0`, not `0.1.0`** — same correction
as every other schema repo in this org; see `ubx-schema-kubernetes`'s own
`HISTORY.md` for the full account.

**UBI-195: real, live RPC-layer load-time cost, filed not fixed.** A pinned
resolution of this provider takes ~54-56s wall time to the first RPC
response, zero network. Three separate live instruments isolated the cost to
the `GetProviderSchema` gRPC call itself (~41s of the total), NOT
parsing/translation/merging (~11s) — an earlier hypothesis, corrected in the
ticket itself once measured properly. Nobody has picked this up yet.

**Bootstrap fallback, not yet retired (2026-08-27).** This repo's own
`v1.0.0` predates `min_binary_version` (UBI-194). Deliberately not forced to
regenerate; see `STATE.md`.
