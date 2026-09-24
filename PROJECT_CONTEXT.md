# CustomerPulse — Project Context

## One-Line Project Statement
CustomerPulse is a customer revenue and retention analytics project that analyzes real e-commerce transactions and uses RFM analysis to identify high-value, loyal, inactive, and at-risk customer groups.

## Main Business Question
Which customers drive business value, which customers show signs of inactivity, and where should the company focus retention and revenue-growth efforts?

## Dataset
UCI Online Retail dataset:
- 541,909 transaction records
- UK-based non-store retailer
- Time period: 01-Dec-2010 to 09-Dec-2011
- Main fields: InvoiceNo, StockCode, Description, Quantity, InvoiceDate, UnitPrice, CustomerID, Country

## Analytical Story
Raw Transactions
→ Data Cleaning
→ Revenue Feature Engineering
→ Executive KPIs
→ Revenue Trends
→ Customer Behaviour
→ RFM Metrics
→ Customer Segments
→ Risk / Opportunity
→ Business Recommendations

## Key Questions
1. How much revenue did the business generate?
2. How many unique orders and customers are present?
3. How does revenue change month by month?
4. Which countries, products and customers generate the most revenue?
5. What percentage of customers make repeat purchases?
6. Which customers are the most valuable?
7. Which valuable customers have not purchased recently?
8. How much revenue comes from each RFM segment?
9. What retention actions should the business prioritize?

## Data Cleaning Rules
The notebook should explicitly document each rule rather than silently deleting data.

Recommended rules:
- Convert InvoiceDate to datetime.
- Remove exact duplicate rows.
- Treat InvoiceNo beginning with `C` as cancellation records.
- For core completed-sales analysis, exclude cancelled transactions.
- Exclude Quantity <= 0 from completed-sales revenue.
- Exclude UnitPrice <= 0 from completed-sales revenue.
- Exclude missing CustomerID from customer-level RFM analysis.
- Keep a count of how many rows are removed at each step.
- Create Revenue = Quantity * UnitPrice.

## KPI Definitions
- Total Revenue = sum of Revenue for valid completed transactions.
- Total Orders = number of unique valid InvoiceNo values.
- Unique Customers = number of unique valid CustomerID values.
- Average Order Value = Total Revenue / Total Orders.
- Revenue per Customer = Total Revenue / Unique Customers.
- Repeat Customer Rate = customers with >1 order / total customers.
- Cancellation Rate = cancelled invoice count / total unique invoice count.

## RFM Definitions
Use an analysis date one day after the latest valid transaction date.

Recency:
analysis_date - customer's latest InvoiceDate

Frequency:
number of unique valid InvoiceNo values per customer

Monetary:
sum of Revenue per customer

## RFM Scoring
Use quantile-based scoring where practical:
- Recency: lower is better, so reverse the score.
- Frequency: higher is better.
- Monetary: higher is better.

Start with quartiles (1–4). If duplicated quantile edges appear, use rank-based quantiles.

## Segment Logic
Keep the first version simple and explainable.

Suggested segments:
- Champions: very recent + frequent + high-spending
- Loyal Customers: strong frequency with good recency
- Potential Loyalists: recent customers with moderate frequency/value
- Needs Attention: mid-value customers whose recency is weakening
- At Risk: previously valuable/frequent customers with poor recency
- Hibernating/Lost: low engagement and long inactivity

The exact rule table should be shown in the notebook before assigning segments.

## Minimum Visuals
1. Monthly Revenue Trend
2. Top 10 Countries by Revenue
3. Top 10 Products by Revenue
4. Top 10 Customers by Revenue
5. Repeat vs One-Time Customer Distribution
6. RFM Segment Distribution
7. Revenue by RFM Segment
8. Recency vs Monetary scatterplot (optional if time allows)

## Strong Final Insights Format
For each major finding use:

Observation:
What does the data show?

Business Meaning:
Why does it matter?

Action:
What should the business do?

## Final Recommendations
Recommendations must be derived from actual notebook results, not written in advance.

Potential action types:
- VIP retention campaign for Champions
- Win-back campaign for high-value At-Risk customers
- Second-purchase incentive for new/one-time customers
- Prioritize inventory/marketing around consistently high-revenue products
- Investigate customer concentration risk if a small group drives excessive revenue

## Scope Guardrails
Do NOT add machine learning just to make the project look complex.
Do NOT claim churn prediction because there is no labelled churn target.
Do NOT call RFM segments predictive.
Do NOT invent business outcomes from recommendations.
Do NOT hard-code conclusions before running the dataset.

## Resume Bullet — Draft
Analyzed 500K+ e-commerce transactions using Python/Pandas and RFM segmentation to evaluate customer value, repeat purchasing, revenue concentration, and retention opportunities; translated behavioral segments into actionable business recommendations.

Replace/expand the numerical claims only after the final notebook results are verified.

## Future Version 2
After the submission version is complete:
- Recreate KPI queries in SQL
- Build a Power BI executive dashboard
- Add cohort retention analysis
- Add customer lifetime value analysis
- Add ABC/Pareto customer concentration analysis
