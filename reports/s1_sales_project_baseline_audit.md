# S1 — Sales Project Baseline Audit (Interview Preparation Archive)

**Status:** INTERNAL DOCUMENT. Not part of, and never added to, the public
repository `sales-performance-business-analytics`. Lives only in this
private repository, `sales-performance-business-analytics-private`.

**Audit date:** 2026-08-29

---

## 1. Project Identity

- **Project title:** Sales Performance & Business Analytics
- **Nature:** Portfolio Data Analyst / Business Analyst project built on a synthetic, disclosed dataset
- **Public repository owner:** naresh-naik

## 2. Public Repository Identity

| Property | Value |
|---|---|
| Repository | `sales-performance-business-analytics` |
| Owner | naresh-naik |
| Visibility | PUBLIC |
| Default branch | `main` |
| Baseline HEAD SHA (this audit) | `6d68c35b8517609ca5a1021061c453eeed156c01` |
| origin URL | `https://github.com/naresh-naik/sales-performance-business-analytics.git` |
| Working-tree status at audit time | Clean, up to date with `origin/main` |
| Commit history at audit time | 4 commits: `3745b15` (initial release), `3a5936e` (docs: record Phase 10 publication results), `2655d18` (remove reports/ from published repo), `6d68c35` (docs: remove dead reports/ links from README) |

This document was produced entirely by inspecting the repository as it
actually exists at the above HEAD — no fact below was assumed from memory
without verification.

## 3. Dataset Facts

| Property | Value | Verification method |
|---|---|---|
| Source file | `data/clean/sales_data_clean.csv` | Direct inspection |
| Row count | 9,985 | Fresh pandas read at this audit |
| Column count | 12 | Fresh pandas read |
| Columns | `Order_ID`, `Order_Date`, `Product`, `Category`, `Quantity`, `Unit_Price`, `Revenue`, `Country`, `Cost`, `Profit`, `Customer_ID`, `Customer_Segment` | Fresh pandas read |
| Data types | Order_ID int64, Order_Date datetime64, Product/Category/Country/Customer_ID/Customer_Segment object(str), Quantity int64, Unit_Price/Revenue/Cost/Profit float64 | Fresh pandas `.dtypes` |
| Categorical fields | Product (5 values), Category (2 values), Country (4 values), Customer_Segment (2 values) | Fresh pandas read |
| Date field | Order_Date, range 2024-01-01 to 2025-12-31 | Fresh pandas read |
| Missing values | 0 | Fresh pandas `.isna().sum()` |
| Duplicate Order_ID | 0 | Fresh pandas `.duplicated().sum()` |
| Provenance | **Synthetic/generated** — produced by `data/generate_data.py` with a fixed random seed (42), documented explicitly in `data/README.md`, `data/data_dictionary.md`, and the README's first paragraph ("The dataset is synthetically generated for portfolio and analytical demonstration purposes and does not represent real company data.") | Direct inspection of `data/generate_data.py` and all documentation; not inferred |
| Raw (pre-cleaning) dataset | `data/raw/sales_data_raw.csv`, 10,020 rows, contains 6 categories of intentionally injected data-quality issues, documented in `data/README.md` | Direct inspection |

**No provenance was invented.** The dataset is explicitly and consistently
documented as synthetic everywhere it is described, including in the
published README's opening lines.

## 4. Business Problem

As stated in the public README: the project models a fictional
multi-country electronics retailer (Laptop, Phone, Tablet, Monitor,
Keyboard; Germany, Austria, France, Netherlands) and answers: overall
sales performance trend, which products/markets drive revenue vs. profit,
how Consumer vs. Business customer segments compare, which product-market
combinations are strongest/weakest, whether revenue leadership matches
profitability leadership, and what a management stakeholder should
investigate further given the data's limitations.

## 5. Analytical Workflow

Verified as actually implemented (not assumed):

1. **Data generation** (`data/generate_data.py`) → **Data cleaning**
   (`data/clean_data.py`) → **Clean dataset** (`data/clean/sales_data_clean.csv`,
   single source of truth for every downstream layer).
2. **Python/pandas EDA & KPI analysis** (`notebooks/sales_analysis.ipynb`).
3. **SQL business analysis** (`sql/*.sql` against a SQLite database, `sql/sales_analysis.db`).
4. **Excel formula-driven business report** (`excel/sales_business_analysis.xlsx`).
5. **Power BI implementation specification** (`powerbi/*.md` — specification only, not an executed dashboard).
6. **Business insights & recommendations** (previously `reports/business_insights.md`, now internal-only — see Section 19).

