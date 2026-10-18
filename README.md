# lang

Handl-the-language as data (ADR-0044 made literal). This repo holds
`handl-kit-data-canonical` — the canonical `Language` assembled purely
from YAML fragments (`crates/handl-kit-data-canonical/data/*.yaml`,
including the kit manifests under `data/kits/`) — plus the
`handl-packages/` entries it pins (`query`, `command`, `event`) and the
`examples/handl/` fixtures its tests evaluate.

It was extracted from the `handl-lang/host` workspace in ADR-0128
Phase 11. Platform crates are git dependencies on
`handl-lang/host`; for local development the workspace root's
`[patch]` table resolves them from a sibling `../host` checkout.
Before the remote is published, make the git source resolve locally
with `url.insteadOf` + `CARGO_NET_GIT_FETCH_WITH_CLI=true` (see the
comment in `Cargo.toml`).
