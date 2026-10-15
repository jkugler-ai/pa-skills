# Execution Health report

Read this reference whenever creating, refreshing, reviewing, or presenting a customer Execution Health report.

## Required executive structure

Use this order:

1. Compact branded header: customer/workstream title, as-of date, overall status, priority, and stack rank.
2. Compact inline workstream PICs.
3. Goal: one or two sentences describing the customer outcome and deployment context.
4. Why At Risk: when status is Yellow or Red, place a prominent one-sentence risk rationale immediately beneath the Goal. Name the customer milestone exposure and the concrete dependencies or decisions causing it. Do not use the callout merely because tickets remain open.
5. What Changed Since Last Update: only accomplishments, regressions, decisions, and validation changes since the previous sent report.
6. Summary / Current State.
7. Blockers / Critical Path.
8. Key Actions.
9. High-Level Roadmap.
10. Postscript issue table.

Use [../assets/execution-health-template.html](../assets/execution-health-template.html) as the visual starting point for rich HTML. Preserve its hierarchy and visual tokens while adapting the content and brand configuration.

## Content rules

- Explain why the overall status has its color.
- Separate delivered, released, internally validated, and customer-validated states.
- Link tickets inline using stable direct links.
- Every critical-path item and key action needs an owner and date, or an explicit unconfirmed or uncommitted value.
- Keep roadmap milestones outcome-oriented and chronological.
- For every product release, locate the actual release record, use its planned or actual release date, and link the release name directly to that record. If a release date still cannot be found after checking the release system, state the evidence gap.
- Keep the narrative at release-version and customer-outcome level. Retain merge requests, cherry-picks, pipelines, and branch mechanics in the tracker unless they explain the risk or decision.
- Source priority and stack rank from explicit planning evidence; never infer them from severity or a visual placeholder.

## Postscript issue table

The issue table is a bounded delta appendix, not the full historical tracker.

- Include every canonical ticket that is open at the report's as-of time.
- Also include tickets closed after the previous Execution Health email was actually sent.
- Use the sent-message timestamp as the cutoff, not the prior draft date, report file date, or an older reporting period.
- Exclude tickets closed before that cutoff.
- If there is no previous sent report, include open tickets and state that this is the initial baseline; add older closed tickets only when they are necessary to explain the current change narrative.
- Consolidate mirrored tickets into one row. Show related identifiers in that row only when they remain relevant under the same open-or-newly-closed rule.
- Use compact columns: canonical ticket, issue, health, and current disposition / next gate.
- Link the detailed source-of-truth tracker above or below the table.

## Final checks

1. Refresh material ticket comments, discussions, release records, and customer evidence.
2. Verify every source link.
3. Confirm owners and dates are evidence-backed.
4. Confirm the health callout matches the actual milestone exposure.
5. Confirm the previous sent-email cutoff used by What Changed and the issue appendix.
6. Verify release dates and availability from release records.
7. Ensure customer validation is not implied from merge, build, release, or internal QA alone.
8. Remove private or restricted discussion links unless approved for the audience.
9. Render the rich report and inspect alignment, wrapping, table width, and link styling.

## Verify trend against the slide

Source Health and Trending independently from the current customer slide using the entrypoint slide-sourced rules. The rendered email header and every narrative trend statement must agree with the explicit slide indicator. Bug closures may be reported as progress but must not automatically change Trending. If the slide value is unavailable, show Unverified rather than a green default. Preserve source slide/date evidence with the report.

## Current-period check

Use the latest dated customer slide and current verified evidence for roadmap entries. Profile milestones and stored report dates are historical context. Exclude superseded past milestones unless a current unresolved dependency justifies them. An elapsed milestone must not be labeled complete without explicit evidence.
