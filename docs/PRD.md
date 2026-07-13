# PRD — ContractFlow: AI Clause Review & Signature Workflow

**Author:** Francis Oluwatobi · **Status:** Draft v1.2 · **Last updated:** July 2026

## 1. Problem Statement

Real estate operators manage hundreds of leases, purchase agreements, and vendor contracts across fragmented tools — email for negotiation, shared drives for storage, a separate e-signature vendor for execution. The result is slow deal cycles, missed renewal deadlines, and no portfolio-level visibility into contractual risk.

From discovery interviews (see [DISCOVERY_PLAN.md](DISCOVERY_PLAN.md)), the three most-cited pain points were: contracts stall in review with no owner or SLA (11 of 14 interviewees), risky non-standard clauses are caught late or never (9 of 14), and leadership cannot answer "what is our total pipeline exposure?" without a manual spreadsheet exercise (12 of 14).

## 2. Goals & Non-Goals

**Goals**

1. Reduce average contract cycle time (draft → executed) by 30% within two quarters of launch.
2. Surface clause-level risk automatically at contract intake, before legal review begins.
3. Give portfolio managers a single dashboard for pipeline status, value, and signature bottlenecks.

**Non-Goals**

- Building a proprietary e-signature engine. We integrate with established providers (DocuSign, Adobe Sign) via API.
- Full CLM authoring/redlining. Negotiation stays in existing tools for v1; we ingest the near-final document.
- Legal advice. AI review flags deviations from templates and benchmarks; it does not render opinions.

## 3. Users & Jobs-to-be-Done

| Persona | Job-to-be-done | Primary surface |
|---|---|---|
| Portfolio / Asset Manager | "Show me every contract in flight, its value, and what's blocked." | Dashboard, KPIs |
| Transaction Coordinator | "Move this lease through review and signature without chasing people by email." | Workflow stepper, reminders |
| In-house Counsel | "Focus my time on the 10% of contracts with real risk." | AI clause review |
| VP Operations | "Prove our cycle times are improving and renewals aren't slipping." | Analytics |

## 4. Solution Overview

A four-stage lifecycle (Draft → Internal Review → Out for Signature → Executed) with:

- **AI clause review at intake** — model compares uploaded contract against the org's template library and market benchmarks; outputs risk tier (Low/Medium/High) and specific flags (e.g., uncapped CAM escalation, non-standard termination notice).
- **Signature orchestration** — envelope creation, signer sequencing, and status webhooks via e-signature provider APIs.
- **Stage SLAs and nudges** — configurable per-stage SLA; automated reminders when a contract exceeds it.
- **Portfolio analytics** — pipeline by stage, cycle time by contract type, executed-contract trend.

## 5. User Stories & Acceptance Criteria (v1)

**US-1: AI risk flag at intake**
*As in-house counsel, I want new contracts automatically scored for risk so I can prioritize my review queue.*
- AC1: On contract creation, a risk tier and ≥1 specific flag render within 10 seconds.
- AC2: Flags cite the clause category and a benchmark or template reference.
- AC3: A contract with no deviations shows an explicit "no material deviations" result (no silent pass).

**US-2: Signature status without leaving the app**
*As a transaction coordinator, I want live signer status so I know who to nudge.*
- AC1: Each signer shows signed/unsigned state, updated via provider webhook within 60 seconds of the event.
- AC2: A contract cannot be marked Executed until all required signers have signed.

**US-3: SLA breach visibility**
*As a portfolio manager, I want stalled contracts surfaced so nothing slips silently.*
- AC1: Days-in-stage is visible per contract; breaching contracts are flagged in the AI panel.
- AC2: Breach triggers one reminder to the stage owner; reminders are logged.

## 6. Success Metrics

North star: **median contract cycle time (days, draft → executed)**. Guardrails and inputs are defined in [METRICS_FRAMEWORK.md](METRICS_FRAMEWORK.md).

## 7. Rollout

Private beta with 3 design partners (one multifamily operator, one commercial landlord, one brokerage) → GA. Launch plan in [GTM_PLAN.md](GTM_PLAN.md).

## 8. Open Questions

1. Should AI review run on every version of a document or only at intake? (Cost vs. coverage trade-off.)
2. Which e-signature provider is the default integration for beta — driven by design partners' existing vendors?
3. Data residency requirements for EU-held portfolios — does v1 scope include EU hosting?
