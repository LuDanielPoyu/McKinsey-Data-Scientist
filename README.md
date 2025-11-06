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
| **P2. Search-Ad Analytics** | Decision cycles needed a decision-grade data layer to extract revenue-driving, model-optimizing insights from search-ad data | Decision-grade BigQuery SQL and Python analytics with consultants | Growth opportunities surfaced with insights; faster weekly decisions;  support weekly exec readouts | **BigQuery SQL** (CTEs, window/analytic functions), **Python** (pandas), **Machine Learning (prediction, clustering, classification)**, Looker Studio Dashboards |
| **P3. SQL Codebase Refactor & Data Ingestion and Extraction Pipelines** | Costly, slow queries; ad-hoc data pulls | Refactored entire SQL codebase and redefine KPI code; automated ingest and extract pipelines reused across workstreams | **Query runtime & cost ↓ ~40%**; pipelines power **~95%** of analyses | **BigQuery SQL**, **Python**, **Scheduled Jobs** |
| **P4. Keyword Product Relevance-Scoring API with Machine Learning Model for Search Engine Optimization (SEO)** | Slow A/B iteration on relevance ranking and low accuracy in relevance predictions limited gains| Automated Production Python API embedded with a trained machine learning model that scores keyword–product pairs and feeds the SEO ranking pipeline | **A/B cadence ↑ 1 → 3 tests/week** | **Python**, **PyTorch**, **REST API**, **pandas/NumPy**, **Experimentation Platform (A/B)** |
| **P5. Event-Driven Ad-Traffic Collector** | High latency and manual pulls on ad-traffic data | Automated event-driven collector in Python | **Retrieval latency ↓ ~88%** | **Python**, **Job Schedulers**, **HTTP/CSV ingestion** |
| **P6. Incentive Targeting Analytics for Mid/Long-Tail Vendors** | Low activation in ad-ssetting of target segment | Pattern analysis of ad-setting behaviors; targeting design with client's strategy team and consultant| **Activation rate ↑ ~13%** on first month of activation| **BigQuery SQL**, **Python**, **Statistical Analysis**, **Experiment Design** |

---

## Project Details

### P1 — Data Platform Reliability & Recovery
**Problem:** Manual checks for dashboard and data pipeline health created toil and slowed incident response.

**Solution:** Programmatic **health checks** and **alerting** backed by BigQuery-derived SLIs and SLOs, plus a **rapid-recovery runbook**.

**Data/ML-oriented highlights:**
- **SLIs/SLOs:** freshness lag, DAG latency, error rates; computed with **BigQuery SQL** window analytics and surfaced in **Looker Studio**.
- **Anomaly detection:** rolling-window thresholds (p90/p95) trigger alerts; noisy spikes damped with simple moving averages.
- **Operations:** runbooks with validation queries, rollback and forward procedures, and post-incident notes for continuous improvement.

**Impact:**
- **Manual monitoring ↓ ~8 hrs/week**; faster mean-time-to-detect and mean-time-to-recover.

```mermaid
flowchart LR
  subgraph Prod["Production"]
    P["Dashboards & Data Pipelines"]
  end

  P --> Q["Metrics via BigQuery SQL"]
  Q --> S["SLIs/SLOs"]
  S --> L["Looker Studio Dashboard"]
  S --> AR["Alerting Rules"]
  AR --> N["Notifications"]
  N --> RB["Rapid-Recovery Runbook"]
  RB --> V["Validation Queries"]
  RB --> RF["Rollback or Deploy Fix"]
  V --> DEC{"Resolved?"}
  RF --> DEC

  DEC -- Yes --> P
  DEC -- No --> ESC["Escalate / Triage"]
  ESC --> P

  DEC --> PI["Post-incident Notes & Improvements"]
  PI --> Q


```
---

### P2 — Search-Ad Analytics
**Problem:**  Decision cycles needed a decision-grade data layer and to extract revenue-driving, model-optimizing insights from search-ad data.

**Solution:** Built a decision-grade analytics layer in BigQuery and a Python, ML pipeline for feature engineering, cohort clustering, and supervised classification/regression, and time-series baselines to extract insights that drive revenue from search-ad logs and optimize e-commerce ad models; delivered reusable SQL (CTEs/windows) and notebooks that power weekly executive readouts.