No technology beyond this list is present or claimed anywhere in the
repository (no machine learning, no forecasting, no web application, no
cloud deployment).

## 6. Python Capability (Verified)

Inspected `notebooks/sales_analysis.ipynb` directly at this audit:

- **63 total cells: 33 code, 30 markdown.**
- **0 errors** present in the notebook's saved cell outputs.
- Imports actually used: `pandas`, `numpy`, `matplotlib.pyplot`, `matplotlib.ticker` — **no other library is imported anywhere in the notebook** (no scikit-learn, no statsmodels, no ML library of any kind).
- Demonstrated: data-quality re-validation, feature engineering (Year/Month/Quarter/Year-Month, row-level profit margin), descriptive statistics, distribution/outlier (IQR) analysis, correlation analysis, a Core+Supporting KPI framework, product/category/market/customer/time/profitability analysis, a Product×Country cross-dimensional heatmap, evidence-based findings and recommendations.
- Reproducibility: independently re-executed from a clean kernel during prior project work with 0 errors and results matching the canonical figures exactly (not re-executed again during this specific audit, to avoid unnecessary environment changes, but the saved 0-error output state was directly inspected).

## 7. SQL Capability (Verified)

Inspected all 10 `sql/*.sql` files directly at this audit:

| Technique | Present? | Files |
|---|---|---|
| Basic SELECT/WHERE/ORDER BY/LIMIT/DISTINCT | Yes | `02_basic_queries.sql` |
| KPI aggregation (SUM/COUNT/AVG) | Yes | `03_kpi_analysis.sql` and others |
| Product/Category analysis | Yes | `04_product_analysis.sql` |
| Market analysis | Yes | `05_market_analysis.sql` |
| Customer analysis | Yes | `06_customer_analysis.sql` |
| Time analysis | Yes | `07_time_analysis.sql` |
| Profitability analysis | Yes | `08_profitability_analysis.sql` |
| `CASE` expressions | Yes | `01_data_setup.sql`, `06`, `08`, `09`, `10` |
| CTEs (`WITH ... AS`) | Yes | `06_customer_analysis.sql`, `08_profitability_analysis.sql` |
| Subqueries | Yes | `04`, `05`, `06`, `09` (correlated and non-correlated) |
| `JOIN` | Yes (one deliberate, justified JOIN — fact table to a derived per-product benchmark table; no artificial dimension tables were created) | `09_advanced_analysis.sql` |
| Window functions (`RANK`, `DENSE_RANK`, `ROW_NUMBER`, `SUM() OVER`) | Yes | `04`, `05`, `06`, `07`, `08`, `09` |

No technique is claimed that is not actually present in the SQL files.

## 8. Excel Capability (Verified)

Directly opened `excel/sales_business_analysis.xlsx` with openpyxl at this audit:

- **12 sheets:** README, Raw_Data, Data_Validation, Customer_Detail, KPI_Summary, Product_Analysis, Market_Analysis, Customer_Analysis, Time_Analysis, Profitability, Product_x_Country, Business_Summary.
- **Raw_Data** is an exact import of the clean CSV as an Excel Table (`SalesData`), 9,985 data rows.
- Sample-checked formula cell (`Product_Analysis!B3`): `=SUMIF(SalesData[Product],$A3,SalesData[Revenue])` — confirmed live-formula-driven, not a hardcoded value.
- Conditional formatting confirmed present (2 rules on `Product_Analysis`, 2 on `Product_x_Country`).
- Charts confirmed present (2 on Product_Analysis, 1 on Market_Analysis, 1 on Time_Analysis — 4 total).
- Product × Country matrix confirmed present as its own dedicated sheet.
- Business_Summary confirmed to use dynamic `INDEX/MATCH(MAX(...))` lookups rather than fixed-row references (a specific bug found and fixed during prior project work; re-verified still correct at this audit).

## 9. Power BI Status (Critical — Verified Honest Wording)

**Confirmed: no `.pbix` file exists anywhere in this project** (verified via a fresh `find . -iname "*.pbix"` at this audit — zero results). The project contains a **Power BI implementation specification** only: `powerbi/README.md`, `powerbi/data_model.md`, `powerbi/power_query.md`, `powerbi/dax_measures.md`, `powerbi/dashboard_specification.md`, `powerbi/validation.md`.

