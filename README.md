# ubx-schema-azure

A real, frozen, versioned Azure provider schema snapshot -- the pinnable
distribution artifact `ubx-provider-dynamic` and `ubiquex` resolve a
single `[providers.azure]` entry against, with zero network calls at
schema resolution time (see `provider/acquireschema.go` in `ubiquex`,
and `internal/snapshot`'s own doc comment in `ubx-provider-dynamic`).
The resource/data-source split below is a real, internal discovery-time
detail -- one pin resolves all of it.

## What's here

Azure's own real published identity is a GROUP of 604 members -- 302
real, distinct Azure Resource Manager resource providers (one real
Swagger 2.0 spec per real product, e.g. `azure_network_virtualnetwork`,
`azure_sql_databases`), each fetched once and built into BOTH a
resource-mode member and a data-source-mode member from that one fetch:

- 302 resource-mode members (1,107 real resource types total -- UBI-181's
  own narrow create-verb allowlist, `internal/dsfilter`, admits 16 more
  than a literal "create"/"insert"-only check found, real, published ARM
  operations like `Databases_Create`/`FirewallRules_CreateOrUpdate` whose
  async response never structurally matched their own read schema).
- 302 data-source-mode members (1,614 real, unclaimed read-only
  operations total -- down from the pre-UBI-181 count: the same PR's own
  five-rule filter now excludes watch/operation-status/execution/
  computed/reference-duplication candidates that were never real data
  sources to begin with).

This is the first real group in this org whose own real specs needed
external `$ref` bundling before they could be published at all: Azure's
own real ARM specs split themselves across shared files by real
relative path (`../../../../../../common-types/resource-management/v5/
types.json#/definitions/ProxyResource`), which a frozen, network-free
snapshot can't resolve on reload without first making every one of
those refs genuinely local. `ubx-provider-dynamic`'s
`internal/openapi.Bundle` does this at generation time -- reference
bundling, not value inlining, since Azure's own real ref graph is
genuinely cyclic (`network/virtualNetwork.json`'s own real
`PublicIPAddress` reaches itself through its own real
`linkedPublicIPAddress` property).

- `manifest.json` -- the group's own real identity: `schema_format`,
  `provider`, one `version` for the WHOLE group, and which member names
  it bundles.
- `members/<name>.json` -- one real, complete, independently-diffable
  file per member, external refs already bundled into local
  `components` entries. Committed as separate files, not one combined
  blob, so a real version bump's own git diff shows exactly which of
  the 604 real members actually changed.
- `.github/workflows/hash-watch.yml` -- runs weekly (and on manual
  dispatch), regenerates every member from its own live Azure spec
  (bundling external refs again, fresh, every run) and opens a PR only
  when the group's own mechanically-derived version actually moves.
  Never auto-merges.
- `.github/workflows/publish.yml` -- manual-dispatch-only. Packs
  `manifest.json` and every `members/*.json` into one compressed
  archive (`snapshot.tar.gz`) and cuts a real GitHub Release tagged
  `v<version>` carrying exactly two assets: `snapshot.tar.gz` and
  `SHA256SUMS`.

## Consuming a real, published version

In `ubiquex`, one real pin resolves the whole group -- all 604 real
members are served together from the SAME launch, the SAME real
download:

```toml
[providers.azure]
source  = "ubiquex/azure"
version = "1.0.0"
```

`provider.AcquireSchema`'s own cache-by-source+version resolves ONE real
download and ONE extracted cache directory
(`~/.ubx/schemas/ubiquex/azure/1.0.0/`) -- the launched process merges
every real member of the group (`internal/snapshot.MergeOpenAPIGroup`)
into one served schema, `ResourceSchemas` and `DataSourceSchemas`
together.

## Versioning

One real, mechanically-derived semver number for the WHOLE group, not
one per member: the highest real change level found across every
member (a brand new resource type or a field that gained write access
bumps MINOR; a resource type or field that disappeared, or a field that
lost write access, bumps MAJOR; a pure description-text change bumps
PATCH), plus an unconditional MAJOR if a member the group used to
bundle is gone entirely. See `internal/snapshot/diff.go` and
`AssembleGroup` in `ubx-provider-dynamic` for the real rule.

`v1.0.0` is this group's real, first-ever snapshot.

<!-- README-GEN:BEGIN -->
**Real, current published version:** `v1.0.0`

## Links

- Docs: https://docs.ubiquex.io
- Internals (architecture and design): https://github.com/Ubiquex/ubiquex-internals
- Linear board: https://linear.app/ubiquex
<!-- README-GEN:END -->
