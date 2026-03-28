---
name: performance-marketing
description: Analyze Google Ads and Meta Ads performance — CPL, search term waste, keyword quality, campaign breakdowns, ad creative performance, and cross-platform comparisons. Use when asked about ad performance, marketing spend, which ads are working, or what search terms to add/remove.
---

# Performance Marketing

Use this skill when the user asks about:
- Google Ads or Meta Ads performance (CPL, spend, leads, clicks)
- Which search terms are wasting money or converting well
- Keyword quality scores and optimization opportunities
- Campaign, ad set, or ad-level performance breakdowns
- Cross-platform comparisons (Google vs Meta)
- Which creative or ad copy is working best

## Available tools

### Google Ads

- **`poppy_google_ads_overview`** — Account health: data freshness, spend, leads, CPL, low quality keywords, top waste search terms. Start here for a quick pulse check. Optional `days` (default 30).

- **`poppy_google_ads_search_terms`** — Search query report with 6-month validated waste classification. Shows what people actually searched for, whether it converted, and spend. Use `days`, optional `campaign` filter, `limit`.

- **`poppy_google_ads_keywords`** — Keyword performance with quality score, match type, bid. Use to find low-QS keywords costing money. Use `days`, optional `campaign` filter, `limit`.

- **`poppy_google_ads_campaigns`** — Campaign performance: spend, clicks, leads, CPL, bidding strategy. Use `days`.

- **`poppy_google_ads_ads`** — Ad performance with RSA headline/description parsing. Shows which ad copy is working. Use `days`, optional `campaign` filter, `limit`.

- **`poppy_google_ads_correlate`** — Detect keyword/campaign status changes and correlate with performance shifts. Use `days` (default 60) for change detection window.

### Meta Ads

- **`poppy_meta_ads_overview`** — Account health: freshness, spend, leads, CPL, quality distribution. Start here. Optional `days`, `action_type`.

- **`poppy_meta_ads_campaigns`** — Campaign performance: spend, clicks, leads, CPL, frequency. Use `days`, optional `action_type`.

- **`poppy_meta_ads_adsets`** — Ad set performance with campaign context. Use `days`, optional `campaign` filter, `action_type`, `limit`.

- **`poppy_meta_ads_ads`** — Ad performance with creative details and quality rankings. Use `days`, optional `campaign` filter, `action_type`, `limit`.

- **`poppy_meta_ads_platforms`** — Performance breakdown by platform (Facebook vs Instagram) and placement. Use `days`.

## Common patterns

### "How are our ads performing?"
1. `poppy_google_ads_overview` + `poppy_meta_ads_overview` — side-by-side health check
2. Compare CPL, spend, and lead volume across platforms

### "Which search terms are wasting money?"
1. `poppy_google_ads_search_terms` with `days: 30` — look for waste-classified terms
2. Terms with spend > $0 and zero leads in 6 months are candidates for negative keywords

### "What ads should we make more of?"
1. `poppy_google_ads_ads` — find top-performing ad copy by CPL and CTR
2. `poppy_meta_ads_ads` — find top-performing creative by CPL and engagement
3. Cross-reference: what themes/messages appear in the best performers?

### "How is Meta performing vs Google?"
1. Call both overview tools with the same `days` window
2. Compare: CPL, total spend, total leads, trend direction

### "What changed recently that might explain a CPL spike?"
1. `poppy_google_ads_correlate` — detects keyword status changes, campaign changes correlated with performance shifts

## Key terminology
- **CPL** = Cost Per Lead (not CPA). Leads are tracked, not generic conversions.
- **Waste classification**: search terms are classified as "waste" if they had spend but zero leads over a 6-month lookback window.
- **Quality score** (Google only): 1-10 rating. Keywords below 5 are flagged.