Both `README.md` and `powerbi/README.md` state, verbatim, that Power BI Desktop was unavailable in the development environment (macOS) and that PBIX assembly requires Power BI Desktop. This wording is confirmed present and unchanged.

**Approved wording for CV/interview use:** "Designed a Power BI dashboard specification (data model, DAX measures, 4-page layout)" or "Prepared a complete Power BI implementation specification, including DAX measures and dashboard design." **Never** "built," "developed," "created an interactive," or "deployed" a Power BI dashboard — no such artifact exists to support that phrasing.

## 10. Verified KPI Inventory

Every figure below was independently recomputed from `data/clean/sales_data_clean.csv` at this audit (not copied from prior reports) and matched exactly, with **zero discrepancies**:

| Metric | Value |
|---|---|
| Total Revenue | €7,765,475.38 |
| Total Profit | €2,733,273.35 |
| Profit Margin | 35.20% |
| Total Orders | 9,985 |
| Total Quantity | 20,391 |
| Average Order Value | €777.71 |
| Top revenue & profit product | Laptop (€3,913,418.03 revenue, €1,268,139.49 profit) |
| Laptop revenue contribution | 50.40% |
| Lowest-margin product | Laptop (32.40%) |
| Highest-margin product | Keyboard (47.34%) |
| Top revenue & profit country | Germany (€2,334,832.14 revenue, €826,074.21 profit) |
| Highest-AOV country | Netherlands (€786.22) |
| Strongest Product×Country combination | Laptop × Germany (€1,180,603.33) |
| Unique customers | 850 |
| Repeat-customer rate | 99.88% (849/850) — **see mandatory caveat, Section 12** |
| 2024 vs. 2025 Revenue | €3,811,573.14 → €3,953,902.24 |
| Revenue YoY | +3.73% |
| Orders YoY | +2.86% |
| Monthly revenue coefficient of variation | 9.41% (no material seasonality — see Section 12) |

**No discrepancy was found between the previously published figures and this audit's independent recomputation.** No STOP condition was triggered.

## 11. Business Findings

Each finding below follows FINDING → EVIDENCE → BUSINESS INTERPRETATION → LIMITATION, re-verified against the data at this audit.

**Finding 1 — Laptop dominates revenue and profit but has the thinnest margin.**
Evidence: Laptop = 50.40% of revenue, top profit contributor, 32.40% margin (lowest of 5 products).
Interpretation: revenue and profit scale are concentrated in one product line; that same product line is the least margin-efficient.
Limitation: no cost-driver breakdown exists beyond aggregate Cost/Unit_Price/Quantity — the *reason* for the lower margin cannot be attributed to any specific business cause from this data alone.

**Finding 2 — Product order counts are balanced; revenue concentration is price-driven, not popularity-driven.**
Evidence: order counts across all 5 products fall in a narrow 1,917–2,070 range despite revenue ranging from 2.35% to 50.40% of total.
Interpretation: differences in revenue share reflect price tier, not how often each product is ordered.
Limitation: none beyond general synthetic-data caveats.

**Finding 3 — Germany leads revenue and profit; Netherlands leads order value.**
Evidence: Germany = top revenue (€2,334,832.14) and top profit (€826,074.21); Netherlands = top AOV (€786.22).
Interpretation: revenue leadership and order-value leadership are held by different markets in this dataset.
Limitation: **"Germany leads revenue" is valid; "Germany leads revenue because customers there prefer laptops" is NOT valid** — the dataset contains no demographic, economic, or preference data to support a causal claim.

**Finding 4 — The strongest revenue combination and strongest margin combination are different Product×Country pairs.**
Evidence: Laptop × Germany = strongest revenue (€1,180,603.33); Keyboard × Germany = strongest margin (per prior cross-tool validation, ~47.47%).
Interpretation: a single "best" product-market combination does not exist — it depends on whether revenue or margin is prioritized.
Limitation: does not establish that any specific commercial action (e.g., promotion) would change these figures.

