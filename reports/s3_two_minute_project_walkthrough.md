# S3 — 2-Minute Analyst Project Walkthrough

**Status:** INTERNAL, PRIVATE interview material. Lives only in
`sales-performance-business-analytics-private`. Never added to the public
`sales-performance-business-analytics` repository. S1 and S2 were not
modified to produce this document.

---

## A. Project Overview

**Business problem:** a fictional multi-country electronics retailer has
transaction data but no structured way to compare revenue vs. profit
performance across products, markets, and customer segments, or to see
whether performance is trending over time.

**Dataset:** 9,985 clean transaction records, 12 columns, 5 products
(Laptop, Phone, Tablet, Monitor, Keyboard), 4 markets (Germany, Austria,
France, Netherlands), 850 customers, 20,391 total units sold,
2024-01-01 to 2025-12-31. Explicitly synthetic, generated with a fixed
random seed (42).

**Core KPI reference (exact figures, for defense under questioning):**
Total Revenue €7,765,475.38 · Total Profit €2,733,273.35 · Profit Margin
35.20% · Average Order Value €777.71 · Revenue YoY (2024→2025) +3.73% ·
Orders YoY +2.86% · Monthly revenue coefficient of variation 9.41% (no
material seasonality).

**Tools:** Python/pandas for EDA and KPI calculation, SQL against a
SQLite database for business-question queries, a formula-driven Excel
workbook, and a Power BI implementation specification (data model, DAX
measures, dashboard design — not an executed `.pbix`, since Power BI
Desktop was unavailable on macOS).

**Main outcome:** 18 core business metrics were independently calculated
in Python, SQL, and Excel and matched exactly. The analysis found that
revenue leadership and profitability leadership belong to different
products and markets — Laptop leads revenue and profit but has the lowest
margin; Germany leads revenue and profit but the Netherlands has the
highest order value — leading to a recommendation to track margin and
order value alongside revenue, not revenue alone.

## B. Business Analyst Version

A multi-country electronics retailer had raw sales transactions but no
structured way to answer basic management questions: which products and
markets actually drive revenue versus profit, how customer segments
compare, and where performance is trending. I built a consistent KPI
framework — total revenue, profit, margin, and average order value — and
applied it across every product, market, and customer segment so the
numbers would be directly comparable rather than one-off totals.

The clearest business finding was that Laptop drives just over half of
total revenue and leads on profit, but actually carries the lowest margin
of the five products, at 32.4%, while Keyboard — the smallest revenue
contributor — has the highest margin, at 47.3%. A similar pattern showed
up at the market level: Germany leads on both revenue and profit, but the
Netherlands has the highest average order value. Neither of those is a
coincidence I could explain from the data — the data doesn't include
customer demographics or competitive information — so I reported them as
observed patterns, not causes.

Based on that, my recommendation was that management should evaluate
products and markets on margin and order value together, not revenue
alone, since the two don't always point to the same place. I also flagged
a limitation upfront: a very high repeat-purchase rate in the data turned
out to be an artifact of how the dataset was generated, not real customer
loyalty, and I made sure that didn't get reported as a business result.
The dataset itself is synthetic, which I disclose clearly rather than
implying it's a real company's numbers.

## C. Data Analyst Version

I started with an intentionally imperfect synthetic dataset — about ten
thousand transaction rows with a small, documented set of issues:
duplicate rows, missing category values, invalid quantities, and a few
inconsistent country labels. I built a reproducible cleaning pipeline that
detected each issue type, applied a specific fix (deduplication,
re-deriving category from product, removing unrecoverable rows,
standardizing typos), and validated the result against explicit rules
before any analysis began.

From there I used Python and pandas for exploratory data analysis —
distributions, outlier checks using IQR, and correlation analysis — and
built engineered features like year, month, and quarter for time-based
grouping. I calculated the core KPIs (revenue, profit, margin, average
order value) and broke them down by product, market, customer segment, and
time period.

To make sure the numbers were actually correct, I independently rebuilt
the same calculations in SQL against a database, using GROUP BY,
window functions, and CTEs, and again in Excel using live formulas
rather than typed-in values. I compared eighteen core metrics across all
three implementations and they matched exactly, which is the check I'd
point to if anyone asked how I know the numbers are right.

