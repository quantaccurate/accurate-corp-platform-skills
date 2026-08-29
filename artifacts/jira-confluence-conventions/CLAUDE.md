## Jira & Confluence conventions

**Jira**

- Project key: `PLAT` for platform-owned services, `PROD` for customer-facing product work. Pick the key by who owns the fix, not who reported it.
- Issue types: `Bug`, `Task`, `Story`, `Incident` (only for a live production event — closing it requires a linked postmortem page).
- Severity scale (put it in the summary line, e.g. `[Sev2] ...`): **Sev1** — production down or data loss, page on-call immediately. **Sev2** — a core flow broken for some users, no safe workaround, fix this sprint. **Sev3** — broken but has a workaround, or affects a non-core flow. **Sev4** — cosmetic, or a "would be nice."
- Every ticket needs: a one-line summary stating the observed behavior (not the fix), steps to reproduce (or "not reproducible, see attached logs"), and the affected environment/version.
- Link the PR that fixes a ticket in the ticket, and reference the ticket key in the PR description (`PLAT-1234`) — not just the branch name.

**Confluence**

- Space key: `PLAT`. Two top-level trees only — `Runbooks/` (operational: what to do when X breaks, owned by whoever's on call, kept current or it's worse than nothing) and `Design/` (why a system is shaped the way it is, written once, revised on real architecture changes, not on every PR).
- Page titles are the thing itself, not a status: `Ingest Pipeline Runbook`, not `Ingest Pipeline Runbook (Updated Aug 2026)` — page history already tracks that.
- A runbook page opens with the on-call-relevant part first: symptom → check → fix. Background and rationale go at the bottom, not the top — nobody mid-incident reads past the third paragraph.
- Every incident's postmortem page lives under `Runbooks/Postmortems/`, links back to its Jira `Incident` ticket, and states the actual root cause distinctly from any contributing factors — "the deploy happened at a bad time" is a contributing factor, not a root cause.
