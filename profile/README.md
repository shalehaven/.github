# Shalehaven Partners Energy & Asset Management

> **Private Oil & Gas Investment Company Focused on Deploying Non-Operated Capital**

[![Website](https://img.shields.io/badge/Website-shalehaven.com-blue?style=flat-square)](https://shalehaven.com)
[![Location](https://img.shields.io/badge/HQ-Dallas%2C%20Texas-green?style=flat-square)](#contact)
[![Language](https://img.shields.io/badge/Code-Python-yellow?style=flat-square)](https://github.com/shalehaven/ShalehavenScripts)

---

## About Us

Shalehaven Partners is a Dallas-based private oil and gas investment firm specializing in **tax-advantaged, non-operated working interests** in proven shale basins across the United States. Our mission is to build long-term relationships with investor partners by delivering significant annual tax savings and above-market returns through disciplined capital deployment in drill-ready, economically proven projects.

We exclusively invest in areas where economic wells have already been drilled and produced successfully — ensuring investor capital is diversified across a portfolio of proven, de-risked wells.

---

## Investment Strategy

- **Non-Operated Capital Deployment** — We participate as a working interest owner, not an operator, allowing for broad diversification across multiple projects and operators.
- **Tax-Advantaged Structure** — Investors benefit from Intangible Drilling Cost (IDC) deductions. Shalehaven delivered a **90.7% deduction for 2024 & 2025 investors**, significantly reducing tax liability.
- **Proven Basin Focus** — Capital is placed only in basins with demonstrated production history and established economics.
- **Low Fee Structure** — Designed to maximize net returns; among the lowest fee structures in the non-operated space.
- **Passive Income** — While investors are living their lives, the portfolio generates oil and gas revenue — true mailbox money.

---

## Repositories

| Repository | Description | Language |
|---|---|---|
| [ShalehavenScripts](https://github.com/shalehaven/ShalehavenScripts) | Python toolkit for shale energy investment analysis — geospatial screening, production modeling, and economic evaluation | Python |
| [.github](https://github.com/shalehaven/.github) | Organization profile and documentation | — |

---

## ShalehavenScripts Overview

Our primary codebase is a Python toolkit built to support internal investment analysis and operational workflows.

**Core Scripts**

- `main_los.py` — AFE data aggregation, JIB reconciliation, and revenue tracking across fund years using internal database and company code mapping
- `main_model.py` — Offset well analysis and AFE modeling via Novi Labs API; reads AFE summaries and retrieves comparable well data for underwriting
- `main_prod.py` — Production data ETL pipeline; pulls operator production data, formats for ComboCurve upload, and compares against original and updated type curves

**Package Modules (`shalehavenscripts/`)**

- `los.py` — AFE data combination, folder parsing, and company code mapping utilities
- `novi.py` — Novi Labs API authentication and well data retrieval for offset analysis
- `afeleaks.py` — AFE Leaks API integration for well cost and production benchmarking
- `production.py` — Operator production data import, formatting, and ComboCurve-ready transformations
- `combocurve.py` — ComboCurve API integration for daily and monthly production data upserts and forecast retrieval

---

## Contact

**Dallas Office (HQ)**
15150 Preston Rd., Ste. 300 · Dallas, Texas 75248
📞 (214) 659-1062

**Denver Office**
5680 Greenwood Plaza Blvd · Greenwood Village, Colorado 80111
📞 (720) 685-6162

📧 [development@shalehaven.com](mailto:dev@shalehaven.com) *(technical inquiries)*

🌐 [shalehaven.com](https://shalehaven.com) · [Investor Portal](http://shalehaven.cashflowportal.com)

---

## Connect

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Shalehaven%20Partners-0077B5?style=flat-square&logo=linkedin)](https://www.linkedin.com/company/shalehaven-partners-energy-asset-management-llc/)
[![Facebook](https://img.shields.io/badge/Facebook-Shalehaven%20Partners-1877F2?style=flat-square&logo=facebook)](https://www.facebook.com/people/Shalehaven-Partners/61565687158968/)
[![Instagram](https://img.shields.io/badge/Instagram-@shalehaven-E4405F?style=flat-square&logo=instagram)](https://www.instagram.com/shalehaven/)

---

*© 2026 Shalehaven Partners Energy & Asset Management, LLC. All rights reserved.*
