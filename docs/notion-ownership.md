# Notion Ownership Map

Which AI writes to which shared Notion DB. Both AIs READ everything. Only the writer-AI EDITS.

To be filled in once the shared Notion workspace is created. Template:

| Database | Writer-AI | Reader-AIs | Notes |
|----------|-----------|------------|-------|
| Summit clients | Sarah | Taya | Pipeline, status, payment state |
| Summit ad campaigns | Sarah | Taya | Nyaaz coordination |
| Joint deliverables | Both (claim protocol) | Both | High coordination |
| Shared content queue | Sarah | Taya | Summit-side content |
| Frost↔Jet sync log | Both (append-only) | Both | Daily/weekly handoff notes |

If a write is needed by a non-owner, file a `notion-write-needed` issue per rules-of-engagement.md §4.
