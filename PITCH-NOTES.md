# OpenNorth — Pitch Notes (working document)

Internal companion to the website. Everything here is the reasoning behind what the site says — positioning, the cost model with its assumptions, an honest audit of claims, and what still needs real-world validation. Last updated July 2026.

---

## 1. Positioning

**Canonical one-liner (kept, verbatim):**
> Private open-weight AI over your company data, with every answer traceable to source.

It's accurate and holds up, but it's *insider* language — "open-weight" means nothing to a non-technical reviewer. So the site leads with the plain-English translation and keeps the one-liner as the formal subtitle:

- **Hero (plain English):** "Private AI for businesses whose data can't go to ChatGPT."
- **Supporting line:** runs on infrastructure you control · answers only from your documents · every answer cites its source.

Why this framing won:
- It names the customer by their *constraint*, not their industry — the fastest possible self-qualification. A reviewer instantly knows who this is for.
- "Can't go to ChatGPT" is honest about the competition: for everyone else, ChatGPT is fine (the site says so explicitly, which buys credibility for everything else on the page).
- The three product pillars map to the three buying triggers found in research: confidentiality (NDAs/PIPEDA/PHIPA), grounding in private documents, and auditability (PHIPA now requires electronic audit logs — traceability is a compliance feature, not a slogan).

**Deliberate de-emphasis:** the old site led with "fixed cost, unlimited usage, $0/query." Research says that's the weakest honest claim — at light usage, APIs are cheaper than any private deployment once GPU + upkeep are counted. Cost *predictability* stays as a supporting benefit; cost *savings* is claimed only for sustained heavy usage. Selling privacy people can verify beats selling savings they can disprove.

---

## 2. The wedge (recommendation)

**First market: mining supply & services (MSS) firms in Greater Sudbury.**

Why this beats the alternatives:

| Candidate | For | Against | Verdict |
|---|---|---|---|
| **Mining supply & services** | 300+ firms locally (~14k jobs, ~$4B exports — Invest Sudbury); mid-size and privately held (fast decisions); document-heavy (safety, ISO, manuals, tenders); NDA-bound to majors → real privacy constraint; founder has mining-software credibility (LoopX, Vale app); reachable via MineConnect/NORCAT | Not all firms are tech-forward; some data is paper | **Primary wedge** |
| Clinics / community health | PHIPA makes private AI + audit logs genuinely compelling | Risk-averse, slow, high stakes for a first reference; "AI + health data" invites scrutiny a solo founder doesn't need yet | Year 2, after references exist |
| Municipalities | Founder worked at City of Greater Sudbury; real records/privacy needs | Procurement cycles are quarters-to-years; RFP processes favor incumbents | Year 2, via pilot programs |
| Law / accounting firms | Privilege = hard privacy constraint; docs are the business | Small firms up North; conservative buyers; bar-association AI guidance still settling | Opportunistic, not primary |

**First POC (the free one):** a read-only, citation-first document assistant for one MSS firm — safety procedures, equipment manuals, past tenders, HR/ISO docs. Deployed in their cloud account or on one machine on their premises. 2–4 weeks.

**What it must prove (the only three questions that matter):**
1. Staff get correct, source-cited answers from their own documents in seconds (vs. hunting or asking the veteran).
2. Zero data leaves their environment — verifiable, not promised.
3. People actually use it during a two-week live test (usage logs answer this objectively).

**Deliverable that converts:** the written evaluation report — accuracy on a customer-chosen question set, *misses included*. It doubles as the honest basis for the production quote, and as reference material for the next prospect even if this one doesn't convert.

**Solo-founder feasibility check:** ingestion + retrieval + chat UI + citations + basic auth on an open stack (Postgres/pgvector, vLLM or Ollama, an 8–32B open model) is squarely within one experienced engineer's 2–4 week window. It's the green-column offer by design — no fine-tuning, no live ERP integrations, no SLA.

---

## 3. Cost estimate model (the reasoning behind the site's numbers)

All CAD, July 2026. Method: public GPU-rental and hardware pricing for the infrastructure lines; published RAG-implementation benchmarks sanity-check the services lines; support line sized from the "10–20 hrs/month upkeep" figure that recurs across self-hosting TCO analyses. Sources are linked on the site's Sources section.

### Assumptions
- Exchange ~1.37 CAD/USD; cloud GPU = 24/7 on-demand in the customer's own account (business-hours-only roughly halves it).
- "Small" = one team, one use case, docs already digital, read-only Q&A. "Mid" = multi-department, RBAC, several connectors, governed answers. "Large" = high concurrency, compliance program, possible air-gap.
- Model licenses: $0 (Apache/MIT). Vector DB/database: $0 (Postgres + pgvector / Qdrant OSS). The money goes to compute and engineering time, which is the honest shape of this market.

