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
| [shp_rqi](https://github.com/shalehaven/shp_rqi) | Rock Quality Index (RQI) training + scoring pipeline — trains per-cohort (Formation × Subbasin) models on the NoviLabs database and percentile-ranks every horizontal well by subsurface rock quality | Python |
| [shp_delaware](https://github.com/shalehaven/shp_delaware) | Delaware Basin landing-zone viewer — interactive HTML map of Wolfcamp / Bone Spring structure-contour and isopach surfaces from USGS OFR 2020-1126 | Python |
| [shp_powder](https://github.com/shalehaven/shp_powder) | Powder River Basin Upper Cretaceous viewer — interactive HTML map of structure and isopach surfaces from Fox Hills down to the Muddy Sandstone, built from WSGS OFR 2020-09 | Python |
| [.github](https://github.com/shalehaven/.github) | Organization profile and documentation | — |

---

## ShalehavenScripts Overview

Our primary codebase is a Python toolkit built to support internal investment analysis and operational workflows.

**Core Scripts**

- `main_los.py` — AFE data aggregation, JIB reconciliation, AFE-vs-actual reporting, well schedule rollup, and revenue tracking across fund years using internal database and company code mapping
- `main_model.py` — Offset well analysis and AFE modeling via Novi Labs API; reads AFE summaries and retrieves comparable well data for underwriting
- `main_prod.py` — Production data ETL pipeline; pulls operator production data, formats for ComboCurve upload, and compares against original and updated type curves

**Package Modules (`shalehavenscripts/`)**

- `los.py` — AFE / JIB / revenue combination, AFE-vs-actual reconciliation (Power BI Facts + Dimensions), well schedule rollup, folder parsing, and company code mapping utilities
- `novi.py` — Novi Labs API authentication and well data retrieval for offset analysis
- `afeleaks.py` — AFE Leaks API integration for well cost and production benchmarking
- `production.py` — Operator production data import, formatting, and ComboCurve-ready transformations
- `combocurve.py` — ComboCurve API integration for daily and monthly production data upserts and forecast retrieval

## Shalehaven Rock Quality Index (RQI) Model

Shalehaven's proprietary subsurface ranking engine. The pipeline trains a separate machine-learning model against a full U.S. horizontal-well database, then scores every eligible horizontal well using rock-only inputs with cohort medians substituted for completion, spacing, and landing-precision features. The output is a percentile-ranked view of subsurface rock quality used internally to screen acreage and benchmark offset wells before capital is deployed. **Private repository — internal use only; not publicly distributed.**

## Delaware Basin Viewer (`shp_delaware`)

A self-contained interactive HTML viewer of the 30 structure-contour and isopach plates published in **USGS Open-File Report 2020-1126** (Wolfcamp / Bone Spring, Delaware Basin), built to support landing-zone scoping for non-operated participation decisions.

**Features**

- Side-by-side structure (depth-to-top) and isopach (thickness) maps for every formation from Leonard Shale down to Wolfcamp D, switchable via dropdown
- Click any point to drop a marker and populate a depth/thickness table for **all** formations at that location
- Real-time tooltip showing **Section / Township / Range** (NMPM) on hover for any New Mexico cell
- Manual lookup form: enter a **Section + Township + Range** (NM) or **Lat/Lon**, plus an optional depth, and the viewer resolves the location, drops the marker, fills the formation table, and identifies which formation contains the entered depth
- Toggleable overlays: state borders, basin counties (NM + TX), county labels, and the NM 6-mile PLSS township grid
- Mouse-wheel zoom with linked subplots so the two maps stay in geographic sync
- Single self-contained HTML file with Plotly inlined — opens on any PC with no internet, CDN, or Python dependency

**Build pipeline (`delaware_basin/`)**

- `catalog.py` — figure → page → formation mapping for all 30 plates
- `georef.py` — per-page affine fit from PDF graticule labels to lat/lon
- `extract.py` — pulls every numeric contour label inside the map bbox and converts to control points
- `surfaces.py` — RBF (thin-plate-spline) interpolation onto a 160×160 grid, masked to the convex hull of control points
- `geo.py` — fetches and caches state/county GeoJSON; generates the NM PLSS 6-mile grid
- `viewer.py` — assembles the Plotly figure, lookup form, click/hover handlers, and PLSS hover-grid

**CLI**

```powershell
python build.py --copy-to default     # rebuilds and syncs to OneDrive
```

## Powder River Basin Viewer (`shp_powder`)

A self-contained interactive HTML viewer of the Upper Cretaceous structure and thickness maps published in **WSGS Open-File Report 2020-09** (Powder River Basin, Wyoming), built to support landing-zone scoping and offset evaluation across the PRB stack.

**Features**

- 15-entry dropdown spanning the Upper Cretaceous column from **Fox Hills Sandstone** (top + base) down through Teckla, Teapot, Red Bird-Parkman, Sussex, Shannon, Niobrara, Sage Breaks-Carlile, Turner-Wall Creek, Pool Creek, Greenhorn, Belle Fourche, Mowry / Mowry-Shell Creek, and the **Muddy Sandstone**
- Side-by-side structure (depth-below-surface) and thickness maps with paired structure / isopach surfaces wherever WSGS published both
- Optional overlay of the WSGS-published thickness contour lines pulled directly from the report's geodatabase
- RBF-interpolated surfaces built from WSGS well-tops, with explicit base-column or next-deeper-top fallback for thickness derivation
- City reference markers (Sheridan, Buffalo, Gillette, Casper, Douglas, Lusk, Sundance) and basin-extent grid scoped to the Wyoming PRB
- Single self-contained HTML file with Plotly inlined — opens on any PC with no internet, CDN, or Python dependency

**Build pipeline (`prb_viewer/`)**

- `catalog.py` — 28-figure → 15-dropdown mapping, formation specs (top / base / next-deeper-key), thickness overrides, and contour-layer registry for the .gdb
- `data_loader.py` — discovers and loads WSGS well-tops from .gdb / .csv / .xlsx (with optional AFELeaks fallback) plus the published contour-line layers
- `surfaces.py` — RBF (thin-plate-spline) interpolation onto a basin-extent grid, with contour-derived fallback for formations missing a base column
- `geo.py` — state / county GeoJSON fetch and Wyoming PRB clipping
- `reference.py` — extracts the WSGS reference plates from the source PDF for in-viewer comparison
- `pipeline.py` — orchestrates tops → surfaces → reference imagery → HTML
- `viewer.py` — assembles the Plotly figure, dropdown, click/hover handlers, and JSON-serialized surface payloads for client-side bilinear interpolation

**CLI**

```powershell
python build.py                       # produces prb_uppercret_viewer.html
python build.py --no-afeleaks -v      # WSGS-only sources, verbose logging
```

---

## Contact

**Dallas Office (HQ)**
15150 Preston Rd., Ste. 300 · Dallas, Texas 75248
📞 (214) 659-1062

**Denver Office**
5680 Greenwood Plaza Blvd · Greenwood Village, Colorado 80111
📞 (720) 685-6162

📧 [dev@shalehaven.com](mailto:dev@shalehaven.com) *(technical inquiries)*

🌐 [shalehaven.com](https://shalehaven.com) · [Investor Portal](http://shalehaven.cashflowportal.com)

---

## Connect

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Shalehaven%20Partners-0077B5?style=flat-square&logo=linkedin)](https://www.linkedin.com/company/shalehaven-partners-energy-asset-management-llc/)
[![Facebook](https://img.shields.io/badge/Facebook-Shalehaven%20Partners-1877F2?style=flat-square&logo=facebook)](https://www.facebook.com/people/Shalehaven-Partners/61565687158968/)
[![Instagram](https://img.shields.io/badge/Instagram-@shalehaven-E4405F?style=flat-square&logo=instagram)](https://www.instagram.com/shalehaven/)

---

*© 2026 Shalehaven Partners Energy & Asset Management, LLC. All rights reserved.*
