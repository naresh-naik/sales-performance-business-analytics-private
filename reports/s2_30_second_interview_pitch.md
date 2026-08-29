# S2 — 30-Second Interview Pitch & Project Story

**Status:** INTERNAL, PRIVATE interview material. Lives only in
`sales-performance-business-analytics-private`. Never added to the public
`sales-performance-business-analytics` repository.

---

## 1. Project Title

**Sales Performance & Business Analytics**

## 2. Business Problem

A multi-country electronics retailer has transaction-level sales data but
no structured way to see what's actually driving performance: which
products and markets generate revenue versus profit, how customer segments
compare, whether performance changes over time, and which product-market
combinations are strongest. The objective is to turn raw order data into a
clean KPI framework, cross-checked analysis, and evidence-based
recommendations — nothing more sophisticated than that.

## 3. 30-Second Version

This project analyzes sales performance for a fictional multi-country
electronics retailer selling five products across Germany, Austria,
France, and the Netherlands, using about ten thousand transaction records.
I cleaned the data and built the KPI analysis in Python and SQL, then
reproduced the same numbers in a formula-driven Excel report and designed
a Power BI specification on top of it. The standout finding was that
laptops drive half of total revenue but actually have the lowest profit
margin, while Germany leads on revenue but the Netherlands has the highest
order value — which changes how you'd prioritize products and markets.

## 4. 45-Second Version

The business problem was that a multi-country electronics retailer had raw
transaction data but no structured way to see which products, markets, and
customers were actually driving revenue versus profit. I worked with about
ten thousand orders across five products and four European markets,
cleaned the data through a documented validation process, and then built a
consistent KPI framework in Python and SQL — revenue, profit margin,
average order value, and product and market contribution. The clearest
finding was that laptops generate half of total revenue but carry the
lowest margin, while Germany leads on revenue and the Netherlands has the
highest order value. Based on that, my recommendation was that the
business should track margin alongside revenue rather than optimizing for
revenue alone, since the two don't always point to the same product or
market.

## 5. 60-Second Version

I built an end-to-end sales analytics project on a synthetic dataset of
about ten thousand transactions for a fictional electronics retailer,
covering five products and four European markets over two years. After
cleaning and validating the data, I calculated the core KPIs — revenue,
profit, margin, and average order value — independently in Python and
SQL, then rebuilt the same analysis as a formula-driven Excel workbook.
Every major number matched exactly across all three tools, which gave me
real confidence in the results. I also designed a Power BI data model and
dashboard specification, though I couldn't build it in Power BI Desktop
since I was working on macOS. The key finding: laptops drive half of
revenue but have the lowest margin, while Germany leads on revenue and
the Netherlands has the highest order value — revenue and profitability
leadership aren't the same here. Because the dataset is synthetic, I was
careful not to over-claim: a very high repeat-purchase rate turned out to
be an artifact of how customer IDs were generated, not real loyalty.

## 6. Business Analyst Version

I approached this as a business problem first: a multi-country electronics
retailer needed a clear picture of what's actually driving revenue and
profit, not just a data dump. I built a KPI framework — total revenue,
profit margin, average order value, and contribution by product and
market — and used it to compare performance across five products and four
countries. The key insight for management is that the product generating
the most revenue, laptops, is not the most profitable one on a margin
basis, and the country leading on revenue, Germany, isn't the same country
with the highest order value. That distinction directly changes how I'd
recommend a business prioritize commercial attention — using margin and
order value alongside revenue, not revenue alone — and I also flagged
where the data has real limits, like customer behavior patterns that
looked strong but turned out not to be reliable evidence of anything.

## 7. Data Analyst Version

I took a raw, intentionally imperfect transaction dataset, ran it through
a documented cleaning process — handling duplicates, missing values, and
inconsistent categories — and validated the result against explicit rules
before doing any analysis. From there I used Python and pandas for
exploratory analysis and KPI calculation, then rebuilt the same
calculations in SQL to check that I got identical numbers, and again in
Excel using live formulas rather than typed-in values. Every core metric —
revenue, profit, margin, average order value, and the product and country
breakdowns — matched exactly across all three tools. I also segmented the
data by customer type and by product-market combination to see where
performance concentrated, and used basic statistics like outlier checks
and correlation to sanity-check the numbers before drawing conclusions.

