# ContractFlow

**AI-assisted contract lifecycle & e-signature workflow management for real estate — a product management portfolio project.**

ContractFlow is an end-to-end product case study: a working prototype plus the full set of PM artifacts behind it — problem discovery, PRD, roadmap, metrics framework, go-to-market plan, and API design. It models how I approach product management for a SaaS platform in the digital transaction management / contract lifecycle management (CLM) space.

## 🖥️ Live prototype

Open **[`index.html`](index.html)** in any browser (or via GitHub Pages if enabled). No install, no backend — everything runs in-browser with simulated data.

The prototype demonstrates the core product loop:

1. **Contract intake** — create a contract; it enters a four-stage lifecycle (Draft → Internal Review → Out for Signature → Executed).
2. **AI clause review** — every contract gets an automatic risk tier (Low/Medium/High) with specific, benchmarked flags (e.g., uncapped CAM escalation, short due-diligence windows, auto-renewal traps).
3. **E-signature workflow** — signer-by-signer status with simulated signature events; contracts can't execute until all parties sign.
4. **Stage SLAs** — stalled contracts are flagged with suggested actions.
5. **Portfolio analytics** — pipeline by stage, cycle time by contract type, executed-contract trend.

*The AI review is deliberately a deterministic rule-based simulation — this is a product prototype for validating workflows and trust UX, not a production model.*

## 📄 Product artifacts

| Document | What it shows |
|---|---|
| [PRD](docs/PRD.md) | Problem statement, goals/non-goals, personas & JTBD, user stories with acceptance criteria |
| [Roadmap](docs/ROADMAP.md) | Outcome-based Now/Next/Later roadmap with RICE prioritization method |
| [Discovery Plan](docs/DISCOVERY_PLAN.md) | Interview guide, evidence standards, risky-assumption testing |
| [Metrics Framework](docs/METRICS_FRAMEWORK.md) | North star, metric tree, input/guardrail/commercial metrics |
| [GTM Plan](docs/GTM_PLAN.md) | Positioning, segmentation, phased launch, cross-functional ownership |
| [API Design](docs/API_DESIGN.md) | Platform/integration thinking: REST resources, provider abstraction, webhooks |

## Why this domain

Real estate transaction management sits at the intersection of high-value documents, multi-party workflows, and painful status opacity — a space where workflow software plus applied AI creates measurable value (cycle time, risk caught early, renewal deadlines never missed). The artifacts here work through that thesis end to end: from discovery evidence standards, to a north-star metric, to how the platform stays vendor-neutral on e-signature.

## Built with

Vanilla HTML/CSS/JavaScript + [Chart.js](https://www.chartjs.org/) — intentionally dependency-light so the prototype is a single reviewable file. AI-assisted development tooling was used throughout, mirroring modern AI-enabled product workflows.

---

*Francis Oluwatobi · oluwatobi.ou@gmail.com*
