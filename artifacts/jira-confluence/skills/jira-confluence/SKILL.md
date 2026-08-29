---
name: jira-confluence
description: Draft a Jira ticket or a Confluence page in Accurate Corp's house format — correct project/space key, required fields, severity scale, and page structure. Use when asked to file a ticket, write up a bug, or draft a runbook/design page, whether or not a live Jira/Confluence connection is available in this session.
---

# Jira & Confluence

This is a **drafting** skill, not a live API integration — it produces ticket/page content in the correct house format. If a Jira or Confluence connector is actually available in this session, use it to create the ticket/page for real with this content; if not, hand the draft back for the user to paste in themselves. Never claim a ticket or page was created unless a real tool call confirmed it.

Full conventions (severity scale, space/project keys, page tree) live in the `jira-confluence-conventions` instruction file — read it first if it's installed; the summary below is the minimum to draft correctly if it isn't.

## Drafting a Jira ticket

```
Project: PLAT (platform-owned) or PROD (customer-facing)
Type: Bug | Task | Story | Incident
Summary: [Sev2] <observed behavior, not the fix>
Severity: Sev1 (prod down/data loss) · Sev2 (core flow broken, no workaround) ·
          Sev3 (workaround exists) · Sev4 (cosmetic)
Environment: <affected version/environment>
Steps to reproduce: <numbered, or "not reproducible — see attached logs">
```

Justify the severity in one sentence rather than just stating it — "Sev2, no workaround" tells the next reader something "Sev2" alone doesn't.

## Drafting a Confluence page

- Space `PLAT`, under `Runbooks/` (operational — on-call reads this mid-incident) or `Design/` (why the system is shaped this way).
- Runbook pages lead with symptom → check → fix; background goes at the bottom.
- Title the thing itself: `Ingest Pipeline Runbook`, never `... (Updated Aug 2026)`.
- A postmortem page (`Runbooks/Postmortems/`) links its Jira `Incident` ticket and states the actual root cause — distinct from contributing factors.

## Example JQL, for when a live connector is available

- `project = PLAT AND status != Done AND priority in (Sev1, Sev2) ORDER BY created DESC` — the current high-severity queue.
- `project = PLAT AND summary ~ "<keyword>" AND created >= -30d` — a quick duplicate check before filing a new ticket, per the `issue-triage` agent's own step 3.