## 8. BI / Analytics Analyst Version

I designed a single, reusable KPI framework — revenue, profit, margin,
average order value, and contribution percentages — and made sure it
produced the exact same numbers whether it was calculated in Python, in
SQL against a database, or in a formula-driven Excel report. On top of
that shared data model, I designed a Power BI specification: the table
structure, a date dimension, the DAX measures, and a four-page dashboard
layout covering an executive overview, product performance, market
performance, and customer detail. I want to be clear that this was a
specification I designed, not an interactive dashboard I built — I didn't
have Power BI Desktop available in my environment, so I verified the DAX
logic by independently reproducing it in Python rather than executing it.
What I'd highlight is the cross-tool consistency: eighteen core metrics
reconciled exactly across every layer, which is the kind of reporting
discipline you'd want before anyone trusts a number in a dashboard.

## 9. Core Project Story

| Stage | What to remember when speaking |
|---|---|
| **Problem** | A multi-country electronics retailer needs a structured view of revenue vs. profit performance by product, market, and customer segment — not just raw transactions. |
| **Data** | ~10,000 synthetic transaction records, 5 products, 4 European markets, 850 customers, 2024–2025. Explicitly disclosed as synthetic, generated with a fixed seed for reproducibility. |
| **Cleaning** | The raw data had a small, intentionally introduced set of issues (duplicates, missing values, invalid quantities, category typos, formula mismatches); a documented, reproducible pipeline cleaned and validated it before analysis. |
| **Analysis** | Independent KPI, product, market, customer, time, and profitability analysis in Python and SQL, then rebuilt as a fully formula-driven Excel workbook — same definitions, same source data, three different tools. |
| **Validation** | Eighteen core metrics were cross-checked across Python, SQL, and Excel and matched exactly; Power BI's DAX logic was verified the same way, by reproducing it in Python, since Power BI Desktop wasn't available. |
| **Insights** | Laptop leads revenue and profit but has the lowest margin; Keyboard has the opposite pattern. Germany leads revenue and profit; Netherlands leads on order value. These are different products and different markets, which is the real finding. |
| **Recommendations** | Track margin and order value alongside revenue, not revenue alone; monitor the product-market combinations that lead on each metric separately; keep the same repeatable data-quality process for any future data. |
| **Limitations** | The dataset is synthetic and disclosed as such; a very high repeat-purchase rate turned out to be a data-generation artifact, not real loyalty; Power BI is a specification, not a built dashboard; no real stakeholder requirements or production deployment exist. |

## 10. My Role

I independently designed and executed the entire project: generating and
cleaning the synthetic dataset, building the Python EDA and KPI analysis,
writing the SQL business-question queries, building the formula-driven
Excel workbook, and designing the Power BI data model and dashboard
specification. I also ran the cross-tool validation myself, catching and
fixing at least one real bug in the process (an Excel summary formula that
looked correct but was quietly assuming a fixed row order). This was not a
team project, and it was not deployed anywhere in production — it's a
self-contained analytical portfolio project.

## 11. Most Important Result

**Eighteen core business metrics — revenue, profit, margin, product and
market breakdowns, year-over-year growth, and the strongest product-market
combination — reconciled exactly across Python, SQL, and Excel, computed
independently in each tool.**

I'm not choosing the largest number here on purpose. To a recruiter, a
single big revenue figure doesn't say much on its own — what actually
signals analyst-level rigor is that the same numbers were independently
verified across three different tools and didn't drift. That's the kind
of validation discipline that prevents a wrong number from ever reaching a
manager's dashboard, and it's the result I'd lead with if asked "why
should I trust your numbers?"

## 12. Most Interesting Business Insight

**Laptop generates the most revenue and the most profit, but has the
lowest profit margin of the five products (32.40%) — while Keyboard, the
lowest-revenue product, has the highest margin (47.34%).**

This is more interesting than a simple ranking because it's not something
you'd see from a one-line "top product" summary — it only shows up once
you look at revenue, profit, *and* margin side by side. It demonstrates
that I didn't stop at "which product sells the most," but asked whether
the biggest revenue driver was also the most efficient one, and found that
it wasn't. That's the kind of distinction that actually changes a
prioritization decision.