**Data/ML-oriented highlights:**
- **Insight mining:** Partnered with consultants and client strategy teams to build **BigQuery SQL and Python/ML analyses** that surface e-commerce search-ad insights; translated raw logs into creative actions. For example: (1) Cohort clustering of vendors by adtype mix and spend elasticity. (2) Uplift cuts to spot segments responsive to keyword expansion. (3) Funnel drop-offs by device and time-of-day to guide bid scheduling. (4) Query-term cannibalization detection across campaigns.
- **Decision support:** Delivered reusable, **parameterized SQL (CTEs/windows) and versioned Python notebooks** that power weekly executive readouts in Looker Studio and BigQuery views; **automated refresh, DQ checks, and promo-window slicing** to keep KPIs consistent.
- **Metric modeling:** Built **clustering, classification, and regression models** with features for seasonality, device, channel, and query intent; evaluated via **cross-validation** and shipped lightweight **predictors** in tables/APIs (scikit-learn/XGBoost). For example: (1) Propensity scoring to rank vendors for incentive trials. (2) ROAS-lift regression to size bid increases. (3) Classifier to flag underperforming keywords for pause. (4) Time-series baselines to forecast daily spend/clicks.

**Impact:**
- Established a **decision-grade KPI layer** used across teams, supporting exec decisions with 4-5 analytic cases weekly.
- Cut **time-to-insight to same-day** via parameterized BigQuery views and auto-refreshed Looker studio dashboards.
- Produced **model-ready features and labels**, accelerating ranking and targeting experiments.

```mermaid
flowchart LR
  %% Inputs
  subgraph RAW["Raw inputs"]
    A["Search-ad logs"]
    B["Vendor & product metadata"]
    C["Promo/calendar · device/channel"]
  end

  %% BigQuery layer
  A & B & C --> D["BigQuery ETL"]
  D --> E["Decision-grade KPI layer"]

  %% ML / Analytics
  E --> F["Python/ML notebooks"]
  F --> G["Insights & models"]
  E --> Q["Feature & label tables"]

  %% BI / Readouts
  E --> H["Looker Studio dashboards"]
  G --> H
  H --> I["Weekly executive readouts"]
  I --> J["Decisions"]

  %% Quality & Refresh
  E --> M["Auto-refresh & DQ checks"]
  M --> H

```
---

### P3 — SQL Codebase Refactor & Data Ingestion and Extraction Pipelines
**Problem:** Slow, costly queries and repeated ad-hoc pulls hurt velocity and consistency.  

**Solution:** Refactored SQL and standardized KPI code; shipped **automated ingestion and extraction** with schema contracts.

**Data/ML-oriented highlights:**
- **Faster queries, lower cost:** Applied date **partitioning** and **clustering** on large tables, simplified heavy CTEs, and verified gains with **bytes-scanned** checks, resulting in faster runs and lower cost.
- **Parameterized codebase:** Converted duplicated SQL into **reusable templates and parameterized views**, moved constants to **reference tables/UDFs**, table value function (TVF), and added lightweight macros, achieving less copy-paste, fewer errors, and one query serving many slices.
- **Reproducible, model-ready outputs:** Deterministic scheduled jobs publish versioned, documented gold tables and views with schema contracts and lineage tracking. The datasets are query-ready for BI and analytics and supply feature and label tables for ML training and inference.

**Impact:**
- **Runtime & cost ↓ ~40%**; pipelines underpin **~95%** of analyses and dashboards.

```mermaid
flowchart LR
  %% Sources
  subgraph SRC["Sources"]
    S1["CSV/JSON exports"]
    S2["APIs"]
    S3["Ad-platform dumps"]
  end

  %% Ingestion & Staging
  SRC --> ING["Ingestion jobs"]
  ING --> STG["Staging tables"]

  %% Data Quality
  STG --> DQ["Data quality checks"]
  DQ --> TR["Transform layer"]

  %% Performance Engineering
  TR --> PERF["Performance tuning"]

  %% Gold Layer
  PERF --> GOLD["Gold tables and views"]

  %% Downstream Consumers
  GOLD --> BI["BI and analytics"]
  GOLD --> ML["ML outputs"]

  %% Observability / Catalog
  PERF --> MON["Perf monitor"]
  GOLD --> CAT["Data catalog"]

```
---

### P4 — Keyword Product Relevance-Scoring API with Machine Learning Model for Search Engine Optimization (SEO)
**Problem:** A/B cycles for SEO ranking were slow, and keyword–product relevance scores lacked accuracy, limiting measurable lift. 

**Solution:** A **Python REST API** that serves a trained **PyTorch** model to score keyword–product pairs for the SEO ranking pipeline.