**Finding 5 — Consumer contributes more total revenue than Business, explained by customer count, not order value.**
Evidence: Consumer and Business have nearly identical AOV and margin; the revenue split tracks the customer-count split.
Interpretation: segment revenue differences here are a volume effect, not a per-transaction value effect.
Limitation: no marketing, acquisition-channel, or customer-motivation data exists to explain *why* segment sizes differ.

**Finding 6 — Revenue rank equals profit rank at both product and country level, but margin rank differs from both.**
Evidence: independently re-verified at this audit.
Interpretation: the largest revenue generators are also the largest absolute profit generators (mechanically, at scale), but the *most efficient* product/market (by margin) is a different one entirely.
Limitation: none beyond the general synthetic-data caveat.

**Finding 7 — No material seasonality; modest YoY growth within the dataset's single 24-month window.**
Evidence: 9.41% monthly revenue coefficient of variation, no repeating pattern; +3.73% revenue / +2.86% orders / +3.81% profit 2024→2025.
Interpretation: performance within the generated window is descriptively stable and mildly increasing.
Limitation: **this is not evidence of a real growth trend** — it describes the synthetic data as generated, within its one designed window, and should not be extrapolated.

**Finding 8 — Repeat-customer rate is 99.88%.**
Evidence: 849 of 850 customers placed more than one order.
Interpretation: **this is a data-generation artifact, not a business result.** See Section 12 for the mandatory caveat framing.

## 12. Data Caveats (Mandatory, Preserved Verbatim in Substance)

### Repeat-customer caveat
The ~99.88% repeat-customer rate is a **data-generation artifact**: Phase 2 generated only 850 fixed `Customer_ID` values and reused them across 9,985 orders (~11.75 orders/customer by construction). **Approved framing:** "the dataset shows a 99.88% repeat-order rate, which is disclosed as an artifact of the synthetic customer-generation design, not measured real-world retention." **Do NOT say:** "99.88% customer retention," "excellent customer loyalty," "strong repeat purchasing," or "high customer lifetime value" — none of these are supported.

### Seasonality caveat
No material seasonality was found (9.41% monthly coefficient of variation, no repeating pattern). **Approved framing:** "no material seasonality was identified in this dataset." **Do NOT say:** the project "proved" seasonal demand, holiday effects, or monthly seasonality — it did not, and could not, given how the dates were generated (uniform random sampling).

### Correlation caveat
Revenue–Cost (r≈0.996) and Revenue–Profit (r≈0.982) correlations are very high but **substantially mechanical**, since Cost and Profit are formula-derived from Revenue by the generation logic (`Revenue = Quantity × Unit_Price`, `Profit = Revenue − Cost`). Not an independently discovered business relationship.

### External-variables caveat
No competitor, marketing, economic, demographic, inventory, returns, discount, or true-acquisition-date data exists anywhere in this project. No causal claim about any of these should ever be made in interview answers.

## 13. Analyst Skill Map

Only skills genuinely supported by direct repository evidence (each cross-checked at this audit):

| Skill | Evidence |
|---|---|
| Data Cleaning | `data/clean_data.py` — documented deduplication, missing-value, invalid-quantity, category-typo, formula-consistency fixes; 6 issue types, before/after counts verifiable |
| Exploratory Data Analysis | Notebook Sections 7 (descriptive stats, distributions, outliers, correlation) |
| KPI Analysis | Notebook Section 8; SQL `03_kpi_analysis.sql`; Excel `KPI_Summary` sheet — same 8 Core KPIs, cross-validated |
| Business Analysis | Product/market/customer/time/profitability sections across all three executed tools |
| SQL | 10 files, CASE/CTE/subquery/JOIN/window functions all genuinely present (Section 7) |
| Excel | Formula-driven 12-sheet workbook, verified live formulas not hardcoded values (Section 8) |
| Data Visualization | Notebook (9 charts), Excel (4 charts + conditional formatting) |
| Profitability Analysis | Section 8/13 of notebook; `08_profitability_analysis.sql`; Excel `Profitability` sheet |
| Customer Analysis | Repeat/one-time customer counts, segment comparison, all three tools |
| Market Analysis | Country-level revenue/profit/AOV/margin, all three tools |
| Product Analysis | Product-level revenue/profit/margin/contribution, all three tools |
| Trend Analysis | Yearly/quarterly/monthly breakdowns, notebook + SQL |
| Query Design | 10 well-organized, purpose-labeled SQL files (not syntax-demo queries) |
| Window Functions | `RANK`, `DENSE_RANK`, `ROW_NUMBER`, `SUM() OVER` genuinely used, verified this audit |
| CTEs | `WITH` clauses genuinely used, verified this audit |
| Scenario/Recommendation Thinking | 8 evidence-linked recommendations (previously in `business_insights.md`, now internal — Section 19) |
| Data Validation | 16-check Phase 2 validation pipeline; independent re-validation in notebook, SQL, and Excel (`Data_Validation` sheet) |
| Cross-tool Reconciliation | 18-metric cross-check across Python/SQL/Excel, documented and re-verified (Section 14) |
| Documentation | Per-tool README files, data dictionary, phase reports (kept internal — Section 19) |
| Reproducibility | Deterministic seed (42); byte-identical regeneration previously verified; 0-error notebook/SQL execution |

