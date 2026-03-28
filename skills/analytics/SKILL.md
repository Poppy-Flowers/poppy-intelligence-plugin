---
name: analytics
description: GA4 web analytics — website traffic, user behavior, traffic sources, page performance, quiz funnel conversion, and campaign attribution. Use when asked about website traffic, which pages are performing, where visitors come from, or how the quiz funnel converts.
---

# Web Analytics (GA4)

Use this skill when the user asks about:
- Website traffic and trends (sessions, users, pageviews)
- Traffic sources and channels (organic, paid, social, LLM/AI referrals)
- Page-level performance (which pages get traffic, engagement time)
- Quiz funnel conversion rates (step-by-step drop-off)
- Campaign attribution from the GA4 perspective
- LLM and AI referral traffic patterns

## Available tools

- **`poppy_ga4_overview`** — Site health dashboard: sessions, users, key events, channel breakdown, daily trend. Start here for a pulse check. Use `days` (default 30).

- **`poppy_ga4_events`** — Event analysis with quiz funnel visualization and step-to-step conversion rates. Shows all tracked events by volume. Use `days`, optional `event` for a single event's daily trend.

- **`poppy_ga4_sources`** — Traffic source analysis with LLM identification and key event conversion rate. Use `days`, `llm: true` for AI-only traffic, `channel: true` to group by channel instead of source/medium.

- **`poppy_ga4_pages`** — Page performance: views, users, key events, engagement time. Use `days`, optional `path` prefix filter (e.g. "/help"), `limit`.

- **`poppy_ga4_campaigns`** — Campaign-level traffic from GA4 perspective, cross-referenceable with ad platform data. Use `days`, optional `campaign` name filter, `limit`.

## Common patterns

### "How's our website traffic?"
1. `poppy_ga4_overview` — sessions, users, key events, channel breakdown
2. Look at the daily trend for anomalies (spikes or drops)

### "Where's our traffic coming from?"
1. `poppy_ga4_sources` — full source/medium breakdown with conversion rates
2. For channel-level view: `poppy_ga4_sources` with `channel: true`
3. For AI/LLM referrals specifically: `poppy_ga4_sources` with `llm: true`

### "How is the quiz funnel converting?"
1. `poppy_ga4_events` — shows all events including quiz steps
2. The quiz funnel visualization shows step-to-step conversion rates

### "Which pages are performing best?"
1. `poppy_ga4_pages` — ranked by views with engagement metrics
2. Filter by section: `poppy_ga4_pages` with `path: "/help"` or `path: "/weddings"`

### "Are our ad campaigns driving real traffic?"
1. `poppy_ga4_campaigns` — GA4's view of campaign traffic
2. Cross-reference with `poppy_google_ads_campaigns` or `poppy_meta_ads_campaigns` (from performance-marketing skill) to compare ad platform reporting vs GA4 attribution

### "Are we getting traffic from AI/ChatGPT?"
1. `poppy_ga4_sources` with `llm: true` — shows all identified AI referral sources with monthly trend

## Key concepts
- **Key events**: GA4's term for conversions (e.g., quiz completions, form submissions)
- **Engagement time**: How long users actively interact with the page (not just time-on-page)
- **LLM traffic**: Referrals identified as coming from AI assistants (ChatGPT, Claude, Perplexity, etc.)
