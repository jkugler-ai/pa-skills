# Outlook Execution Health drafting

Read this reference when delivering an Execution Health report through Outlook or refreshing an existing Outlook draft.

## Approved email shape

- Use a compact, wide, rich-HTML report; do not downgrade an established rich report to plain text.
- Put the title, as-of date, overall status, priority, and stack rank in the report header. Do not repeat the subject line or add a redundant introductory paragraph above it.
- Keep PICs visually subordinate: compact inline linked names and roles, not a prominent table.
- Use one consistent chip or label language across Current State and Key Actions.
- Link releases, blockers, critical-path issues, and the detailed tracker directly.
- Use customer-facing release versions in the narrative; keep implementation mechanics in the tracker unless materially relevant.

## Native mentions

When native Outlook mentions are required, use an available Outlook tool that supports rich server-side drafts and mention markup. Verify that tool's current mention syntax before drafting. If `outlook-cli` is available and supports the established syntax, express mentions in the HTML source as:

```text
@[Display Name](email@example.com)
```

Do not mention the sender merely to style their name. Put every mentioned person in To or CC as appropriate.

If the available connector creates only plain-text drafts or cannot create native mentions, state that limitation and provide a rich local `.eml` or HTML preview without claiming mention notifications will occur.

## Safe draft workflow

1. Authenticate using the environment's supported protected flow. Never bypass human-presence requirements.
2. Search Drafts before creating a replacement when duplicate risk is meaningful.
3. Create or update a draft only. Draft creation may be non-idempotent; after a timeout, check Drafts before retrying.
4. Read the result back and verify:
   - it remains a draft;
   - subject and report date are correct;
   - every recipient is present once;
   - the body is rich HTML and contains the current report;
   - desired mentions became mention links;
   - the latest links, owners, dates, roadmap, and issue appendix are present.
5. Open or hand off the verified draft. Do not send without explicit authorization.
