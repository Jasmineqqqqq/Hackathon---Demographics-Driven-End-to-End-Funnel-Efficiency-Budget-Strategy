# Precision Spend: Demographic-Driven CPA Optimization for Social Ads

## Overview
This project analyzes paid-social campaign data to:
- Measure funnel efficiency — **impressions → clicks (CTR)** and **clicks → sales (Conversion Rate)**.
- Compare **cost efficiency** — **CPM** (₹/1k impressions), **CPC**, **CPA** (₹/sale).
- Benchmark performance across **age × gender** segments and campaigns.
- Recommend **budget reallocation** to lower blended CPA.
- Auto-generate a **12–15 slide deck** summarizing insights.

## Environment
- Python 3.9+  
- Libraries: `pandas`, `numpy`, `matplotlib`, `python-pptx`

```bash
pip install -U pandas numpy matplotlib python-pptx
```

## Data Fields (key)
- `Impressions`, `Clicks`, `Spent`, `Approved_Conversion` (renamed to `conversions`)
- Demographics: `age` (bands), `gender`; targeting: `interest`
- IDs: `xyz_campaign_id`, `fb_campaign_id`, `ad_id` (optional)

## KPI Definitions
- **CTR (%)** = Clicks / Impressions × 100  
- **Conversion Rate (CVR, %)** = Conversions / Clicks × 100  
- **CPM (₹/1k)** = Spent / Impressions × 1000  
- **CPC (₹/click)** = Spent / Clicks  
- **CPA (₹/sale)** = Spent / Conversions  
- **Sales per 1k Impressions** = (CTR% × CVR%) / 10  
- **Conversions per ₹1k Spend** = 1000 / CPA

> All metrics are computed on **aggregated totals** for correctness.

```

## Insights & Recommendations (from this dataset)
- **Costs rise with age:** both **CPA** and **CPM** increase from 30–34 to 45–49.  
- **Gender gap:** **M** cohorts are cheaper than **F** at the same age on CPA and CPM.  
- **Best segment:** **M 30–34** (lowest CPA & CPM).  
- **Worst segment:** **F 45–49** (highest CPA & CPM).  
- **Funnel behavior:** CTR tends to increase with age, but **CVR declines**; older cohorts click more but buy less → higher CPA.  
- **Budget rule (data-only):** allocate share ∝ **1/CPA**; rebalance weekly and monitor **marginal CPA** as you scale.

## Tools / Libraries
- Python, pandas, numpy, matplotlib, python-pptx  
- (Jupyter) Notebook workflow for EDA and reporting

## Known Challenges
- Sparse conversions can make CPA volatile; ensure minimum volume before decisions.  
- Aggregation vs. row averages (avoid Simpson’s paradox).  
- No revenue/LTV → CPA-only view; ROAS not computed.  
- Attribution limits (single conversion field).

## Repro Tips
- Ensure column names match (`Approved_Conversion → conversions`).  
- Compute metrics on **aggregated totals** and use safe division.  
- Lock age order for pretty pivots: `['30-34','35-39','40-44','45-49']`.
