# API & Integration Design Sketch — ContractFlow

Platform thinking for the "Later" roadmap horizon: ContractFlow should be integratable, not a silo. This sketch defines the core resources and the e-signature provider abstraction.

## Core resources (REST, JSON)

```
GET    /v1/contracts                 # list, filterable by status/type/risk
POST   /v1/contracts                 # intake; triggers AI review
GET    /v1/contracts/{id}
PATCH  /v1/contracts/{id}/stage      # advance lifecycle stage (validated transitions only)
GET    /v1/contracts/{id}/analysis   # AI clause review result
POST   /v1/contracts/{id}/envelope   # create signature envelope
GET    /v1/analytics/cycle-time      # aggregated, org-scoped
```

## Example: AI analysis payload

```json
{
  "contract_id": "c_8f2a",
  "risk_tier": "High",
  "flags": [
    {
      "category": "escalation_clause",
      "severity": "high",
      "summary": "CAM escalation uncapped; portfolio standard is 3-5% annual cap.",
      "clause_ref": "Section 6.2",
      "benchmark_source": "org_template:commercial_lease_v4"
    }
  ],
  "model_version": "clause-review-2026-06",
  "reviewed_at": "2026-07-10T14:32:00Z"
}
```

## E-signature provider abstraction

All providers implement the same internal interface so product features never depend on a specific vendor:

```
create_envelope(contract, signers[], sequence) -> envelope_id
get_status(envelope_id) -> {signer: status}
webhook: envelope.signed | envelope.completed | envelope.declined
```

v1 adapter: DocuSign. v2: Adobe Sign + generic webhook adapter for long-tail vendors.

## Webhooks (outbound)

Orgs can subscribe to `contract.stage_changed`, `analysis.completed`, `sla.breached`, `envelope.completed` — the events property management systems (MRI, Yardi) need to keep records in sync.

## Design principles

1. Lifecycle transitions are validated server-side; the API never allows Draft → Executed.
2. AI analysis is versioned and immutable per run — auditability over convenience.
3. Org-scoped API keys with per-resource scopes; no cross-org data access, ever.