## 13. Analytical Judgment

The most important judgment call in this project was treating cross-tool
validation as a required step, not an optional nice-to-have. I calculated
every core KPI independently in Python, in SQL, and in Excel, using the
same source data but three completely separate calculation paths, and
required all eighteen metrics to match exactly before treating any number
as trustworthy. For Power BI, since I didn't have Power BI Desktop
available, I was explicit that I verified the *DAX measure logic* by
reproducing it in Python — I never presented that as an executed dashboard
result. This demonstrates reproducibility, comfort working across multiple
analytical tools, and — maybe most importantly — the discipline to say
clearly what was actually executed versus what was independently verified
logic, rather than blurring the two.

## 14. Most Surprising Finding

The most surprising number in the project is that 99.88% of customers
placed more than one order. On its own that looks like an extraordinary
retention result. But when I traced it back to how the dataset was built,
it turned out to be a direct consequence of the synthetic data generation:
only 850 customer IDs were created and then reused across roughly ten
thousand orders, which mechanically produces a very high repeat-order rate
regardless of any actual purchasing behavior. I explicitly do not present
this as evidence of customer loyalty or retention. Recognizing this
mattered because it would have been easy to report an impressive-sounding
number without checking where it actually came from — and catching that is
exactly the kind of skepticism an analyst is supposed to apply before
reporting a result.

## 15. Business Value

**What the analysis enables:** a consistent, cross-validated KPI view of
revenue, profit, margin, and contribution by product, market, and customer
segment, instead of ad hoc totals.

**What decision it supports:** where to focus commercial and inventory
attention — distinguishing "highest revenue" from "highest margin" from
"highest order value," since this project shows they aren't always the
same product or market.

**What it reveals:** that revenue leadership and profitability leadership
can diverge, and that a headline metric (like a 99.88% repeat rate) can be
a data artifact rather than a real signal — both are things a decision-maker
would want flagged, not hidden.

**What data would be needed next:** real transaction history, actual cost
breakdowns, genuine customer tenure, and marketing/channel data, before any
of this could inform an actual business decision rather than a portfolio
demonstration.

I'm not claiming any actual cost savings, revenue increase, retention
improvement, or production impact from this project — none of that was
measured, because this is a synthetic, non-deployed analysis.

## 16. Limitations

I'd be upfront about the limitations if asked. The dataset is entirely
synthetic — a fictional electronics retailer, generated by my own script
with a fixed random seed, not real transactions from a real company. It's
a single generated dataset, not something validated against real business
requirements or a real stakeholder. Nothing here was deployed anywhere;
there's no production system, no live dashboard, and no real Power BI
build — just a complete specification for one, since I didn't have Power
BI Desktop available on macOS. Some patterns in the data, like the very
high repeat-purchase rate, are artifacts of how the data was generated
rather than real customer behavior. And because there's no real-world
experiment or external variables in the data, I can describe what the
numbers show, but I can't draw causal conclusions about why any market or
product performs the way it does.

## 17. What I Would Do Next

1. Replace the synthetic dataset with real transaction data, if this were
   applied to an actual business.
2. Validate the business questions and KPI definitions directly with
   stakeholders rather than assuming them.
3. Add real product cost and margin data instead of a single aggregated
   cost field.
4. Add genuine customer-level longitudinal data to measure real retention,
   instead of relying on the current customer ID structure.
5. Add inventory, returns, and marketing/channel data if the business
   questions required them.
6. Actually build and test the Power BI dashboard in Power BI Desktop once
   that environment is available.
7. Set up a refresh and monitoring process so the KPIs stay current
   against live data.

## 18. What I Would Do Differently

1. Start with a written list of stakeholder questions before designing the
   KPI framework, even in a self-directed project, to practice that habit.
2. Add a lightweight cost-driver breakdown at generation time, so
   profitability findings could go one level deeper than "margin differs."
3. Build the Power BI report earlier in the process (on a machine with
   Power BI Desktop) rather than treating it as a specification-only
   deliverable from the start.
4. Simulate a slightly more realistic customer structure so repeat-purchase
   analysis wouldn't need as large a caveat.
5. Keep a single running validation log from the start instead of
   reconstructing the cross-tool check after each tool was built.

## 19. Hardest Part

The hardest part was keeping KPI definitions genuinely consistent across
four different tools and independently validating eighteen metrics between
them. It's easy for a formula in Excel to quietly diverge from a pandas
calculation or a SQL aggregation — different rounding, a different join
condition, a stale reference — and initial versions did have at least one
real bug like that, where an Excel summary cell assumed a fixed row order
instead of genuinely looking up the top result. Finding and fixing that
kind of subtle inconsistency, rather than assuming a spreadsheet or a
notebook is correct just because it runs without an error, was the most
demanding and most valuable part of the project.

## 20. STAR Version

**Situation:** A multi-country electronics retailer's sales data existed
only as raw transactions, with no consistent way to compare revenue,
profit, and performance across products, markets, and customer segments.

**Task:** Build a validated analytical pipeline — from data generation and
cleaning through Python, SQL, and Excel analysis, plus a Power BI
specification — that produces trustworthy, cross-checked business KPIs and
turns them into evidence-based recommendations.

**Action:** I generated and cleaned a synthetic 9,985-row transaction
dataset, built independent KPI/product/market/customer/time/profitability
analysis in Python and SQL, rebuilt the same analysis as a formula-driven
Excel workbook, cross-validated eighteen core metrics across all three,
and designed a Power BI data model, DAX measures, and dashboard
specification.

**Result — demonstrated analytical result:** all eighteen cross-checked
metrics matched exactly across Python, SQL, and Excel; the analysis
identified that revenue leadership (Laptop, Germany) and profitability/
order-value leadership (Keyboard's margin, Netherlands' AOV) belong to
different products and markets; one real implementation bug was found and
fixed during validation.

**Result — unmeasured real-world business impact:** none claimed. This is
a synthetic, non-deployed portfolio project — no actual revenue increase,
cost saving, or retention improvement was measured or should be implied.

## 21. Problem → Approach → Result → Decision

| Stage | Summary |
|---|---|
| **Problem** | A multi-country electronics retailer needs a structured, trustworthy view of revenue vs. profit performance across products, markets, and customers. |
| **Approach** | Clean and validate the data, then independently compute a shared KPI framework in Python, SQL, and Excel, cross-check the results, and design a Power BI specification on the same model. |
| **Result** | 18/18 core metrics matched exactly across tools; Laptop leads revenue/profit but has the lowest margin; Germany leads revenue/profit but Netherlands leads AOV. |
| **Decision** | Prioritize product and market attention using margin and order value alongside revenue — not revenue alone — and treat the repeat-purchase rate as a data artifact, not a loyalty signal. |

## 22. Interview Follow-Up Map

| Likely Question | Short Transition |
|---|---|
| Why Python? | "For the exploratory analysis and KPI calculations, since pandas made it easy to iterate — happy to walk through the notebook." |
| Why SQL? | "To demonstrate business-question querying against a real database, and as an independent check on the Python numbers." |
| Why Excel if Python was used? | "Because most business stakeholders still work in Excel — I wanted the same numbers accessible as a formula-driven report, not just a notebook." |
| Why Power BI? | "To design the reporting layer a business would actually use day to day — I can walk through the data model and DAX measures." |
| Why no actual Power BI dashboard? | "Power BI Desktop isn't available on macOS, so I built a complete specification instead and verified the logic in Python — I can show exactly what's specified." |
| What was the most important KPI? | "Profit margin, alongside revenue — I can explain why those two together tell a more complete story than revenue alone." |
| Why does Laptop lead revenue but have lower margin? | "That's one of the clearest findings — let me walk through the product-level numbers." |
| Why does Germany lead revenue? | "It's the top market by both revenue and profit in the data — I can show the full country breakdown." |
| Why is Netherlands important? | "It has the highest average order value, even though it's not the top market by total revenue — that distinction matters." |
| What does 99.88% repeat rate mean? | "That's actually a data-generation artifact, not real retention — let me explain how I traced that." |
| How did you validate the results? | "I cross-checked eighteen metrics across Python, SQL, and Excel independently — I can show the comparison." |
| Why should I trust your numbers? | "Because they weren't computed once — they were computed three separate ways and matched exactly." |
| What business decision does the analysis support? | "Where to focus commercial attention, based on margin and order value, not just revenue." |
| What would you do with real company data? | "Re-validate the business questions with stakeholders first, then apply the same framework to real transactions." |

