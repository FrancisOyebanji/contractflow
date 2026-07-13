# Metrics Framework — ContractFlow

## North Star

**Median contract cycle time (days, Draft → Executed)** — the single number that captures the value promise. Segmented by contract type and org size; reported as a rolling 90-day median to smooth deal lumpiness.

## Metric tree

```
Median cycle time
├── Time in Draft            → intake completeness, template usage rate
├── Time in Internal Review  → AI flag act-on rate, approval routing hit rate
├── Time in Signature        → signer reminder effectiveness, envelope error rate
└── Rework loops             → % contracts returned to a prior stage
```

## Input metrics (leading indicators)

| Metric | Definition | Target (2 qtrs post-GA) |
|---|---|---|
| AI flag act-on rate | % of High/Medium flags where the user edits, escalates, or annotates within 7 days | ≥ 55% |
| SLA breach rate | % of contracts exceeding stage SLA | ≤ 15% |
| Signature completion within 72h | % of envelopes fully signed within 72h of send | ≥ 70% |
| Weekly active orgs | Orgs with ≥1 contract state change per week | ≥ 80% of paying orgs |

## Guardrail metrics

| Metric | Why it guards | Threshold |
|---|---|---|
| AI false-positive rate (user marks flag "not useful") | Trust erosion kills act-on rate | ≤ 20% |
| Executed contracts later amended within 30 days | Speed shouldn't create rework | No regression vs. baseline |
| Support tickets per active org | Workflow complexity creep | No regression vs. baseline |

## Commercial metrics

Net revenue retention (target ≥ 110%), analytics add-on attach rate (≥ 25% by H1 2027), and logo retention (≥ 92%). Product reviews these monthly with Sales and CS; a metric moving against target for two consecutive months triggers a roadmap re-prioritization discussion, not just a dashboard annotation.

## Instrumentation notes

Every lifecycle transition, AI flag render, and flag interaction emits a structured event (`org_id`, `contract_id`, `event_type`, `stage`, `timestamp`). Dashboards are stakeholder-specific: exec (north star + commercial), squad (input metrics + funnel), CS (per-org health).