## 14. Cross-Tool Validation

The previously established 18-metric cross-check (Python ↔ SQL ↔ Excel, with Power BI figures included only as **independently Python-re-derived expected values**, never as executed DAX output) was reviewed and its underlying totals were re-confirmed at this audit via fresh recomputation from the clean CSV (Section 10). **This remains true in the current repository.**

| Metric | Python | SQL | Excel | Power BI (Python-derived reference, not executed) | Match |
|---|---|---|---|---|---|
| Total Revenue | €7,765,475.38 | €7,765,475.38 | €7,765,475.38 | €7,765,475.38 | Yes |
| Total Profit | €2,733,273.35 | €2,733,273.35 | €2,733,273.35 | €2,733,273.35 | Yes |
| Total Orders | 9,985 | 9,985 | 9,985 | 9,985 | Yes |
| Total Quantity | 20,391 | 20,391 | 20,391 | 20,391 | Yes |
| AOV | €777.71 | €777.71 | €777.71 | €777.71 | Yes |
| Profit Margin | 35.20% | 35.20% | 35.20% | 35.20% | Yes |
| Laptop Revenue | €3,913,418.03 | €3,913,418.03 | €3,913,418.03 | €3,913,418.03 | Yes |
| Laptop Profit | €1,268,139.49 | €1,268,139.49 | €1,268,139.49 | €1,268,139.49 | Yes |
| Germany Revenue | €2,334,832.14 | €2,334,832.14 | €2,334,832.14 | €2,334,832.14 | Yes |
| Germany Profit | €826,074.21 | €826,074.21 | €826,074.21 | €826,074.21 | Yes |
| Netherlands AOV | €786.22 | €786.22 | €786.22 | €786.22 | Yes |
| Laptop × Germany | €1,180,603.33 | €1,180,603.33 | €1,180,603.33 | €1,180,603.33 | Yes |
| Orders YoY | +2.86% | +2.86% | (referenced) | (referenced) | Yes |
| Revenue YoY | +3.73% | +3.73% | +3.73% | +3.73% | Yes |

**Important, interview-relevant distinction:** the "Power BI" column above was never produced by Power BI Desktop executing DAX — Power BI Desktop was unavailable throughout this project (macOS environment). Those values were obtained by independently reproducing the *documented DAX logic* in Python against the same clean CSV. This distinction must be preserved in any interview explanation: "I verified the DAX measure logic would produce the correct values by independently recomputing it in Python, since I didn't have access to Power BI Desktop to execute it directly."

## 15. Interview Strengths (Ranked, Evidence-Checked)

1. **Cross-tool analytical consistency** — 18/18 metrics matching across 3 independently executed tools is a genuinely strong, verifiable claim (Section 14).
2. **Business KPI analysis** — a consistent, reused KPI framework (not redefined per tool) across Python/SQL/Excel.
3. **SQL depth** — CASE, CTEs, subqueries, a justified JOIN, and 4 different window functions, all genuinely present (Section 7), not just basic SELECTs.
4. **Excel business analysis** — a fully formula-driven (not hardcoded) 12-sheet workbook with conditional formatting and charts (Section 8).
5. **Data validation discipline** — a documented, reproducible Phase 2 cleaning pipeline plus independent re-validation inside every downstream tool.
6. **Product/market/customer analysis depth** — genuinely multi-dimensional (not just top-line totals), including a Product×Country cross-tab.
7. **Business recommendations tied to evidence** — 8 recommendations, each traceable to a specific finding, each with a stated limitation (not overclaimed).
8. **Honest limitations** — the repeat-customer and seasonality caveats are disclosed prominently and consistently, which is itself a mark of analytical maturity.
9. **Power BI specification knowledge** — DAX measure design and data-modeling reasoning (star-schema-vs-single-table decision) demonstrated even without Power BI Desktop access.

