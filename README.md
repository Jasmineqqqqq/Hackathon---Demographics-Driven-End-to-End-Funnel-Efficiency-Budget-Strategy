🧭 What the Analysis Covers
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

4) Underperformers (Data-Driven)

Flag campaigns with CPA > 75th percentile or CVR < 25th percentile, among those with ≥ median spend.

Produce a short list for fix / cut / reallocate actions.



🧠 Key Insights (from this dataset)

Costs rise with age: both CPA and CPM increase from 30–34 → 45–49.

Gender gap: male cohorts are cheaper than female cohorts (same age) on CPA and CPM.

Best segment: Male 30–34 — lowest CPA & CPM.

Worst segment: Female 45–49 — highest CPA & CPM.

Funnel behavior: CTR tends to rise with age, but CVR declines; older cohorts click more but convert worse → higher CPA.

Budget move: shift spend toward the most efficient segments (M 30–34, then F 30–34, M 35–39), constrain high-cost cohorts unless LTV justifies.

🧾 Reproducible Snippets
Rename & aggregate safely
df = pd.read_csv("KAG_conversion_data_raw.csv")
df.rename(columns={'Approved_Conversion': 'conversions'}, inplace=True)

agg_demo = (df.groupby(['age','gender'], as_index=False)
              .agg(impressions=('Impressions','sum'),
                   clicks=('Clicks','sum'),
                   conversions=('conversions','sum'),
                   spent=('Spent','sum')))

agg_demo['CTR'] = agg_demo['clicks']/agg_demo['impressions']*100
agg_demo['ConversionRate'] = agg_demo['conversions']/agg_demo['clicks']*100
agg_demo['CPM'] = agg_demo['spent']/agg_demo['impressions']*1000
agg_demo['CPC'] = agg_demo['spent']/agg_demo['clicks']
agg_demo['CPA'] = agg_demo['spent']/agg_demo['conversions']

Campaign funnel & ranking
agg_camp = (df.groupby('xyz_campaign_id', as_index=False)
             .agg(impressions=('Impressions','sum'),
                  clicks=('Clicks','sum'),
                  conversions=('conversions','sum')))

agg_camp['CTR'] = agg_camp['clicks']/agg_camp['impressions']*100
agg_camp['ConversionRate'] = agg_camp['conversions']/agg_camp['clicks']*100
agg_camp['Conv_per_1k_Impr'] = (agg_camp['CTR']*agg_camp['ConversionRate'])/10.0

agg_camp.sort_values('Conv_per_1k_Impr', ascending=False).head(5)


⚠️ Assumptions & Limitations

Approved_Conversion ≈ final sale; revenue/LTV not provided (no ROAS).

Metrics computed on aggregated totals; safe division with NaN for zero denominators.

No multi-touch attribution; results reflect last-touch in the file.

Performance across demographics may be confounded by creative/offer differences.