(Full detailed Q&A answers belong in a later document, not here.)

## 23. Recommended Analyst Terminology

Analyzed · Validated · Benchmarked · Reconciled · Quantified · Compared ·
Identified · Evaluated · Segmented · Aggregated · Assessed · Interpreted ·
Visualized · Investigated · Recommended · Decision support · Cross-checked
· Reproducible · Documented · Traced

## 24. Terms to Avoid

| Term | Why it's unsafe here |
|---|---|
| AI-powered | No AI/ML technique was used anywhere in the project. |
| Machine-learning model | No ML model exists in the project. |
| Forecasting | No forecasting/time-series prediction was implemented. |
| Optimized | Nothing was tuned or optimized against an objective function — this was descriptive analysis. |
| Automated | The pipeline is reproducible via scripts, but nothing runs automatically/unattended in production. |
| Production-ready | The project was never deployed or hardened for production use. |
| Deployed | No component is deployed anywhere — all artifacts are local files. |
| Real-time | All analysis is static/batch on a fixed historical snapshot. |
| Guaranteed | No result should be described as guaranteed; findings are descriptive of this dataset only. |
| Proved | The project *found* patterns (e.g., no seasonality); it didn't "prove" anything in a general business sense. |
| Customer retention | The 99.88% figure is a data-generation artifact, not measured retention. |
| Customer loyalty | Same reason — not supported by this data. |
| Built Power BI dashboard | Only a specification exists — no `.pbix` was ever created. |
| Developed Power BI dashboard | Same — inaccurate; use "designed a Power BI specification" instead. |
| Reduced costs | No cost reduction was measured or implemented anywhere. |
| Increased revenue | No revenue change was caused by this project — it's a portfolio analysis, not a live intervention. |

## 25. Interview Memory Card

```
PROJECT        Sales Performance & Business Analytics
PROBLEM        Multi-country electronics retailer needs revenue vs. profit clarity
DATA           ~10,000 synthetic orders, 5 products, 4 markets, 850 customers
TOOLS          Python, SQL, Excel, Power BI specification
ANALYSIS       KPI + product + market + customer + time + profitability analysis
KEY KPI        Revenue €7.77M, Profit €2.73M, Margin 35.20%
KEY FINDING    Laptop leads revenue/profit but lowest margin; Germany leads, Netherlands highest AOV
VALIDATION     18/18 core metrics matched across Python, SQL, Excel
BUSINESS VALUE Prioritize by margin + order value, not revenue alone
LIMITATION     Synthetic data; Power BI is a specification, not a built dashboard
```

## 26. Final Spoken Version

I built a sales analytics project for a fictional multi-country electronics
retailer selling five products — laptops, phones, tablets, monitors, and
keyboards — across Germany, Austria, France, and the Netherlands, using
about ten thousand synthetic transaction records. I cleaned and validated
the data, then built a KPI framework covering revenue, profit, margin, and
average order value, applied across product, market, customer, and time
dimensions. What made this stronger than just running some pandas
code was that I calculated every core number independently in Python, SQL,
and a fully formula-driven Excel workbook, and checked that all of them
matched — which they did. I also designed a Power BI data model and
dashboard specification, but I want to be honest that I didn't have Power
BI Desktop available to actually build it, so I verified that logic in
Python instead of claiming a dashboard that doesn't exist. The most useful
finding was that laptops drive the most revenue but are actually the least
profitable product by margin, while Germany leads on revenue but the
Netherlands has the highest order value — revenue leadership and
profitability leadership point to different products and markets. I also
caught a case where a very high repeat-purchase rate turned out to be an
artifact of how the dataset was generated, not real customer loyalty, and
made sure not to overstate that. Overall, the project shows I can take
messy data, build trustworthy KPIs across multiple tools, and turn that
into a business recommendation I can defend.