This ranking is supported by direct repository evidence checked in Sections 6–10 above, not asserted.

## 16. Interview Weaknesses / Limitations (Honest)

- **Synthetic/generated dataset** — no real company, real customers, or real transactions anywhere in the project. Must be disclosed proactively, not just if asked.
- **No production deployment** — this is a static analytical artifact set (notebook, SQL DB, Excel file, spec docs), not a running application or live dashboard.
- **Power BI is a specification, not a built `.pbix`** — genuinely the weakest point technically; must be framed honestly (Section 9), never overstated.
- **Limited real-world operational context** — no marketing, discount, inventory, returns, or true customer-tenure data; several natural follow-up business questions cannot be answered from this data.
- **Customer-data generation artifacts** — the 99.88% repeat rate is a known limitation of the synthetic design, not a real finding (Section 12).
- **No absence of live/streaming data** — all analysis is static/batch on a fixed snapshot.
- **No real stakeholder requirements process** — the business problem and KPIs were self-defined for portfolio purposes, not gathered from an actual business stakeholder.
- **No LICENSE file** — noted at this audit; a minor packaging gap, not an analytical one.

## 17. Claims to Avoid

Explicit list, cross-checked against Sections 9 and 12:

- "Built / developed / created / deployed a Power BI dashboard" — **false**; only a specification exists.
- "99.88% customer retention" / "excellent customer loyalty" / "strong repeat purchasing" / "high customer lifetime value" — **unsupported**; it is a data-generation artifact.
- "The project proved seasonal demand / holiday effects / monthly seasonality" — **false**; the finding is the *absence* of material seasonality.
- "Germany performs better because [any unmeasured cause]" — **unsupported**; no demographic/economic/competitive data exists.
- "Quantity causes revenue" or similar causal phrasing about mechanically-related fields — **misleading**; Revenue/Cost/Profit relationships are formula-derived by construction.
- Any claim implying this is real company data — **false**; the dataset is disclosed as synthetic everywhere.

## 18. Source-of-Truth References

All facts in this document trace to direct inspection, at this audit, of:
`README.md`, `data/README.md`, `data/data_dictionary.md`, `data/generate_data.py`,
`data/clean_data.py`, `data/clean/sales_data_clean.csv`, `notebooks/sales_analysis.ipynb`,
all 10 `sql/*.sql` files, `sql/README.md`, `excel/sales_business_analysis.xlsx`,
`excel/README.md`, all 6 `powerbi/*.md` files, and (for historical/internal
context only, not published) the locally-retained `reports/` folder from prior
project phases.

## 19. Public/Private Separation Policy

- The public repository (`sales-performance-business-analytics`) contains only the analytical implementation: data pipeline, notebook, SQL, Excel workbook, Power BI specification, and a single top-level `README.md`. It does **not** contain the `reports/` folder (phase-by-phase build reports, `business_insights.md`, `management_summary.md`) — that folder was intentionally untracked from git and added to `.gitignore` in the public repository, per explicit prior instruction, and remains local-only there.
- This private repository (`sales-performance-business-analytics-private`) contains **only** Sales-project interview/CV preparation material. It must never contain unrelated Café project material (`cafe-demand-forecasting-inventory`, `cafe-demand-forecasting-private`).
- This audit performed **zero** write operations against the public repository — no commit, no push, no file modification.

## 20. Baseline SHA

`6d68c35b8517609ca5a1021061c453eeed156c01` (public repository `main` branch, at the time this audit began and — verified again at the end of this audit — unchanged throughout).

## 21. Audit Date

2026-08-29

## 22. Final Baseline Verdict

**READY FOR INTERVIEW PACKAGING.**

Every headline metric was independently re-derived from the actual clean dataset and matched the previously published figures exactly, with zero discrepancies. Every technology claim (Python, SQL, Excel, Power BI specification) was verified against the actual files, not assumed. All mandatory caveats (synthetic dataset, repeat-customer artifact, no-seasonality, mechanical correlations) are intact and consistently documented. No unsupported causal or retention claim exists in the source material. The public repository was left completely unmodified throughout this audit.