**Data/ML-oriented highlights:**
- **Modeling:** Engineered features from query and product text (tokenization, n-grams, embeddings), behavioral signals (co-click/co-purchase, dwell time), and lexical–semantic similarity (BM25, cosine, edit distance). Trained a **PyTorch** classifier/regressor with class weighting and early stopping; tuned via stratified cross-validation. Evaluated with **AUC-PR** and ranking metrics (**NDCG@k**, MAP), ran ablations, and calibrated scores (Platt/Isotonic) for stable thresholds.
- **Serving:** Deployed a **FastAPI** microservice with a **TorchScript** model for low-latency inference. Requests are schema-validated and micro-batched; hot pairs are cached.
- **Experimentation:** Integrated with the **A/B platform** via feature flags and score thresholds, with predefined win criteria and guardrails (CTR, CVR, revenue, latency). Used staged rollout (shadow → 5% → 25% → 100%) with stop-loss triggers.

**Impact:**
- **A/B iteration ↑ from ~1 → 3 tests/week**, accelerating learning and ranking improvements.

```mermaid
flowchart LR
  %% Data & Features
  L["Search logs"]
  C["Catalog / product metadata"]
  U["User/session signals"]
  L & C & U --> FE["Feature engineering"]

  %% Offline Training & Eval
  FE --> TR["Training (PyTorch)"]
  TR --> EV["Offline evaluation"]
  EV --> MA["Model artifact"]

  %% Serving
  MA --> SVC["FastAPI inference service"]
  SVC --> RANK["SEO ranking pipeline"]

  %% Experimentation / Rollout
  RANK --> AB["A/B platform"]
  AB --> RAMP["Rollout plan"]
  RAMP --> MET["Online metrics"]

  %% Observability
  SVC --> OBS["Observability"]
  MET --> DEC["Go/No-Go and tuning"]
  EV  --> DEC

  %% Feedback Loop
  DEC --> LOOP["Retraining and threshold tuning"]
  LOOP --> FE

```
---

### P5 — Event-Driven Ad-Traffic Collector
**Problem:** Manual retrieval and laggy availability delayed downstream analytics and experiments.  

**Solution:** **Event-driven Python collector** with incremental fetch, retries, and idempotent writes to ready-to-query tables.

**Data/ML-oriented highlights:**
- **Automation & one-click UX:** Python collector automates incremental ingestion of traffic files (e.g., CSV/JSON) from shared folders or cloud storage, packaged as a **one-click desktop tool** so non-technical users can fetch data on demand or on a schedule.
- **Freshness & observability:** BigQuery computes end-to-end ingestion lag and file-to-table completeness; the tool logs run metadata and raises alerts when freshness or row-count thresholds are breached.
- **Reliability & data quality:** Checkpointing and idempotent writes prevent duplicates; schema and type checks and reconciliations catch anomalies; partitioned and clustered tables keep queries fast and produce **model-ready** inputs for KPIs and features.

**Impact:**
- **Retrieval latency ↓ ~88%**; fresher signals for KPIs, model training, and A/B tests.

```mermaid
flowchart LR
  S["Shared folders or cloud storage"] --> T["One-click desktop tool"]
  T --> F["Incremental fetch and checkpoint"]
  F --> V["Schema and type validation with reconciliation"]
  V --> W["Idempotent write"]
  W --> BQ["BigQuery staging"]
  BQ --> P["Partitioned and clustered tables"]
  P --> K["KPIs and dashboards"]
  P --> M["ML features and labels"]

  %% Observability
  F --> O["Freshness monitor"]
  O --> A["Alerts and run logs"]
```

---

### P6 — Incentive Targeting Analytics for Mid/Long-Tail Vendors
**Problem:** Low adoption of ad setup among mid/long-tail vendors, suppressing ad spend and revenue.

**Solution:** **Segmented vendors** by ad-setup behavior and partnered with consultants and the client’s strategy team to design **targeting rules** that raised ad-setup activation.

**Data/ML-oriented highlights:**
- **Segmentation:** Segment vendors with **K-means or hierarchical clustering** (optionally PCA) to surface mid/long-tail cohorts with low ad-setup adoption and high lift potential.
- **Incentive design and Prediction:** Use uplift and propensity models to forecast segment response, then choose the best incentive (ad credits/discounts, ready-made campaign bundles, or short-term managed setup by our team) via a lightweight policy simulator to maximize activation and ROI.
- **Tracking and Governance:** SQL rules and dashboards that ops can apply without code changes; monitoring for post-launch drift after targeting rules are applied.

**Impact:**
- **Activation rate ↑ ~13%** in targeted cohorts during first-month rollout.

```mermaid
flowchart LR
  A[Problem: Low ad-setup adoption in mid/long-tail vendors] --> B[Segment vendors]
  B --> C[Forecast response]
  C --> D[Simulate and choose incentives]
  D --> E[Design targeting rules]
  E --> F[Deploy via parameterized SQL and dashboards]
  F --> G[Monitor and govern]
  G --> H[Impact: Activation +13% in first month]

  I[Consultants and Client Strategy Team]
  I -. co-design .-> E
```

