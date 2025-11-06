# Contributing

Thanks for your help improving these A/OS resources.

## Scope
This org hosts:
- **aos-decision-trace-schema** — minimal event schema for governed AI decisions.
- **aos-evidence-export-packs** — NDJSON & OpenTelemetry mappings + starter SIEM queries.
- **aos-policygates-checklist** — checklist to approve/hold/block AI actions.

## How to propose changes
1. Open an Issue (Bug or Feature) using the templates.
2. Fork the repo and create a branch: `feat/...` or `fix/...`.
3. Make small, atomic commits.
- Conventional style is welcome: `feat:`, `fix:`, `docs:`, `chore:`.
4. Submit a PR referencing the Issue.

## Versioning & releases
- We use **v0.1.x** while iterating. Changes should be backward-compatible when possible.
- Maintainers publish releases with tags (e.g., `v0.1.1`) and notes. Releases are immutable.

## Testing / validation
- **Schema** repo: validate JSON/NDJSON against `schema.json` (CI runs on PRs).
- **Evidence packs**: validate JSON syntax; run lint on OTel examples if applicable.

## Security
Please **do not** file public issues for vulnerabilities. Follow [`SECURITY.md`](SECURITY.md).

## Code of Conduct
By participating, you agree to follow our [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md).
