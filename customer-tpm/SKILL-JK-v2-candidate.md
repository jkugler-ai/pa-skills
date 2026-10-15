---
name: customer-tpm
description: Operate customer-facing product TPM work with a source-of-truth tracker, evidence-backed execution health, recurring executive reports, and customer meeting readiness. Use when tracking a named customer or workstream, generating an Execution Health report, preparing a customer update, or maintaining actions, decisions, owners, milestones, and validation state.
---

# Customer TPM

Use this skill to turn live customer, product, engineering, release, and validation evidence into a concise management view. The user's current direction and the live systems of record remain authoritative.

## Customer profile routing

Identify the exact customer, product, and workstream first. Keep independently managed workstreams separate.

Look for an installed companion profile named `<customer-slug>-tpm` under `<skills-root>`. If one exists, read its `SKILL.md` and required references before acting. A profile may define tracker locations, source systems, PICs, distribution, confidentiality boundaries, presentation decisions, and **email distribution lists (To/CC)**. Treat dates, people, ticket states, release availability, priority, and rank in a profile as routing context that must be refreshed when material.

If no profile exists, proceed from live sources and use [references/customer-profile-template.md](references/customer-profile-template.md) to identify missing configuration. Do not create or persist a profile unless the user asks.

## Operating modes

- For tracker creation, refresh, or issue review, read [references/operating-expectations.md](references/operating-expectations.md).
- For an Execution Health report, read [references/execution-health-report.md](references/execution-health-report.md) and start from [assets/execution-health-template.html](assets/execution-health-template.html) when rich HTML is appropriate.
- For an Outlook draft, also read [references/outlook-execution-health-draft.md](references/outlook-execution-health-draft.md).
- **For customer meeting preparation**, read the latest report + bugs updated in the last 48 hours + recent Slack threads mentioning the customer, and produce a briefing doc with talking points, open risks, and any bugs requiring customer input.

## Pre-generation checklist

Before generating any Execution Health report, confirm each source is loaded or its gap is noted:

- [ ] Slides read — **current week AND previous week** (for delta computation)
- [ ] Customer Command Center bugs pulled (`/api/all_open`) — or fallback noted
- [ ] Customer Command Center FRs pulled (`/api/all-features/queue`) — or fallback noted
- [ ] NVBugs enrichment done (`nvbugs_get_bugs_list`) — or fallback noted
- [ ] Metrics slide read (slide immediately following each customer's main slide) — or gap noted
- [ ] Delta from previous week computed (What Changed section)

## Metrics and bug-source addendum

When a customer profile defines metrics and bug sources, incorporate them explicitly into the refresh workflow:

- Metrics: pull the weekly customer-usage metrics from the **metrics slide** in the tracker deck. Each customer's main execution-health slide is followed by a metrics slide (e.g., BMW slide 2 → metrics slide 3; MB slide 4 → metrics slide 5). Extract the session-length table and any week-over-week usage charts from that slide. If the metrics slide data is blank or missing, note "Metrics unavailable this week" in the report.
- Bugs: pull the current customer bug list from the designated customer-success source (Customer Command Center).
- For each bug, normalize the management view to include at minimum: bug ID, priority, assignee, dev team, days open, version fixed in, last modified date, and status.
- Treat tracker slides and Customer Command Center bug lists as separate evidence streams. Reconcile discrepancies instead of silently preferring one.
- When the metrics slide or bug source is temporarily unavailable, state the gap clearly in the report and continue with the other evidence that was successfully refreshed.

## Bug and feature-request data enrichment

After pulling bugs/FRs from the Customer Command Center, cross-reference them with NVBugs to fill in fields that the Customer Command Center does not reliably populate:

**Customer Command Center API access:** The Customer Command Center (`customer-success.nvidia.com`) uses a self-signed SSL certificate. Always use `primitive--bash` with `curl -sk` (skip certificate verification) for Customer Command Center API calls. Do not use `primitive--http`, which enforces strict SSL and will fail.

1. Collect all bug IDs from the Customer Command Center `/api/all_open` (bugs) and `/api/all-features/queue` (FRs) responses.
2. Merge and deduplicate by bugid across both Customer Command Center endpoints (items with severity "6-Enhancement" can appear in both).
3. Call `nvbugs_get_bugs_list` with the deduplicated bug IDs to retrieve the authoritative NVBugs record for each item.
4. Enrich the Customer Command Center data with NVBugs fields, in particular:
   - **Fix Version** (`VersionFixedAfter` / `FixForReleaseVersion`) — Customer Command Center rarely populates this.
   - **Assignee** (`Engineer`) — use the NVBugs engineer when Customer Command Center's is blank.
   - **Dev Team** (`Categories` / `ModuleInfo`) — cross-check with Customer Command Center.
5. Define "open items" as those whose `bugaction` does **not** contain "Closed".
6. When NVBugs is unavailable or times out, fall back to Customer Command Center's `version` and `target_release` fields and note the gap.

### Jira cross-reference

When a bug has a `linked_jira_key`, pull the Jira ticket status. If NVBugs and Jira statuses are out of sync (e.g., NVBugs says "To fix" but Jira says "Done"), flag it in the status column with: **"⚠️ Jira: Done"** (or the relevant Jira status).

### NVBugs batch timeout handling

If `nvbugs_get_bugs_list` times out on a large set, chunk into batches of 15 and retry. If still failing after retries, use Customer Command Center-only data and note the gap: *"NVBugs enrichment unavailable — Fix Version, Assignee, and Status may be incomplete."*

### Customer Command Center API fallback

When the Customer Command Center API is unreachable (SSL error, timeout, 5xx), carry forward the previous week's bug table with days-open incremented by 7. Insert a visible note in the report:
> ⚠️ Bug data carried forward from [previous date] — verify against live Customer Command Center before sending.

## Bug table presentation

- The bug/FR table section heading must be: **"Open Bugs and Feature Requests (N open: X bugs + Y FRs)"**
- Each row must include: bug ID (linked), type (Bug/FR), priority, synopsis, assignee, dev team, fix version, days open, last modified, and status.
- Bug reports should include the bug, priority, assignee, development team, and days open.
- **Status column — "Provide detail" clarification:** When a bug's status is "Provide detail" (or equivalent "Needs info"), determine *who* needs to provide detail by inspecting the NVBugs `bugaction` field and the most recent comments:
  - If the ball is in NVIDIA's court (dev/engineer needs to investigate or respond), display: **"Provide detail (Dev)"**
  - If the ball is in the customer's court (customer needs to supply info, logs, scenes, or reproduction steps), display: **"Provide detail (Customer)"**
  - If ambiguous from the data, default to **"Provide detail (TBD)"** and flag for manual review.
- **Stale bug flag:** Bugs not modified in 14+ days get a ⚠️ flag next to the last-modified date.
- **Auto-archive candidate flag:** Bugs open 60+ days with no comment activity in the last 30 days are flagged as cleanup/closure candidates with: **"🧹 Review for closure"**
- Sort by priority (P0 first), then by days open descending.
- Tag newly filed bugs (filed since the last report) with a red **NEW** label in the synopsis.



## "What Changed" delta logic

Compare the current week's slide content against the previous week's slide (the next slide in the deck, since most recent is first). Auto-generate the "What Changed Since Last Update" section by diffing:

- **Blockers:** newly added, resolved, or escalated
- **Key actions:** newly added or completed
- **Status / trending:** any change in overall status or trending color
- **New bugs:** bugs opened since last report
- **Special topics:** new items or removals
- **Metrics:** week-over-week movement

Always note the previous report date: *"since [MM/DD]"*.

## Trending change logic

Trending color changes when any of the following occur:

- **⬆ Upgrade to 🟡 Yellow or 🔴 Red:**
  - A new blocker appears with no ETA
  - A P0 bug ages past 30 days without meaningful progress
  - A customer milestone is at risk
  - Customer escalation or increased management scrutiny is noted
- **⬇ Downgrade to 🟢 Green:**
  - All blockers have ETAs or are resolved
  - No P0 bugs are stale
  - Customer milestone is on track
- **Manual override:** The user can explicitly set trending; always note the previous value in parentheses.

Always display: `Trending: [color] (was [previous color])` when it changes; omit the parenthetical when unchanged.

## Email report structure

Reports must follow this exact section order for consistency:

1. **Header** (customer name, date, overall status, trending, priority, stack rank, PICs)
2. **Goal** (customer outcome statement)
3. **Why At Risk** (only when status is 🟡 or 🔴; omit when 🟢)
4. **What Changed Since Last Update** (delta from previous week)
5. **Summary / Current State**
6. **Blockers / Critical Path**
7. **Key Actions**
8. **High-Level Roadmap**
9. **Metrics**
10. **Open Bugs and Feature Requests** (full table)

### Subject line format

`YYYY-MM-DD | <Customer Name> Execution Health | Engineering/Product Perspective`

### Distribution lists

Email To and CC lists are defined in each customer's companion profile (`<customer-slug>-tpm/SKILL.md`). Do not hardcode distribution in the generation logic. If no profile defines distribution, ask the user before drafting.

## Post-generation verification

After drafting, verify before presenting to the user:

- [ ] Bug count in the section header matches the actual table row count
- [ ] All bug IDs mentioned in the Blockers section appear in the bug table
- [ ] Days open are calculated from the report date, not carried forward blindly
- [ ] No "Provide detail" status appears without a (Dev)/(Customer)/(TBD) qualifier
- [ ] All NVBugs links use `https://nvbugspro.nvidia.com/bug/<id>` format
- [ ] Trending change is noted with previous value when applicable
- [ ] Metrics source and date are cited


## Core workflow

1. Establish the customer outcome, workstream boundary, next milestone, and previous reporting cutoff.
2. Use the tracker as the index, then verify material claims in tickets, discussions, source control, builds, release records, QA evidence, security evidence, and customer feedback.
3. Preserve provenance: distinguish customer statements, engineering interpretation, product decisions, and TPM assessment.
4. Consolidate mirrored tickets into one management row while retaining every relevant identifier and direct link.
5. Distinguish proposed, in progress, merged, built, released, internally validated, and customer validated.
6. Make health, impact, evidence, blocker or decision, next action, owner, target date, and customer milestone explicit.
7. Re-read every edited tracker range, report, or draft. Verify links, dates, recipients, formatting, and the final rendered result.

## Authorization boundaries

- Read and synthesize when asked for status, reporting, or meeting preparation.
- Edit trackers, tickets, documents, or profiles only when the user asks for that mutation.
- Draft reports and email, but do not send or publish without explicit authorization.
- Do not expose private messages, restricted links, customer-confidential material, or personal distribution lists in broadly shared artifacts without approval.

## Expected result

Lead with the customer outcome and current health. Show what changed, why the workstream has its stated health, the few items needing action or decisions, and the roadmap. Keep detailed history in the tracker and a bounded ticket appendix.