The quantitative findings were consistent across every method: total
revenue of €7.77 million, 35.2% profit margin, Laptop contributing just
over half of revenue but the lowest margin at 32.4%, and Germany leading
revenue while the Netherlands led on order value. I treated those last two
findings as descriptive results, not causal explanations, since the
dataset doesn't contain the variables needed to explain "why."

## D. BI / Analytics Analyst Version

I designed a single, shared KPI framework — total revenue, profit, margin,
average order value, and contribution percentages by product and market —
and made sure it produced identical results whether it was calculated in
Python, queried from a SQL database, or built as formulas in an Excel
report. That consistency was the core reporting-layer design goal: one set
of business definitions, reproduced independently across tools, rather
than redefining metrics differently in each one.

On top of that shared data model, I designed a Power BI implementation
specification: the fact table structure, a date dimension for time
intelligence, a full set of DAX measures (core KPIs, product and market
ranking, customer segmentation, year-over-year growth), and a four-page
dashboard layout — executive overview, product performance, market
performance, and customer detail, each with the relevant slicers and
visuals mapped out.

I want to be explicit about one thing: Power BI Desktop wasn't available
in my working environment, so I never built or executed the `.pbix` file.
What exists is a complete specification — I verified the DAX measure logic
was correct by independently reproducing the same calculations in Python
against the same dataset, rather than claiming a dashboard that doesn't
exist.

What I'd highlight from a BI-reporting standpoint is the cross-tool
validation itself: eighteen core metrics reconciled exactly across Python,
SQL, and Excel. That's the kind of reporting discipline that has to exist
before a business ever trusts a number on a dashboard, and it's the habit
I'd bring into a real Power BI build the moment I had Desktop access.

## E. Project Walkthrough Framework

| Stage | What I Did | Why It Mattered |
|---|---|---|
| **1. Business problem** | Defined the question: which products, markets, and customers actually drive revenue vs. profit for a multi-country retailer. | Without a defined problem, KPI work becomes arbitrary — this anchored every later decision. |
| **2. Data** | Generated a synthetic 9,985-row dataset (5 products, 4 markets, 850 customers, 2 years) with a fixed seed, explicitly disclosed as synthetic. | Gave a controlled, reproducible base to build a full analyst workflow on, without implying real company data. |
| **3. Cleaning** | Detected and fixed 6 documented issue types (duplicates, missing values, invalid quantities, category typos) via a reproducible pipeline. | Demonstrates the analyst habit of never trusting raw data — validate before analyzing. |
| **4. KPI framework** | Defined revenue, profit, margin, and AOV once, then reused the same definitions everywhere. | A metric that means something different in two reports is a common real-world failure — this avoided it. |
| **5. Multi-dimensional analysis** | Broke KPIs down by product, market, customer segment, time period, and product×market combination. | Surfaced the revenue-vs-margin split that a single top-line number would have hidden. |
| **6. Cross-tool validation** | Independently recomputed 18 core metrics in Python, SQL, and Excel and confirmed they matched exactly. | This is the strongest evidence of analytical reliability in the whole project. |
| **7. Business insights** | Interpreted findings cautiously — descriptive statements only, no unsupported cause given for market/product differences. | Shows judgment about what the data can and can't support. |
| **8. Recommendations** | Recommended tracking margin and order value alongside revenue, and flagged the repeat-rate figure as a data artifact, not a result. | Converts analysis into an actionable, honestly-scoped business takeaway. |

## F. Why I Chose This Project

I didn't pick this project to "learn Python" — I picked it because it let
me trace one thread end to end: raw sales transactions turn into business
KPIs, KPIs turn into a revenue-versus-profit comparison across products
and markets, and that comparison turns into an actual recommendation about
where a business should focus. That chain — data to KPI to insight to
decision — is what an Analyst role actually is, and I wanted a project
that forced me to defend every step of it, including the parts where the
data has real limits.

## G. My Role

