# Shalehaven Partners Energy & Asset Management

> **Private Oil & Gas Investment Company Focused on Deploying Non-Operated Capital**

[![Website](https://img.shields.io/badge/Website-shalehaven.com-blue?style=flat-square)](https://shalehaven.com)
[![Location](https://img.shields.io/badge/HQ-Dallas%2C%20Texas-green?style=flat-square)](#contact)
[![Language](https://img.shields.io/badge/Code-Python-yellow?style=flat-square)](https://github.com/shalehaven/ShalehavenScripts)

---

## About Us

Shalehaven Partners is a Dallas-based private oil and gas investment firm focused on deploying capital into **non-operated working interest** projects, both producing assets and non-producing AFE opportunities. Our goal is to leverage our robust balance sheet, our subject-matter expertise in energy, and our technology infrastructure to generate significant alpha for our LPs.

---

## Repositories

| Repository | Description | Language |
|---|---|---|
| [ShalehavenScripts](https://github.com/shalehaven/ShalehavenScripts) | Python toolkit for technical underwriting, economics, production and accounting ETL, spatial analysis, and operational reporting | Python |
| [rqi](https://github.com/shalehaven/rqi) | Rock Quality Index (RQI) training + scoring pipeline — trains per-cohort (Formation × Subbasin) models on the NoviLabs database and percentile-ranks every horizontal well by subsurface rock quality | Python |
| [shalehaven-platform](https://github.com/shalehaven/shalehaven-platform) | Shalehaven's AI platform — an MCP server that gives Claude secure access to our well, production, finance and deal data, behind Microsoft Entra sign-in, with a small admin console | TypeScript |
| [shp_pud](https://github.com/shalehaven/shp_pud) | PUD location generator — learns how each operator develops each landing zone from the Novi well database, fills undrilled space across eleven Lower 48 basins with laterals that follow that practice, back-tests against wells drilled since, and prices every location through the ShalehavenScripts economics model | Python |
| [shp_research](https://github.com/shalehaven/shp_research) | Well & operator benchmarking dashboard — Streamlit app over the weekly NoviLabs warehouse (DuckDB): type curves, completion-vs-performance, geology-normalized operator skill, well cards, and gun-barrel subsurface spacing | Python |
| [.github](https://github.com/shalehaven/.github) | Organization profile and documentation | — |

---

## ShalehavenScripts Overview

Our primary codebase is a Python toolkit supporting the full internal workflow from deal ingestion and technical underwriting through economics, production surveillance, hedging, accounting reconciliation, and reporting. Novi data lives in a weekly-refreshed SQL Server warehouse; ComboCurve provides type-curve, production, forecast, and economic-model integration. Reporting has moved off Power BI onto self-contained HTML dashboards, refreshed from SQL with one click.

**Core Scripts**

- `main_run.py` — Daily orchestrator for the capital formation, production, and LOS pipelines (plus a weekly hedge-volume pull), with independent subprocess execution, a run lock, and SQL-backed run logging
- `main_capital.py` — Publishes the investor tracker to SQL for capital formation reporting
- `main_prod.py` — Full production run: deal pipeline, ComboCurve push/pull, operator-file normalization, downtime capture, the seven-day production report, and SQL merges
- `main_los.py` — Well schedule, AFE, JIB, and revenue ETL; AFE-vs-actual reconciliation; and Lease Operating Statement reporting
- `main_model.py` — AFE underwriting pipeline: auction or workbook ingestion, ComboCurve type-curve or radius-peer cohorts (per-zone widening ladder), Novi-calibrated lateral-length scaling, economics HTML/PDF and email delivery, with geology and operator analysis built alongside
- `main_geology.py` — Builds a deal's regional geology report on its own, without running the model

**Package Modules (`shalehavenscripts/`)**

- `economics.py` — Per-well and portfolio economics (P10/P50/P90), ComboCurve assumption resolution, sensitivities, goal seek, and report generation
- `orri.py` — ORRI sell-down analysis: what an overriding royalty carved out of the lease NRI is worth to a buyer, and what selling it does to the retained working interest
- `lateral_scaling.py` / `normalization.py` — Novi-calibrated lateral-length scaling exponents per basin × formation × county, and a standalone lateral-normalization study
- `geology.py` — Regional geology deep-dive per landing zone, with statistically gated drivers of well performance
- `novi.py` — Novi warehouse refresh/read layer, offset cohort construction, subsurface and production analysis, interactive deal reports, and operator benchmarking
- `auction.py` — Auction-export ingestion and AFE Summary project scaffolding
- `afedatabase.py` — Registry of every modeled well's AFE for cost benchmarking
- `combocurve.py` — ComboCurve client for wells, type curves, production, forecasts (including auto-forecast), directional surveys, and economic models
- `production.py` — Operator production importers, ComboCurve-ready transformations, downtime capture, and the production dashboard
- `hedging.py` — Swaps-only hedge book per fund, built from final deal economics and actuals, priced on the strip
- `finance.py` — Loads every won deal's final economics into SQL for fund-level forecasts and returns
- `los.py` / `wellschedule.py` — AFE, JIB, revenue, AFE-vs-actual, LOS, and well-schedule processing
- `capitalformation.py` / `dealsheet.py` — Investor tracker and deal-pipeline ingestion and reporting
- `rigwatch.py` / `timelapse.py` — Weekly rig activity near won deals, and an animated basin-development time-lapse
- `pud_scores.py` — Review page for PUD locations priced through the model (see `shp_pud` below)
- `sql.py` / `gis.py` — SQL Server access (staged loads, atomic view swaps, run logging) and spatial layers for live QGIS use
- `tech.py` — Shared mail, branding, machine setup, and the `shalehaven://` link handler that lets report buttons run jobs
- `ui/` — HTML report builders and their client-side JavaScript

**HTML Reports**

- **Economics report** — one self-contained page per deal with live, in-browser recalculation: Summary (editable cash promote / carry, per-well grid), AFE Overview, Assumptions, Cash Flow / Zone, Rollup, Sensitivity, Goal Seek, Risk Profile, and **ORRI** (value of selling down the lease NRI as an overriding royalty, with a buyer-discount-rate control and a PDF export)
- **Operations dashboards** — production, deal pipeline, AFE vs actual, LOS, and hedge book, each refreshed from SQL by a button on the page
- **Admin page** — every pipeline and load as a one-click job with live status, last-run history, and a status window that streams progress
- **Model Runs page** — every AFE Summary in the current fund grouped by deal stage, with Run / Final buttons that launch the model directly

## Shalehaven Rock Quality Index (RQI) Model

Shalehaven's proprietary subsurface ranking engine. The pipeline trains a separate machine-learning model against a full U.S. horizontal-well database, then scores every eligible horizontal well using rock-only inputs with cohort medians substituted for completion, spacing, and landing-precision features. The output is a percentile-ranked view of subsurface rock quality used internally to screen acreage and benchmark offset wells before capital is deployed. **Private repository — internal use only; not publicly distributed.**

## PUD Location Generator (`shp_pud`)

Shalehaven's in-house undrilled-inventory engine, built to replace a paid inventory product with something we own and can calibrate. For each basin it learns how every operator actually develops every landing zone (in-zone spacing, stagger, lateral-length mix, 3-mile practice, wells per section) from the Novi horizontal-well database, then fills the undrilled space with laterals that follow that practice.

**Coverage** — eleven Lower 48 basins: Delaware, Midland, Williston, DJ, Eagle Ford, Haynesville, Marcellus, Utica, Anadarko, Uinta, and Powder River.

**How it works**

- **Resolve and learn** — generic formation tags are resolved to a landing zone, then spacing, stagger, and lateral rules are learned per operator × zone, falling back to operator, basin-zone, and basin levels
- **Place** — sticks hang off existing wells at the operator's spacing, cut on real drilling units (PLSS sections in New Mexico, RRC surveys in Texas), and trimmed to free space around every producing, DUC, and permitted lateral
- **Attribute** — each location carries its operator, lateral class, permit signal, parent wells, and any acreage-ownership gap along the stick (flagged as a leasing target, never a blocker)
- **Categorize** — `PUD` inside the proven play, or `EMERGING` for step-outs and stacked pay
- **Back-test** — every run is replayed as of an earlier date and scored on recall and precision against the wells drilled since
- **Publish** — results go to SQL Server with stable names across runs, a live multi-basin QGIS project, and a weekly refresh after each Novi load

**Scoring** — every location can be exported as an AFE Summary (capex fit from Shalehaven's own AFEs) and run unattended through the ShalehavenScripts economics model. Results are stored per location, with expected deal terms applied per basin, and reviewed on a scores dashboard.

**Private repository — internal use only.**

## Benchmarking Dashboard (`shp_research`)

A Streamlit research tool for benchmarking operators and wells by **basin / subbasin / formation**, built on the weekly NoviLabs *US Horizontals* extract. A DuckDB-over-Parquet warehouse is rebuilt from the raw weekly drop, giving sub-second analytical SQL over 29M+ monthly-production rows.

**Features**

- **Type curves** — normalized P10 / P50 / P90 production decline by operator or vintage, oil and gas tracked separately (per 1,000 ft lateral)
- **Completion vs. performance** — proppant / fluid / stage-spacing intensity against productivity, with an in-cohort regression fit
- **Geology-normalized operator skill** — a within-cohort regression of production on rock + completion separates operating skill from acreage quality, reporting the cross-validated R² so the ranking's trust is explicit
- **Well cards** — paste a set of API10s to get per-well summary cards compared to their cohort median
- **Gun barrel** — pick a reference well (map click or API10) and see a subsurface cross-section of nearby laterals, revealing bench stacking and spacing within the unit
- **Oil/gas-first metrics** — BOE is deliberately secondary; gas drives returns in the Haynesville/Marcellus and is near-worthless in the oily Delaware, so each stream is benchmarked on its own

**Private repository — internal use only.**

---

## Contact

**Dallas Office (HQ)**
15150 Preston Rd., Ste. 300 · Dallas, Texas 75248
📞 (214) 659-1062

**Denver Office**
5680 Greenwood Plaza Blvd · Greenwood Village, Colorado 80111
📞 (720) 685-6162

📧 [development@shalehaven.com](mailto:development@shalehaven.com) *(technical inquiries)*

🌐 [shalehaven.com](https://shalehaven.com)

---

*© 2026 Shalehaven Partners Energy & Asset Management, LLC. All rights reserved.*
