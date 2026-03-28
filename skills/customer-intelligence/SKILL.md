---
name: customer-intelligence
description: Look up leads, check deal status, find stale or engaged leads, and view full customer evidence packets. Use when asked about a specific lead, deal, or proposal, or when asked to find leads matching criteria like "who needs follow-up" or "show me hot leads."
---

# Customer Intelligence

Use this skill when the user asks about:
- A specific lead or deal (by email, deal ID, or name)
- Proposal status and activity
- Finding leads that need follow-up (stale, engaged, missing phone)
- Full customer story with evidence from sales consultations
- Activity timelines for a deal

## Available tools

All data is accessed through the `poppy-data` MCP server tools.

### Customer-level queries (start here for a specific person)

- **`poppy_customer_packet`** — Full customer evidence packet: multi-source aggregation with provenance, quality scoring, and freshness. Returns contact info, CRM stage, milestones, proposal state, VOC transcript insights, and more. Use `identifier` (event ID or deal ID).

- **`poppy_lead_lookup`** — Quick lead snapshot: CRM stage, proposal status, milestones, recent activity. Faster than customer packet but less comprehensive. Use `identifier` (email or deal ID).

- **`poppy_lead_timeline`** — Chronological event log: portal activity, emails, comments for a deal. Use `deal_id`.

### Cohort queries (finding groups of leads)

- **`poppy_leads_stale`** — Engaged leads gone cold (no activity for N days). Use `days` (default 7) and optionally `min_budget`.

- **`poppy_leads_engaged`** — Hot leads with recent portal activity. Use `days` (default 7).

- **`poppy_leads_no_phone`** — Leads without phone numbers. Optionally filter by `source` and `days`.

## Common patterns

### "What's happening with this lead?"
1. Use `poppy_lead_lookup` with their email or deal ID for a quick snapshot
2. If you need the full story (VOC insights, all evidence sources): use `poppy_customer_packet`
3. For CRM/email perspective: also check `poppy_ac_contact` (from crm-operations skill)

### "Which leads need follow-up?"
1. `poppy_leads_stale` with `days: 5` — engaged leads gone cold
2. `poppy_leads_engaged` with `days: 3` — hot leads to capitalize on

### "Show me the full activity history"
1. `poppy_lead_timeline` with the deal ID — portal activity, emails, comments in chronological order

## Data source notes
- Lead lookup queries the DW (nightly: CRM stage, milestones, budget) and prod DB (real-time: proposal audits)
- Customer packet aggregates from Neon/VOC, Customer API, and prod DB
- Cohort queries join DW and prod DB
- If a data source is unavailable, the response includes degradation info