I independently designed and executed the entire project: generating and
cleaning the synthetic dataset, building the Python EDA and KPI analysis,
writing the SQL business-question queries, building the formula-driven
Excel workbook, and designing the Power BI data model, DAX measures, and
dashboard specification. I also ran the cross-tool validation myself and
found and fixed a real bug during that process — an Excel summary formula
that quietly assumed a fixed row order instead of genuinely looking up the
top result. This was not a team project and nothing was deployed to
production; it's a self-contained analytical portfolio project.

## H. Most Important Result

**18 out of 18 required metrics reconciled exactly across Python, SQL, and
Excel — computed independently in each tool, not copied between them.**

I lead with this rather than "revenue was €7.77 million" because a single
big number doesn't tell a recruiter anything about whether it's correct.
What actually demonstrates Analyst-level rigor is that the same result
was produced three separate ways and didn't drift — that's the standard
that prevents a wrong number from ever reaching someone's dashboard, and
it's the answer I'd give to "why should I trust your numbers?"

## I. Most Important Business Finding

Laptop generated 50.40% of total revenue and led on both revenue and
profit — but had the lowest product margin of the five products, at
32.40%, while Keyboard, the smallest revenue contributor, had the highest
margin, at 47.34%. The business interpretation is limited to what the
data actually supports: Laptop's scale makes it the largest absolute
profit contributor even with a thinner margin, and that's a genuine
trade-off between scale and efficiency worth flagging to management. I
deliberately don't infer *why* Laptop's margin is lower — the dataset's
Cost field doesn't break down into sub-components like materials or
logistics, so any specific cause would be speculation, not a finding.

## J. Secondary Business Finding

Germany leads on both revenue and profit among the four markets, but the
Netherlands has the highest average order value at €786.22. Declaring one market
simply "best" would hide that these are two different signals: total
market scale versus typical transaction size. A market can lead on one and
not the other, and a business deciding where to invest commercial
attention needs both numbers side by side — revenue tells you where the
volume is, AOV tells you where individual transactions are largest —
rather than a single ranked list that only shows revenue.

## K. Product-Market Finding

Laptop × Germany was the strongest single product-market combination,
generating €1,180,603.33 in revenue — more than any other product-country
pairing in the dataset. Finding this required looking at the data in two
dimensions at once, not just product totals or country totals separately,
which is what a cross-dimensional matrix (Product rows, Country columns)
is for. I don't claim this combination is strong *because* of anything
specific about German demand for laptops — the dataset has no variable
that would support that — only that it's the largest revenue cell in the
matrix as calculated.

## L. Most Surprising Data Finding

99.88% of customers — 849 out of 850 — placed more than one order. On its
own that number looks like an outstanding retention result. But tracing it
back to how the dataset was built showed it's a direct consequence of the
generation process: only 850 customer IDs were created and then reused
across roughly ten thousand orders, which mechanically produces a very
high repeat-order rate no matter what actual purchasing behavior might
have looked like. If asked "isn't 99.88% repeat rate excellent?", my
answer is: it looks excellent, but I wouldn't use it as evidence of
customer loyalty, because the dataset generation process reuses customer
IDs in a way that produces that high rate by construction, not because it
reflects real repeat-purchase behavior.

## M. Hardest Analytical Part

The hardest part was keeping KPI definitions genuinely identical across
four different tools and independently validating eighteen metrics between
them — it's easy for a rounding difference, a different join condition, or
a stale cell reference to quietly break that consistency. That's exactly
what happened once: an early version of the Excel `Business_Summary` sheet
had a formula that assumed the "top product" was always in a fixed row,
rather than actually looking up whichever product had the highest revenue.
**Problem:** the summary would have shown the wrong "top product" if the
row order ever changed. **Investigation:** caught by directly inspecting
the generated workbook's formulas rather than trusting that it looked
correct. **Fix:** replaced the fixed-row reference with a genuine
`INDEX/MATCH(MAX(...))` lookup. **Validation:** re-ran the cross-tool check
to confirm the corrected formula matched Python and SQL. **Lesson:** a
spreadsheet that runs without an error isn't the same as a spreadsheet
that's correct — I check formula logic, not just whether it executes.

## N. Validation Explanation