### Per-tier logic
| Line | Small (5–50) | Mid (50–500) | Large (500+) | Basis |
|---|---|---|---|---|
| Setup & implementation (one-time) | $8k–$25k | $25k–$80k | $80k–$250k+ | US agency benchmarks run US$15k–40k basic / 40k–120k production / 120k–300k+ enterprise; solo founder prices below agency but in the same universe |
| Hardware if on-prem (one-time) | $5k–$12k (one 24–32GB GPU box or Mac-class unified memory) | $15k–$40k (1–2 × 48–80GB, L40S/A100 class) | $60k–$300k+ (multi-GPU node) | Retail GPU/workstation pricing, 2026 |
| Cloud GPU if cloud (monthly) | $400–$1,600 (L4/A10G/L40S class) | $1,500–$5,000 | $5,000–$25,000+ | L40S ≈ US$1–1.6/hr, A100 80GB ≈ US$1–1.5/hr (neoclouds; hyperscalers 2–4×) |
| Support & maintenance (monthly) | $500–$1,500 | $1,500–$4,000 | $4,000–$10,000+ | 10–20 hrs/mo upkeep at sustainable rates; includes model updates, re-indexing, monitoring, backups |
| Fine-tuning (one-time, optional) | skip | $5k–$20k | $20k–$75k | LoRA-scale, only past a data threshold |

### One-time vs. ongoing (the sentence version)
You pay once to build it (implementation, and hardware if on-prem), and monthly to keep it alive (GPU rental if cloud, plus support). Nothing is per-token or per-seat.

### Break-even honesty (keep saying this out loud)
- Light usage + non-sensitive data → **APIs/ChatGPT are cheaper. Full stop.** The site says this verbatim; it's the single biggest credibility purchase on the page.
- Private AI wins on: confidentiality (can't use public AI at any price), auditability, offline capability, cost *predictability* — and raw cost only at sustained heavy usage (analyses put the crossover anywhere from ~0.5M to 30M tokens/day depending on model class and assumptions; too assumption-sensitive to promise, so the site doesn't).

### What makes quotes move
Cheap: one team · digital docs · read-only · customer's cloud · business hours. Expensive: scanned paper & messy permissions · finance-grade structured-data accuracy · 24/7 SLAs · air-gap · write-access integrations · formal compliance evidence.

---

## 4. Claims audit — strong vs. weak

**Strong (verified, cited on the site):**
- Open-weight models lead/match on independent leaderboards (GLM-5.2 top open model; Qwen3 family Apache 2.0) — multiple 2026 sources.
- One 24GB GPU serves a ~30B-class model — consistent across 2026 hardware guides.
- Sudbury cluster: 300+ MSS firms, ~14k jobs, ~$4B exports — Invest Sudbury.
- PHIPA requires electronic audit logs on PHI systems — 2026 compliance coverage.
- GPU price ranges — multiple public price sheets.
- Founder delivery history (Flosonics warehouse + AI assistant, Vale offline app, OreAcle offline POC) — real, and OreAcle is publicly linked.

**Defensible but softer (framed with hedges on the site):**
- Implementation cost ranges — grounded in published benchmarks, but a solo founder's actual costs will vary; framed as "planning ranges, not quotes."
- "~40% reporting overhead reduction" at Flosonics — real experience but internal/unauditable; kept, attributed to past employment only.
- "2–4 weeks to POC" — realistic for the scoped green-column offer, but the first live customer will find friction; the scope box exists to protect this claim.

**Weak / removed from the old site:**
- "$0/query" and "$8.2B market by 2026" hero stats — replaced (marginal-cost framing was misleading; market-size stats are decoration for a services wedge).
- "Same answer company-wide" as a headline promise — demoted to the amber "with engineering effort" column ("governed answers"), which is where it truthfully lives.
- Any implication of traction, customers, or team — replaced with explicit "pre-revenue, building in the open."

---

## 5. Validation checklist (real world, in order)

1. **Name check (do this first):** "Open North" / opennorth.ca is an existing Canadian nonprofit (open data / civic tech). Check trademark and confusion risk before printing anything — CIPO search + a call with an IP clinic. Have a backup name ready in case.
2. **10 discovery conversations** with Sudbury MSS firms (via MineConnect, NORCAT, PDAC contacts): does the "can't use public AI" constraint actually bite? Which documents hurt most? Would they test a free POC? Target: 3 warm POC candidates.
3. **Pick 1 POC** against the fit criteria on the site — resist taking a bad-fit freebie; the evaluation report is the real product of this phase.
4. **Validate the support price** ($500–$1,500/mo small tier) against what an SMB actually tolerates — this line is the recurring-revenue heart of the model.
5. **Measure real POC economics:** actual hours spent (setup + support) vs. the model in §3; correct the site's ranges with lived numbers.
6. **Test the Copilot objection live** — it's the most likely competitive response in any M365 shop; the FAQ answer needs field-testing.
7. **Insurance & contracts:** E&O/cyber liability quote, POC agreement + NDA template, before the first customer data lands on a machine you configured.
8. **Grant/support scan:** NOHFC, FedNor, and regional innovation programs (NORCAT) for services-to-product runway — Northern Ontario location is an asset here.

## 6. Known risks (say them before a judge does)

- **Platform absorption:** Microsoft/Google push governed AI down-market; mitigation: on-prem/air-gap + audit depth + local hands-on service is the un-absorbable residue.
- **Model churn:** open-weight leaders change quarterly; mitigation: the model is a swappable component — churn is an upgrade path, not a rebuild.
- **Services trap:** custom deployments don't scale; mitigation: same stack every time, productize the repeatable 80% after ~3 deployments.
- **Solo capacity:** one founder caps concurrent projects at ~2; mitigation: scope discipline (green column only), contractor bench for growth, honesty on the Large tier.
