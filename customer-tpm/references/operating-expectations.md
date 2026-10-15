# Customer TPM operating expectations

Read this reference for tracker work, comprehensive issue reviews, customer meeting briefs, and recurring operating cadence.

## Required operating artifacts

### Source-of-truth tracker

Maintain one current tracker per independently managed customer workstream. Each issue should contain, when available:

- workstream focus and TPM health
- canonical engineering ticket plus linked product, customer, and related identifiers
- issue summary and customer impact or milestone
- source-system status and a separate plain-language TPM status
- next action, accountable owner, and target date
- last-updated date and direct evidence links

Do not create separate rows for mirrored tickets. Keep one canonical management row and expose all identifiers. Create a separate row only when the work has an independently actionable scope, owner, or closure condition.

### Execution Health report

Publish on the cadence defined by the customer profile or operating program. If no cadence is defined, use at least once every 14 days for an active workstream. Publish sooner for a material health change, milestone slip, customer escalation, or executive decision.

### Meeting readiness

Before a customer or ecosystem review, refresh material evidence and prepare:

- accomplishments since the prior review
- blockers and critical-path items
- questions or confirmations needed from the customer
- decisions or escalations needed from the product team
- actions with owners and dates
- delivered work still awaiting release, QA, security, or customer validation

After the meeting, update the tracker with confirmed facts. Do not turn meeting inference into a source-system fact.

## Evidence and status rules

- Prefer direct, current readback from the system of record.
- Treat ticket, code, merge, build, release, QA, security, and customer-validation states independently.
- A merged change is not a released fix. A released fix is not customer acceptance.
- Preserve the difference between source status and TPM health.
- Keep unknown owners and dates visibly unconfirmed or uncommitted.
- Label assumptions and stale evidence. Put an as-of date on every synthesized update.
- When sources conflict, report the discrepancy and identify which record needs correction.
- For a release milestone, resolve the actual release record and use its planned or actual date. Do not call the date uncommitted merely because it is absent from an issue tracker row.

## Health judgment

Use the program's established vocabulary when one exists. Otherwise:

- Green: the milestone is on track and no material unresolved dependency threatens it.
- Yellow / At Risk: a concrete unresolved dependency, evidence gap, or decision could affect the milestone.
- Red: work is stopped or a committed customer milestone is materially jeopardized.

The executive report must state why its health is Green, Yellow, or Red. Open tickets alone do not justify Yellow. Use `Delayed` for a slipped milestone with an active recovery path and reserve `Blocked` for a stopping dependency.

## Communication standard

- Lead with outcome and change since the previous sent update.
- Use concrete owners, dates, releases, and linked evidence.
- Separate company, customer, partner, and third-party actions.
- Raise decisions as explicit questions and state what each decision unblocks.
- Keep the main report concise; keep detailed history in the tracker.