If asked "how did you know your results were correct?": I started from
the same clean dataset and calculated every core metric independently in
Python, then again in SQL against a database, then again in Excel using
live formulas rather than typed values. I compared eighteen core metrics
across all three and required an exact match before treating any number
as trustworthy — when I found a discrepancy (the Excel bug described
above), I investigated it, fixed the root cause, and reran the comparison
to confirm the fix. For Power BI, I reviewed and reproduced the DAX
measure logic in Python to confirm it was correct, but I want to be clear
that Power BI itself was never executed, since the `.pbix` file was never
built — Power BI Desktop wasn't available in my environment.

## O. Why Python, SQL, and Excel?

I didn't use three tools because "more tools looks better" — I used them
because each one demonstrates something different, and using all three on
the same numbers is itself the point. **Python** gave me flexible
exploratory analysis, calculation, and visualization. **SQL** demonstrated
database-oriented, business-question-driven querying — the skill most
directly transferable to querying a company's actual data warehouse.
**Excel** demonstrated business-friendly, formula-driven reporting that
non-technical stakeholders can open and review themselves. The real value
is that the same revenue, profit, and margin numbers were independently
reproducible across all three — that's a stronger claim than any single
tool could make on its own.

## P. Why Power BI?

Power BI is directly relevant to BI/Analyst reporting, so I designed the
full reporting layer for it: the data model, the DAX measures, and a
four-page dashboard specification covering executive, product, market, and
customer views. What I didn't do is build the actual `.pbix` file, because
Power BI Desktop wasn't available in my working environment — it's a
Windows-only application and I was working on macOS. In a real
environment, the next step would be exactly what's already specified:
open Power BI Desktop, import the clean CSV, build the date table and
relationships as documented, paste in the DAX measures, build the four
pages, and validate every number against the same 18-metric check I
already ran across Python, SQL, and Excel.

## Q. Business Value

**Demonstrated analytical value:** a structured, reusable KPI framework;
independently validated calculations across three tools; genuine
product, market, and customer-level insights (not just top-line totals);
decision-oriented recommendations tied to specific findings; a documented,
reproducible data-cleaning process.

**Unmeasured real-world business impact:** no actual revenue increase, no
actual cost reduction, no actual customer-retention improvement, and no
production business impact — none of that was measured, and I wouldn't
claim it, because this is a synthetic, non-deployed portfolio project, not
a live business intervention.

## R. Limitations

I'd volunteer these rather than wait to be asked. The dataset is entirely
synthetic — a fictional electronics retailer I generated myself with a
fixed random seed, not a real company. Customer purchasing behavior in
the data is a byproduct of how customer IDs were generated, not modeled
real behavior — that's exactly why the 99.88% repeat rate isn't reliable
evidence of anything. There were no real stakeholders defining the
business questions, and nothing here was deployed to production; the
Power BI piece is a complete specification, not a built dashboard, since
Power BI Desktop wasn't available. And because there's no real-world
experiment, no A/B test, and no external variables like marketing or
competition in the data, I can describe what the numbers show, but I
can't draw causal conclusions or claim a measured business outcome.

## S. What I Would Do Next

1. Replace the synthetic dataset with real transaction data.
2. Work with stakeholders to define the actual KPIs that matter to them.
3. Add real product cost and margin data instead of one aggregated field.
4. Add genuine customer purchase history to measure real retention.
5. Gather actual business requirements before choosing what to analyze.
6. Build and test the Power BI dashboard in Power BI Desktop.
7. Set up a refresh and monitoring process against live data.
8. Validate the recommendations with the business users who'd act on them.

## T. What I Would Do Differently

1. Write down the specific stakeholder questions before building the KPI
   framework, even in a self-directed project.
2. Lock in KPI definitions in writing before doing any calculation, so
   there's a single reference to check every tool against.
3. Design the Power BI requirements earlier, rather than treating it as a
   final-stage addition.
4. If synthetic data has to be used again, generate customer behavior more
   realistically so repeat-purchase analysis wouldn't need a caveat this
   large.
5. Keep a running validation log from the start, instead of reconstructing
   the cross-tool comparison after each tool was already built.

## U. STAR Version

