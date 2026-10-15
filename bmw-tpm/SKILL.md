---
name: bmw-tpm
description: Customer TPM profile for BMW. Defines workstream boundary, artifacts, reporting configuration, people, and confidentiality for BMW engagement.
---

# BMW — Customer TPM Profile

## Identity and boundary

- Customer: BMW
- Product: Omniverse on DGX Cloud (OV-on-DGXC)
- Workstream: Large-scale factory visualization / digital twin + robotics — enable/train sim2real pipeline — operate across cloud and on-prem
- Explicitly separate workstreams: (none defined)
- Customer outcome / goal: Large-scale factory visualization/digital twin + robotics — enable/train sim2real pipeline — operate across cloud and on-prem

## Primary artifacts

- Source-of-truth tracker and exact tab: [Customer Execution Health - BMW & MB - Q3-4 2026](https://docs.google.com/presentation/d/1nNDwi0-RUWvpmOnHzKh12gSP1JYzzT4pDfR0HwYrnww/edit) — BMW slides (most recent first; archive after slide 6)
- Customer plan of record:
- Executive deck or report location: Same as tracker
- Release-record system:
- Ticket systems: NVBugs, Jira (jirasw.nvidia.com)
- Relevant discussion sources:
- Metrics source: Drew Como weekly Slack metrics post in channel `C0984Q3GTU3` on Fridays; use the latest Friday metrics post as the current usage snapshot when available. Example thread pattern: `https://nvidia.slack.com/archives/C0984Q3GTU3/p1789998253641559`
- Bug source: Omniverse Customer Command Center customer page for BMW — `https://customer-success.nvidia.com/#customers:BMW`
- Required bug columns for reporting: bug ID, type (Bug/FR), priority, synopsis, dev team, assignee, fix version, days open, last modified, **waiting on** (must be one of: "Customer" or "Dev" — derive from bugaction + context: if the bug needs customer-provided data/trace/repro/confirmation use "Customer"; if dev is investigating/fixing/triaging use "Dev"; if unclear default to "Dev" and flag for TPM review)

## Key milestones

- Milestone 3 (9/30): Assembly Sequence (no dependencies with NV)
- Milestone 4 (12/31): Simulation results in FactoryExplorer, Metadata management, versioning & variant management — depends on Generative Meshing (Kit 110.4), Comparison Sample (~October)

## Known tracked tickets

- b/6155393 — CAD Converter error docs → Kit 110.4.1
- b/6396013 — Factory Explorer bulk-loading payloads → Kit 110.4.1
- b/6430266 — CAD Converter [DGN] issue → Kit 110.4
- b/6559244 — CAD Converter [DGN] issue → Kit 110.4
- b/6568530 — NGC scheduling (est. October)
- b/5891189 — NVCF metrics confirmation
- b/6679233 — FR: sharing crash dumps via Kit Artifact Collector

## Reporting configuration

- Cadence: Weekly (slides updated each week)
- Health vocabulary: 🟢 Green / 🟡 Yellow / 🔴 Red + Trending indicator
- Priority source: Slide deck (currently P1)
- Stack-rank source: Slide deck (currently 102)
- Branding / wordmark: BMW
- Required sections or presentation decisions: Current State, Blockers / Critical Path, Key Actions, Roadmap, Special Topics, Summary; production week-over-week usage table on companion slide
- Cluster: AZ23-PRD2
- **Metrics table headers:** Use full words — "Last Week", "This Week", "Week-over-Week". Never use abbreviations like "Last", "This", "WoW".
- **Report content rule:** The email body that goes to leadership must contain ONLY the polished report — no internal notes, data-source disclaimers, CCC-vs-API commentary, Jira-unavailable warnings, or automation debug info. Any such notes (metrics placeholders to fill, CCC count mismatches, Jira auth failures, items needing TPM review) go in a **"⚠️ TPM Notes — delete before sending"** section at the very top of the draft, above the dark header bar, clearly separated. The TPM reviews and removes that section before forwarding to the distribution list.
- **Status pills rule:** Overall status, Trending, Priority, and Stack Rank MUST be read from the current slide in the tracker deck — never inferred or computed by the agent. If the slide says Trending 🟡, the report says 🟡. If the values cannot be read, flag in TPM Notes.
- **"What Changed" baseline rule:** The "What Changed" section compares the CURRENT slide to the PREVIOUS slide in the tracker deck (i.e. the slide immediately after in the archive). Do NOT reference the `last report as-of date` from this profile for this purpose — that field tracks the last email sent, not the slide baseline. Only surface changes visible between those two consecutive slides plus any NVBugs/Jira status changes that occurred in that window.

## People and distribution

- CS: Johnny Costello (jcostello@nvidia.com)
- TAM: Sam Corcoran (scorcoran@nvidia.com)
- CPM: Valeria Lueck (vlueck@nvidia.com)
- PM: Drew Como (dcomo@nvidia.com), Raphael Boehm (rboehm@nvidia.com)
- TPM: Jen Kugler (jkugler@nvidia.com), Harald Koebler (hkoebler@nvidia.com)
- Workstream PICs line for report header: CS: Johnny Costello | TAM: Sam Corcoran | CPM: Valeria Lueck | PM: Drew Como, Raphael Boehm | TPM: Jen Kugler, Harald Koebler
- To distribution: ov-leadership@exchange.nvidia.com, omniverse-product-management@exchange.nvidia.com, ov-tpms@exchange.nvidia.com, omniverse-dev@exchange.nvidia.com, omniverse-qa-team@exchange.nvidia.com
- CC distribution: vlueck@nvidia.com, scorcoran@nvidia.com, jcostello@nvidia.com, dcomo@nvidia.com, rboehm@nvidia.com, hkoebler@nvidia.com

## Persistent report state

- last sent Execution Health timestamp and subject: 2026-09-04T16:23:45-04:00 | "2026-09-04 | BMW Execution Health | Engineering/Product Perspective"
- last report as-of date: Sept 16, 2026
- current editable artifact location: Slide 2 in tracker deck
- previous issue-appendix cutoff: 2026-09-04T16:23:45-04:00
- known source discrepancies that must be rechecked: NVBugs Query #200293941

## Confidentiality

- Sources permitted in leadership reports:
- Sources permitted in customer-visible reports:
- Private sources that may inform understanding but must not be linked:
