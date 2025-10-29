# McKinsey-Data-Scientist

**Role:** Data Scientist (Full-Time: 40 hrs/wk)  
**When:** Jan. 2025 – Jan. 2026 *(expected)* · **Location:** Taipei, Taiwan  

> **Disclaimer:** This portfolio uses sanitized descriptions and **synthetic examples only**.  
> No proprietary code, data, screenshots, internal IDs, or client configurations are included.

---

## Projects at a Glance

| Project | Problem | What I Built | Result | Stack |
|---|---|---|---|---|
| **P1. Data Platform Reliability & Recovery** | Manual checks and slow incident response around dashboards and data pipelines | Health checks, alerting, and rapid-recovery runbook | **Manual monitoring ↓ ~8 hrs/week** | **Python**, **BigQuery SQL** (freshness/latency SLIs), **Monitoring/Alerting**, **Operational Runbooks**, Looker Studio Dashboard |
| **P2. Search-Ad KPI Analytics** | Decision cycles needed a decision-grade data layer and to extract revenue-driving, model-optimizing insights from search-ad data | Decision-grade BigQuery SQL and Python analytics with consultants | Growth opportunities surfaced; faster weekly decisions;  support weekly exec readouts | **BigQuery SQL** (CTEs, window/analytic functions), **Python** (pandas), **Machine Learning (prediction, clustering, classification)**, **Looker Studio Dashboards** |
| **P3. SQL Codebase Refactor & Data Ingestion and Extraction Pipelines** | Costly, slow queries; ad-hoc data pulls | Refactored entire SQL codebase and redefine KPI code; automated ingest and extract pipelines reused across workstreams | **Query runtime & cost ↓ ~40%**; pipelines power **~95%** of analyses | **BigQuery SQL**, **Python**, **Scheduled Jobs** |
| **P4. Relevance-Scoring API with Machine Learning Model for Search Engine Optimization (SEO: Keyword ↔ Product)** | Slow A/B iteration on relevance ranking and low accuracy in relevance predictions limited gains| Automated Production Python API that scores keyword–product pairs and feeds the SEO ranking pipeline | **A/B cadence ↑ 1 → 3 tests/week** | **Python**, **PyTorch**, **REST API**, **pandas/NumPy**, **Experimentation Platform (A/B)** |
| **P5. Event-Driven Ad-Traffic Collector** | High latency and manual pulls on ad-traffic data | Automated event-driven collector in Python | **Retrieval latency ↓ ~88%** | **Python**, **Job Schedulers**, **HTTP/CSV ingestion** |
| **P6. Incentive Targeting Analytics for Mid and Long-Tail Vendors** | Low activation in ad-ssetting of target segment | Pattern analysis of ad-setting behaviors; targeting design with client's strategy team and consultant| **Activation rate ↑ ~13%** on first month of activation| **BigQuery SQL**, **Python**, **Statistical Analysis**, **Experiment Design** |

---

## Project Details

### P1 — Data Platform Reliability & Recovery
**Problem.** Manual checks for dashboard/pipeline health created toil and slowed incident response.  
**Solution.** Introduced programmatic **health checks**, **alerting**, and a **rapid-recovery runbook** for on-call.

**Highlights**
- Proactive monitors on SLIs/SLOs (freshness, latency, failure rates).
- Alert routing with clear ownership and escalation path.
- Recovery playbooks with verifications and post-incident notes.

**Impact**
- **Manual monitoring reduced ~8 hrs/week** while improving mean-time-to-recover.

---

### P2 — Search-Ad KPI Analytics for Executive Readouts
**Problem.** KPI definitions were fragmented; weekly decisions stalled on manual queries.  
**Solution.** Co-developed **decision-grade BigQuery SQL** with consultants; standardized KPI logic for **weekly executive readouts**.

**Highlights**
- Unified KPI layer (spend, clicks, CTR/CPC/ROAS, cohort views).
- Reusable parameterized queries for weekly/MTD/YTD cuts.
- Clear audit trail of metric definitions for stakeholders.

**Impact**
- Consistent metrics and **faster weekly decisions**; surfaced concrete **e-commerce ad revenue opportunities**.

---

### P3 — SQL Refactor & Ingestion/Extraction Pipelines
**Problem.** Queries were costly/slow; repeated ad-hoc pulls.  
**Solution.** Refactored the SQL codebase; shipped automated **ingestion/extraction pipelines** reused across analyses and dashboards.

**Highlights**
- Partitioning, clustering, and predicate pushdown.
- Common CTE library and tested macros.
- Scheduled ingest/extract with schema contracts.

**Impact**
- **Runtime & cost ↓ ~40%**; pipelines underpin **~95%** of analyses/dashboards.

---

### P4 — Relevance-Scoring API (SEO: Keyword ↔ Product)
**Problem.** Ranking tweaks were bottlenecked; A/B tests ran ~1/week.  
**Solution.** A **Python REST API** that scores keyword–product pairs for SEO relevance and feeds the ranking pipeline.

**Highlights**
- Deterministic scoring with unit tests and simple offline evals.
- Lightweight schema; backfills and shadow deploys for safety.
- Easy integration with A/B platform.

**Impact**
- **A/B iteration ↑ from ~1 → 3 tests/week**, accelerating learning cycles.

---

### P5 — Event-Driven Ad-Traffic Collector
**Problem.** Ad-traffic retrieval was slow and manual, delaying downstream analytics.  
**Solution.** **Event-driven Python collector** with incremental fetch, retries, and idempotent writes.

**Highlights**
- Checkpointing to avoid duplicates; backoff/retry for flaky sources.
- Incremental loads that land ready-to-query.
- Simple ops dashboard for freshness and lag.

**Impact**
- **Retrieval latency ↓ ~88%**; fresher inputs for KPIs and experiments.

---

### P6 — Incentive Targeting for Mid/Long-Tail Vendors
**Problem.** Activation lagged in mid/long-tail vendor segments.  
**Solution.** Analyzed **ad-setting patterns** and partnered with the client strategy team to design **incentive targeting**.

**Highlights**
- Feature cuts by vendor cohort, spend tier, and adtype mix.
- Hypothesis-driven segmentation; simple uplift checks.
- Rollout plan aligned with client ops cadence.

**Impact**
- **Activation rate ↑ ~13%** in targeted cohorts.

---

## Impact Highlights (Summary)
- Ops & reliability: **–8 hrs/week** manual monitoring; faster incident recovery.  
- Analytics foundation: Unified **BigQuery** KPI layer enabling **weekly exec decisions**.  
- Efficiency: SQL refactor + pipelines → **–40%** runtime/cost; coverage of **~95%** analyses.  
- Experiment velocity: Relevance API → **1 → 3** A/B tests per week.  
- Data freshness: Event-driven collector → **–88%** latency.  
- Growth: Incentive targeting → **+13%** activation in focus segments.

---

## Ops & Experimentation Loops (Simplified)

```mermaid
flowchart LR
  A[Prod Pipelines] --> B[Health Checks & Alerts]
  B --> C[On-Call Runbook]
  C --> D[Rapid Recovery]
  D --> A
```
