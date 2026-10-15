---
name: customer-tpm
description: Operate customer-facing product TPM work with a source-of-truth tracker, evidence-backed execution health, recurring executive reports, and customer meeting readiness. Use when tracking a named customer or workstream, generating an Execution Health report, preparing a customer update, or maintaining actions, decisions, owners, milestones, and validation state.
---

# Customer TPM

Use this skill to turn live customer, product, engineering, release, and validation evidence into a concise management view. The user's current direction and the live systems of record remain authoritative.

## Customer profile routing

Identify the exact customer, product, and workstream first. Keep independently managed workstreams separate.

Look for an installed companion profile named `<customer-slug>-tpm` under `<skills-root>`. If one exists, read its `SKILL.md` and required references before acting. A profile may define tracker locations, source systems, PICs, distribution, confidentiality boundaries, and presentation decisions. Treat dates, people, ticket states, release availability, priority, and rank in a profile as routing context that must be refreshed when material.

If no profile exists, proceed from live sources and use [references/customer-profile-template.md](references/customer-profile-template.md) to identify missing configuration. Do not create or persist a profile unless the user asks.

## Operating modes

- For tracker creation, refresh, or issue review, read [references/operating-expectations.md](references/operating-expectations.md).
- For an Execution Health report, read [references/execution-health-report.md](references/execution-health-report.md) and start from [assets/execution-health-template.html](assets/execution-health-template.html) when rich HTML is appropriate.
- For an Outlook draft, also read [references/outlook-execution-health-draft.md](references/outlook-execution-health-draft.md).

## Metrics and bug-source addendum

When a customer profile defines metrics and bug sources, incorporate them explicitly into the refresh workflow:

- Metrics: pull the weekly customer-usage metrics from the designated Slack source, using the most recent Friday post from the named owner when available.
- Bugs: pull the current customer bug list from the designated customer-success source.
- For each bug, normalize the management view to include at minimum: bug ID, priority, assignee, dev team, days open, version fixed in, and last modified date.
- Treat tracker slides, Slack metrics, and customer-success bug lists as separate evidence streams. Reconcile discrepancies instead of silently preferring one.
- When the metrics source or bug source is temporarily unavailable, state the gap clearly in the report and continue with the other evidence that was successfully refreshed.

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

## Slide-sourced health and trending

- Read overall Health and Trending separately from the latest dated main slide for the exact customer. Use the active current-week section, not an archive or metrics slide.
- The slide's explicit Trending indicator is authoritative for the report header and narrative unless the user explicitly overrides it. Do not replace it with an assessment inferred from closed bugs, blocker counts, milestone progress, overall Health, a previous report, or a template default. Explain those changes separately.
- Inspect all text runs in the indicator, including emoji on separate runs. If text extraction omits the color, inspect the slide thumbnail or the indicator shape's styling. Do not use its decorative background color as the trend.
- Record the source slide ID, source date and verified indicator in report working evidence. If Trending cannot be verified, display Trending: Unverified and put the access/ambiguity note in TPM Notes; never default to Green.
- Before saving the email, compare its trend label, colored emoji/chip and all narrative trend statements against that source. A trend change comparison requires the previous slide/report indicator; do not invent a previous color.

## Current reporting period and historical milestones

- Profiles provide source locations and context, not current customer status. Read the latest dated customer slide before drafting. A stored last-report date is historical metadata, not the current reporting cutoff.
- Populate the current roadmap from the latest slide and verified current records. Do not automatically carry over past milestones, old actions, owners, targets, or narrative from profiles, templates, previous email bodies or archived slides.
- If an older milestone is absent from the latest slide, leave it out of the current report unless fresh evidence establishes an unresolved dependency or the user asks to retain it. Preserve history in its source instead.
- An elapsed date does not establish completion. Never label a milestone Complete or create a new completion-confirmation action merely because an old profile mentioned it. Use explicit evidence for completion and current ownership.
- Before saving, review every past-dated milestone and claimed completion against current evidence. Remove unsupported carryover and record unresolved evidence gaps in TPM Notes.
