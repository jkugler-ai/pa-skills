---
name: mercedes-benz-tpm
description: Customer TPM profile for Mercedes-Benz. Defines workstream boundary, artifacts, reporting configuration, people, and confidentiality for Mercedes-Benz engagement.
---

# Mercedes-Benz — Customer TPM Profile

## Identity and boundary

- Customer: Mercedes-Benz
- Product: Omniverse on DGX Cloud (OV-on-DGXC)
- Workstream: Planning for cars production in digital twin — large-scale factory visualization, large-scale car variants switch, collision checks — operating across cloud and on-prem, multi-user and third-party collaboration
- Explicitly separate workstreams: (none defined)
- Customer outcome / goal: Digital-twin-based production planning with large-scale factory visualization, variant switching, collision checks, multi-user and third-party collaboration across cloud and on-prem

## Primary artifacts

- Source-of-truth tracker and exact tab: [Customer Execution Health - BMW & MB - Q3-4 2026](https://docs.google.com/presentation/d/1nNDwi0-RUWvpmOnHzKh12gSP1JYzzT4pDfR0HwYrnww/edit) — Mercedes-Benz slides (most recent first; archive after slide 6)
- Customer plan of record:
- Executive deck or report location: Same as tracker
- Release-record system:
- Ticket systems: NVBugs, Jira (jirasw.nvidia.com)
- Relevant discussion sources:
- Metrics source: Drew Como weekly Slack metrics post in channel `C0984Q3GTU3` on Fridays; use the latest Friday metrics post as the current usage snapshot when available. Example thread pattern: `https://nvidia.slack.com/archives/C0984Q3GTU3/p1789998253641559`
- Bug source: Omniverse Customer Command Center customer page for Mercedes-Benz — `https://customer-success.nvidia.com/#customers:Mercedes%20Benz`
- Required bug columns for reporting: bug ID, type (Bug/FR), priority, synopsis, dev team, assignee, fix version, days open, last modified, **waiting on** (must be one of: "Customer" or "Dev" — derive from bugaction + context: if the bug needs customer-provided data/trace/repro/confirmation use "Customer"; if dev is investigating/fixing/triaging use "Dev"; if unclear default to "Dev" and flag for TPM review)

## Historical milestone context — refresh from the latest slide before reporting

- ~~(September) Use of OV as main vehicle for Board of Management presentation~~ — historical profile entry; excluded from current report at user request October15. Completion was not verified.
- (October) Workshop with Shopping Cart application (highly visible across multiple teams)
- (~November) Customer rolling out 'external' access to their application (via OVC) to their suppliers for collaboration purposes

## Known tracked tickets

### Source of truth: the CCC customer page
The CCC customer page (https://customer-success.nvidia.com/#customers:Mercedes%20Benz)
is what leadership looks at. The Execution Health report MUST match what that
page shows — same bug count, same FR count. If the report and the page
disagree, leadership will flag it.

### NVBugs — cross-check to catch CCC API gaps
The CCC `all_open?customer=` API filter is unreliable — it returns fewer bugs
than the CCC frontend page. Always supplement the CCC API pull by fetching
ALL known tracked bug IDs below directly from NVBugs (nvbugs_get_bugs_list).
Merge into the CCC results by bug ID — NVBugs is authoritative for
status/action. Include any bug that is still open in NVBugs even if the CCC
API didn't return it. If the merged count still doesn't match the CCC page,
flag the discrepancy in the report with a ⚠️ note so the TPM can reconcile
before sending.

- b/5865219 — 'Hall 32' content-specific performance issue (P0, open 6+ months) — PIC: Ignacio, Kevin C
- b/6643207 — OVC session termination + auth errors; Portal 1.7.0 blocked by NVCF (P1)
- b/6829676 — IDLE session status inaccurate → usability issues (P1)
- b/6829391 — NVCF failure to assign instances for new function (P1)
- b/6828867 — Portal "Failed" session status misapplied (P1)
- b/6397097 — Stream pixelated during VPN usage (P1)
- b/6396729 — Camera continues stale navigation after VPN packet loss (P1)
- b/6629273 — FR: Continue an interrupted render on the next session (P1, 6-Enhancement)
- b/6435447 — LLS / session disconnection issue; Portal 1.7.0 blocked by NVCF (verify if closed)
- b/5512887 — NVCF and Web Portal session status tracking improvements (verify if closed)
- b/6604881 — GPU overprovisioning causing session disconnections (showstopper — Closed & Verified 09/19)

### Jira FRs — shown on CCC page but not in CCC API
The CCC page shows these as MB feature requests but they live in Jira, not
NVBugs. The CCC `all-features/queue` endpoint does NOT return them. Always
fetch live status via Jira MCP (jira_get_issue) — populate the same columns
as NVBugs rows (priority, assignee, status, fix version, last modified).
Only fall back to "⚠️ Jira unavailable — verify manually" if the Jira MCP
returns a 403/5xx error. Never show "Jira — verify" as a status when the
data is actually available.

- OMPE-94258 — Visually compare point clouds vs. 3D data / 3D data vs. 3D data
- OMPE-77461 — Storage API - Live Sync (target Kit 111.0)
- NVCF-11413 — Feature request (Jira)
- NVCF-11412 — Feature request (Jira)

## Awareness items

- Geometry Streaming and Render Instancing need to graduate from experimental to production — customer's production application is entirely reliant on these
- NVCF 'IDLE' status desync causing usability issues; waiting for customer-filed support case and session logs

## Reporting configuration

- Cadence: Weekly (slides updated each week)
- Health vocabulary: 🟢 Green / 🟡 Yellow / 🔴 Red + Trending indicator
- Priority source: Slide deck (currently P1)
- Stack-rank source: Slide deck (currently 103)
- Branding / wordmark: Mercedes-Benz
- Required sections or presentation decisions: Current State, Blockers / Critical Path, Key Actions, Roadmap, Special Topics, Summary; production week-over-week usage table on companion slide
- Cluster: AZ25-PRD1
- **Metrics table headers:** Use full words — "Last Week", "This Week", "Week-over-Week". Never use abbreviations like "Last", "This", "WoW".
- **Report content rule:** The email body that goes to leadership must contain ONLY the polished report — no internal notes, data-source disclaimers, CCC-vs-API commentary, Jira-unavailable warnings, or automation debug info. Any such notes (metrics placeholders to fill, CCC count mismatches, Jira auth failures, items needing TPM review) go in a **"⚠️ TPM Notes — delete before sending"** section at the very top of the draft, above the dark header bar, clearly separated. The TPM reviews and removes that section before forwarding to the distribution list.
- **Status pills rule:** Overall status, Trending, Priority, and Stack Rank MUST be read from the current slide in the tracker deck — never inferred or computed by the agent. If the slide says Trending 🟡, the report says 🟡. If the values cannot be read, flag in TPM Notes.
- **"What Changed" baseline rule:** The "What Changed" section compares the CURRENT slide to the PREVIOUS slide in the tracker deck (i.e. the slide immediately after in the archive). Do NOT reference the `last report as-of date` from this profile for this purpose — that field tracks the last email sent, not the slide baseline. Only surface changes visible between those two consecutive slides plus any NVBugs/Jira status changes that occurred in that window.

## People and distribution

- CS: Johnny Costello (jcostello@nvidia.com)
- TAM: Sam Corcoran (scorcoran@nvidia.com)
- CPM: Anastasia Mamaev (amamaev@nvidia.com)
- PM: Drew Como (dcomo@nvidia.com), Raphael Boehm (rboehm@nvidia.com)
- TPM: Jen Kugler (jkugler@nvidia.com), Harald Koebler (hkoebler@nvidia.com)
- Other workstream PICs: Ignacio (b/5865219 perf PIC), Kevin C (b/5865219 PIC)
- Workstream PICs line for report header: CS: Johnny Costello | TAM: Sam Corcoran | CPM: Anastasia Mamaev | PM: Drew Como, Raphael Boehm | TPM: Jen Kugler, Harald Koebler
- To distribution: ov-leadership@exchange.nvidia.com, omniverse-product-management@exchange.nvidia.com, ov-tpms@exchange.nvidia.com, omniverse-dev@exchange.nvidia.com, omniverse-qa-team@exchange.nvidia.com
- CC distribution: mabourizk@nvidia.com, mgeyer@nvidia.com, dcomo@nvidia.com, dfagnou@nvidia.com, azoellner@nvidia.com, mdevlin@nvidia.com, djohnston@nvidia.com, amamaev@nvidia.com, scorcoran@nvidia.com, jcostello@nvidia.com, hkoebler@nvidia.com

## Persistent report state

- last sent Execution Health timestamp and subject: 2026-09-04T16:19:50-04:00 | "2026-09-04 | Mercedes-Benz Execution Health | Engineering/Product Perspective"
- historical stored report as-of date: Sept 16, 2026 — not the current reporting period; do not carry this date or its milestones into a new report.
- current editable artifact location: Slide 4 in tracker deck
- previous issue-appendix cutoff: 2026-09-04T16:19:50-04:00
- known source discrepancies that must be rechecked: NVBugs Query #200293946; Anastasia flagged ~5 out-of-scope AV tickets in bug list — review needed before next send

## Confidentiality

- Sources permitted in leadership reports:
- Sources permitted in customer-visible reports:
- Private sources that may inform understanding but must not be linked:
