# Shalehaven Partners Energy & Asset Management

> **Private Oil & Gas Investment Company Focused on Deploying Non-Operated Capital**

[![Website](https://img.shields.io/badge/Website-shalehaven.com-blue?style=flat-square)](https://shalehaven.com)
[![Location](https://img.shields.io/badge/HQ-Dallas%2C%20Texas-green?style=flat-square)](#contact)
[![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)](#repositories)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)](#repositories)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](#repositories)
[![SQL](https://img.shields.io/badge/SQL%20Server-CC2927?style=flat-square&logo=microsoftsqlserver&logoColor=white)](#repositories)
[![PowerShell](https://img.shields.io/badge/PowerShell-5391FE?style=flat-square&logo=powershell&logoColor=white)](#repositories)
[![HTML/CSS](https://img.shields.io/badge/HTML%2FCSS-E34F26?style=flat-square&logo=html5&logoColor=white)](#repositories)

---

## About Us

Shalehaven Partners is a Dallas-based private oil and gas investment firm focused on deploying capital into **non-operated working interest** projects, both producing assets and non-producing AFE opportunities. Our goal is to leverage our robust balance sheet, our subject-matter expertise in energy, and our technology infrastructure to generate significant alpha for our LPs.

---

## Repositories

| Repository | Description | Language |
|---|---|---|
| [ShalehavenScripts](https://github.com/shalehaven/ShalehavenScripts) | Shalehaven's Internal Analysis and Economics Platform | Python |
| [rqi](https://github.com/shalehaven/rqi) | Shalehaven's Internal Rock Quality Model | Python |
| [shalehaven-platform](https://github.com/shalehaven/shalehaven-platform) | Shalehaven's Internal AI Platform | TypeScript |
| [shp_pud](https://github.com/shalehaven/shp_pud) | Shalehaven's Internal PUD Development Model | Python |
| [shp_research](https://github.com/shalehaven/shp_research) | Shalehaven's Internal Research Platform | Python |
| [.github](https://github.com/shalehaven/.github) | Organization profile and documentation | — |

---

## ShalehavenScripts Overview

Our primary codebase: a Python toolkit covering the full internal workflow, from deal ingestion and technical underwriting through economics, production, hedging, accounting, and reporting. Built on a SQL Server well-data warehouse and ComboCurve.

- **Underwriting** — AFE ingestion, type-curve and offset-peer cohorts, lateral-length scaling, geology and operator analysis
- **Economics** — P10/P50/P90 per-well and portfolio economics with sensitivities, goal seek, risk profile, and ORRI sell-down valuation
- **Operations** — daily production, LOS, AFE-vs-actual, hedge book, and deal-pipeline pipelines
- **Reporting** — self-contained HTML dashboards with live recalculation and one-click refresh, plus an admin page that runs every job

**Private repository — internal use only.**

## Shalehaven Rock Quality Index (RQI) Model

Shalehaven's proprietary subsurface ranking engine. It trains machine-learning models per formation and sub-basin on rock-only inputs, then percentile-ranks every horizontal well by rock quality.

- **Screening** — rank acreage on rock quality before capital is deployed
- **Benchmarking** — separate rock quality from completion and operator effects on offset wells

**Private repository — internal use only.**

## PUD Location Generator (`shp_pud`)

Shalehaven's in-house undrilled-inventory model. For each basin it learns how every operator develops every landing zone (spacing, stagger, lateral length, wells per section), then fills the undrilled space with locations that follow that practice.

- **Coverage** — eleven Lower 48 basins, placed on real drilling units
- **Calibrated** — every run is back-tested against the wells actually drilled since
- **Priced** — every location runs through the ShalehavenScripts economics model

**Private repository — internal use only.**

## Benchmarking Dashboard (`shp_research`)

A Streamlit research tool for benchmarking operators and wells by basin, sub-basin, and formation, built on a weekly-refreshed horizontal-well warehouse.

- **Type curves** — normalized P10 / P50 / P90 decline by operator or vintage, oil and gas tracked separately
- **Operator skill** — completion and performance analysis that separates operating skill from acreage quality
- **Spacing** — well cards and gun-barrel cross-sections of nearby laterals

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
