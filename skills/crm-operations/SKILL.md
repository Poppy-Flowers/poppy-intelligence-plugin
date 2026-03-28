---
name: crm-operations
description: Query ActiveCampaign CRM data — contacts, deals, automations, campaigns, pipeline operations, stuck deals, and task queues. Use when asked about email performance, automation effectiveness, deal pipeline status, CRM contact history, or operational metrics.
---

# CRM Operations

Use this skill when the user asks about:
- Email campaign performance (open rates, click rates, engagement)
- Automation effectiveness and which emails need attention
- Contact CRM history (what emails they've received, automations they're in)
- Deal pipeline status, stuck deals, task queues
- Operational metrics across the CRM

## Available tools

### Contact-level queries (start here for a specific person)

- **`poppy_activecampaign_contact`** — Full contact record: profile, deal stage, automation progress, campaign sends. Use `identifier` (contact ID or email).

- **`poppy_activecampaign_contact_automation`** — Drill into a specific automation entry: timestamps, log timeline, send steps reached, campaign performance. Use `entry_id`.

### Deal queries

- **`poppy_activecampaign_deal`** — Deal detail: stage timeline with time in each stage, tasks, activities, notes. Use `deal_id`.

- **`poppy_activecampaign_deals`** — Search deals by title. Use `query` (search text), `limit`.

### Automation and campaign performance

- **`poppy_activecampaign_automation`** — Full automation report: block counts, all campaigns in the automation, engagement metrics. When asked about one email, this returns ALL emails in the automation for context. Use `automation_id`, optional `contact` filter.

- **`poppy_activecampaign_automations`** — List or search automations. Use `query`, `limit`.

- **`poppy_activecampaign_campaigns`** — Recent campaigns with open rate, click rate, click-to-open, bounces. Use `query`, `limit`.

- **`poppy_activecampaign_campaign`** — Single campaign detail. Use `campaign_id`.

### Operational dashboards (fast, Neon-backed)

- **`poppy_activecampaign_ops_summary`** — Pipeline overview: open deals, stuck deals, overdue tasks, active automation entries. Optional filters: `pipeline`, `assignee`, `days`.

- **`poppy_activecampaign_ops_stuck_deals`** — Deals stuck beyond threshold. Use `days` (default 7), optional `pipeline`, `stage`, `assignee`.

- **`poppy_activecampaign_ops_tasks`** — Task queue with overdue tracking. Use `status` (open/overdue/done/all), optional filters.

- **`poppy_activecampaign_ops_automation_entries`** — Active automation entries with contact and deal context. Use `status` (active/completed/all), optional `automation` filter.

### Discovery

- **`poppy_activecampaign_overview`** — Account inventory: total contacts, deals, automations, campaigns, pipelines.

- **`poppy_activecampaign_contacts`** — Search contacts by email or text. Use `query`, `limit`.

## Common patterns

### "How are our automations performing?"
1. `poppy_activecampaign_automations` — list all automations
2. For each automation of interest: `poppy_activecampaign_automation` with the ID
3. Compare open rates and click rates across emails within the same automation

### "What's happening with this lead?" (CRM perspective)
1. `poppy_activecampaign_contact` with their email — returns deal stage, automation progress, campaign receipts
2. If they have deals: `poppy_activecampaign_deal` for stage timeline and tasks

### "Which deals need attention?"
1. `poppy_activecampaign_ops_summary` — the full operational dashboard
2. `poppy_activecampaign_ops_stuck_deals` — drill into stuck deals
3. `poppy_activecampaign_ops_tasks` with `status: overdue` — check overdue tasks

### "How is this specific email performing?"
1. Find the automation: `poppy_activecampaign_automations` with the name
2. Get the full report: `poppy_activecampaign_automation` — returns ALL campaigns in the automation
3. Compare the target email against its siblings

## Key concepts
- **Automation**: A sequence of emails/actions triggered by a condition. Contains multiple campaigns.
- **Campaign**: A single email send with metrics (sends, opens, clicks, bounces).
- **Ops commands** use pre-materialized Neon data (fast). Other commands hit the AC API directly.
