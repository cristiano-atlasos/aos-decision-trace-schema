<!-- smoke test -->
[![latest tag](https://img.shields.io/github/v/release/cristiano-atlasos/aos-decision-trace-schema?label=latest%20tag)](https://github.com/cristiano-atlasos/aos-decision-trace-schema/releases)
[![license: MIT](https://img.shields.io/badge/license-MIT-green.svg)](./LICENSE)
**Quick links:** [schema.json](./schema/schema.json) • [example.ndjson](./examples/example.ndjson) • [release notes](https://github.com/cristiano-atlasos/aos-decision-trace-schema/releases)

# A/OS DecisionTrace Schema (v0.1 · draft)
**Latest:** v0.1.0 (draft) — [release notes](https://github.com/cristiano-atlasos/aos-decision-trace-schema/releases/tag/v0.1.0)

**Spec & examples**
- JSON Schema: [`schema.json`](./schema.json)
- NDJSON example: [`examples/example.ndjson`](./examples/example.ndjson)

**Scope**
Minimal event schema for governed AI decisions (trace_id, episode_id, actor, attempted_action, result, policy_enforced, env, isolation_key, artifacts).
Portable today on Lovable/Supabase; cloud-agnostic tomorrow. SIEM/GRC exportable.

Minimal event schema for governed AI decisions: a single, append-only record that proves **what acted, under which policy, on what, when, and with what result** — exportable to SIEM/GRC.

**Why**
- Make every AI-driven operation auditable.
- Enable policy analytics, incident response, and compliance evidence.
- Portable across stacks (Lovable/Supabase today; any cloud tomorrow).

**TL;DR – Event fields (v0.1)**
- `trace_id` (uuid v4) – unique id of this record
- `episode_id` (string) – workflow/run id
- `decision_id` (string) – gate decision id
- `ts` (RFC3339) – timestamp (UTC)
- `actor` (object) – `{ type: "agent|human|system", id, role }`
- `policy_gate` (string) – gate or rule bundle name
- `action` (string) – attempted action (verb)
- `target` (string) – resource/entity key
- `inputs_redacted` (object) – minimal inputs, PII removed
- `result` (string) – `approved | hold | blocked`
- `latency_ms` (number) – eval latency
- `output_hash` (string) – sha256 of produced output (if any)
- `scope` (string) – GateScope / environment (e.g., `sandbox`, `prod`)
- `risk_level` (string) – `low|medium|high` (pre-policy scoring)
- `tenant_id` (string, optional) – multi-tenant isolation key
- `evidence_uris` (array<string>, optional) – artifacts (NDJSON/OTel)
- `schema_version` (string) – `0.1.0`

**Example**
```json
{
"trace_id": "6d7c1a8e-2b7b-4c18-9a2b-0f8a2a9f2b30",
"episode_id": "ap-invoice-2025-11-05-00123",
"decision_id": "gate-approve-000045",
"ts": "2025-11-05T12:15:41Z",
"actor": { "type": "agent", "id": "ap-bot-v1", "role": "operator" },
"policy_gate": "finance-approve",
"action": "post_invoice",
"target": "invoice:INV-009874",
"inputs_redacted": { "amount": 5420.13, "currency": "USD", "vendor_id": "V-1342" },
"result": "approved",
"latency_ms": 187,
"output_hash": "sha256:8d7f…c1a",
"scope": "sandbox",
"risk_level": "medium",
"tenant_id": "demo-tenant-a",
"evidence_uris": ["otel://traces/abc123", "s3://evidence/packs/p2025-11-05.ndjson"],
"schema_version": "0.1.0"
}
