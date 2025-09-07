What the Analysis Covers
1) Funnel Effectiveness (Campaign-level)

Aggregate by xyz_campaign_id and compute CTR and CVR (safe division).

Rank campaigns by:

CTR (%)

Conversion Rate (%)

Sales per 1k impressions = (CTR × CVR)/10


2) Demographic Performance (Age × Gender)

Aggregate by ['age','gender'] and compute CTR, CVR, CPM, CPC, CPA.

Build pivots for stakeholder-friendly views and bar charts with hue.


3) Facebook Campaigns & Pair View

Mirror the campaign analysis by fb_campaign_id.

Build a pair table for (fb_campaign_id × xyz_campaign_id) and rank combinations by end-to-end efficiency.



Key Insights (from this dataset)

Costs rise with age: both CPA and CPM increase from 30–34 → 45–49.

Gender gap: male cohorts are cheaper than female cohorts (same age) on CPA and CPM.

Best segment: Male 30–34 — lowest CPA & CPM.

Worst segment: Female 45–49 — highest CPA & CPM.

Funnel behavior: CTR tends to rise with age, but CVR declines; older cohorts click more but convert worse → higher CPA.

Budget move: shift spend toward the most efficient segments (M 30–34, then F 30–34, M 35–39), constrain high-cost cohorts unless LTV justifies.




⚠️ Assumptions & Limitations

Approved_Conversion ≈ final sale; revenue/LTV not provided (no ROAS).

Metrics computed on aggregated totals; safe division with NaN for zero denominators.

No multi-touch attribution; results reflect last-touch in the file.

Performance across demographics may be confounded by creative/offer differences.