**Situation:** A multi-country electronics retailer's sales data existed
only as raw transactions, with no consistent, trustworthy way to compare
revenue, profit, and performance across products, markets, and customers.

**Task:** Build a validated analytical pipeline — from data generation and
cleaning through Python, SQL, and Excel analysis, plus a Power BI
specification — that produces cross-checked KPIs and turns them into
evidence-based business recommendations.

**Action:** Generated and cleaned a synthetic 9,985-row dataset; built
independent KPI, product, market, customer, time, and profitability
analysis in Python and SQL; rebuilt the same analysis as a formula-driven
Excel workbook; found and fixed a real Excel formula bug during
validation; cross-checked 18 core metrics across all three tools; designed
a Power BI data model, DAX measures, and dashboard specification.

**Result — demonstrated analytical result:** 18/18 metrics matched exactly
across Python, SQL, and Excel; identified that revenue leadership and
profitability/order-value leadership belong to different products
(Laptop vs. Keyboard) and markets (Germany vs. Netherlands); caught a data
artifact (the repeat-rate figure) before it could be misreported as a
finding.

**Result — unmeasured real-world impact:** none claimed. No revenue was
actually increased, no cost was actually reduced, and nothing was
deployed — this is a synthetic, self-contained analytical project.

## V. Problem-Approach-Result-Decision

| Stage | Summary |
|---|---|
| **Problem** | A multi-country retailer needs a trustworthy, structured view of revenue vs. profit performance across products, markets, and customers. |
| **Approach** | Clean and validate the data; build one shared KPI framework independently in Python, SQL, and Excel; cross-check the results; design a Power BI specification on the same model. |
| **Result** | 18/18 core metrics matched across tools; Laptop leads revenue/profit but has the lowest margin; Germany leads revenue/profit but Netherlands leads AOV. |
| **Decision** | Evaluate products and markets on margin and order value alongside revenue — not revenue alone — and treat the repeat-purchase rate as a data artifact, not a loyalty signal. |

## W. 10 Deep Project Ownership Questions

| Question | Short Transition |
|---|---|
| 1. Why did Laptop have the lowest margin despite leading revenue? | "That's one of the clearest findings in the project — let me walk through the product-level numbers." |
| 2. How exactly did you calculate the 35.20% margin? | "Total profit divided by total revenue, calculated independently in Python, SQL, and Excel — I can show the formula in each." |
| 3. Why does Germany lead revenue? | "It's the top market by both revenue and profit in the data — I can show the full country breakdown." |
| 4. Why is Netherlands important if it doesn't lead revenue? | "Because it has the highest average order value — a different signal than total revenue, and worth tracking separately." |
| 5. How did you calculate the 99.88% repeat rate? | "Customers with more than one order divided by total unique customers — but I'd want to explain the caveat behind that number first." |
| 6. Why did you trust the 18/18 reconciliation? | "Because each tool calculated it independently from the same source data — I didn't copy numbers between them." |
| 7. What was the Excel bug? | "A summary formula that assumed a fixed row instead of looking up the actual top result — I can show the fix." |
| 8. Why use SQL if Python could do the same analysis? | "To demonstrate database-style querying, and as an independent check on the Python numbers." |
| 9. Why didn't you build Power BI? | "Power BI Desktop wasn't available on macOS — I designed the full specification instead and verified the logic in Python." |
| 10. What would change with real company data? | "I'd validate the KPI definitions with stakeholders first, then apply the same framework to real transactions." |

(Full detailed answers belong in a later document, not here.)

## X. Interview Interruption Map

| Interviewer Interruption | What I Should Transition To |
|---|---|
| "Why this product?" | Laptop's revenue-vs-margin finding (Section I) |
| "Why this market?" | Germany-vs-Netherlands finding (Section J) |
| "How did you validate it?" | The 18-metric cross-tool reconciliation (Section H/N) |
| "Is this real data?" | Direct, upfront: synthetic, fixed-seed generated, explicitly disclosed (Section R) |
| "Did you build Power BI?" | Direct, upfront: specification only, no `.pbix`, Desktop unavailable (Section P) |
| "What's the actual business impact?" | Demonstrated analytical value vs. unmeasured real-world impact distinction (Section Q) |
| "What would you do differently?" | Section T's 5 improvements |
| "Why should I trust these numbers?" | The 18/18 cross-tool match plus the Excel bug story as evidence of active checking (Section H/M) |

## Y. Delivery Guidance

**What to say first:** the business problem in one sentence, then the
dataset scale — not a tool list. Recruiters remember "multi-country
retailer, revenue vs. profit" before they remember "pandas."

**Which numbers to remember:** €7.77M revenue, 35.2% margin, Laptop's
50.4% share and 32.4% margin, Germany leads / Netherlands highest AOV, and
18/18 cross-tool match. That's it — five numbers, not fifteen.

**Which finding demonstrates judgment:** the Laptop revenue-vs-margin
split (Section I) and the 99.88% repeat-rate caveat (Section L) — both
show you looked past the obvious headline number.

**Where to pause:** after stating the 18/18 cross-tool validation result —
let it land before moving on, since it's the strongest single credibility
signal in the project.

**Where not to over-explain:** don't narrate every SQL function or every
Excel sheet unless asked; name the tools and one representative technique
each, then wait for a follow-up.

**How to handle the Power BI question:** answer it directly and early if
it comes up — "I designed the full specification, but didn't have Power BI
Desktop to build it" — don't wait for it to be caught, and don't hedge.

**How to handle the synthetic-data question:** same approach — state it
plainly before being asked if the conversation heads that way, and pivot
immediately to why the workflow still demonstrates real analyst skills.

**How to finish strongly:** end on the recommendation (track margin and
order value alongside revenue) rather than trailing off on a limitation —
limitations are for when asked, the recommendation is the takeaway.

## Z. Memory Card

```
PROJECT         Sales Performance & Business Analytics
PROBLEM         Multi-country retailer needs revenue vs. profit clarity
DATA            9,985 synthetic orders, 5 products, 4 markets, 850 customers
TOOLS           Python, SQL, Excel, Power BI specification
KPI             Revenue €7.77M, Profit €2.73M, Margin 35.20%
KEY FINDING     Laptop leads revenue/profit, lowest margin (32.4%)
MARKET FINDING  Germany leads revenue/profit; Netherlands highest AOV
VALIDATION      18/18 metrics matched across Python, SQL, Excel
BUSINESS VALUE  Prioritize by margin + order value, not revenue alone
LIMITATION      Synthetic data; Power BI is a specification, not a build
```

## AA. 15-Second Backup

"It's a sales analytics project for a multi-country electronics retailer
where I built and cross-validated a KPI framework across Python, SQL, and
Excel, found that the top-revenue product actually has the lowest margin,
and turned that into a business recommendation."

## AB. Final 2-Minute Version

I built a sales analytics project for a fictional multi-country electronics
retailer selling five products — laptops, phones, tablets, monitors, and
keyboards — across Germany, Austria, France, and the Netherlands, using
about ten thousand synthetic transaction records. Raw transaction data
doesn't tell you which products and markets actually drive revenue versus
profit, so I built one KPI framework — revenue, profit, margin, average
order value — applied consistently across product, market, customer, and
time dimensions. I calculated every core number independently in Python,
in SQL, and again in a formula-driven Excel workbook, and checked eighteen
metrics across all three — they matched
exactly, which is the result I'm proudest of, because it means I can
defend these numbers, not just report them. I also designed a Power BI
data model and dashboard specification, but I want to be upfront that I
didn't have Power BI Desktop available to build it, so I verified that
logic in Python instead of claiming a dashboard that doesn't exist. The
clearest finding was that laptops drive half of total revenue and lead on
profit, but actually have the lowest margin of the five products, while
Germany leads on revenue but the Netherlands has the highest order value —
so revenue leadership and profitability leadership point to different
products and markets, which is why I'd recommend tracking margin and
order value alongside revenue rather than optimizing for revenue alone. I
also caught a very high repeat-purchase rate that turned out to
be an artifact of how the dataset was generated, not real customer
loyalty, and made
sure that didn't get reported as a business win. Overall, this project
shows I can take imperfect data, build KPIs I can trust across multiple
tools, and turn that into a recommendation a business could act on.
