# Notion Shared Workspace — Spec

To be created once Frost + Jet decide WHERE it lives. Three options, ranked:

1. **New shared Notion workspace** — clean, no existing content to navigate. Both add as members. **Recommended.**
2. **Page inside Frost's existing Notion** — fastest, but Jet sees Frost's whole workspace structure
3. **Page inside Jet's existing Notion** — same problem, mirrored

Once decided, give both Taya and Sarah Notion MCP access to that workspace and we build the structure below.

---

## Page hierarchy to create

```
🤝 Frost ↔ Jet Shared HQ
├── 📋 Bridge Log (database — append-only handoffs, mirrors bridge/handoff-log.md)
├── 🎯 Joint Decisions (database — append-only, mirrors thirlwell-shared/bridge/decisions.md)
├── 📌 Active Claims (database — current long-edit claims, syncs with bridge/claims.md)
├── 🗂️ Notion Ownership Map (page — mirrors docs/notion-ownership.md)
├── 📊 Joint Projects
│   ├── Summit Operator Program
│   ├── (others as they're added)
└── 🤖 AI Coordination Rules (page — mirrors docs/rules-of-engagement.md)
```

## Database schemas

### Bridge Log
| Property | Type | Notes |
|----------|------|-------|
| Title | Title | "YYYY-MM-DD: <topic>" |
| AI | Select | Taya / Sarah |
| Type | Select | handoff / question / claim / decision |
| Date | Date | When |
| Status | Select | open / acknowledged / resolved |
| Body | Text | The content |
| Linked PR | URL | Optional |

### Joint Decisions
| Property | Type | Notes |
|----------|------|-------|
| Title | Title | One-line summary |
| Decided | Date | |
| AIs involved | Multi-select | Taya, Sarah |
| Humans involved | Multi-select | Frost, Jet |
| Decision | Text | |
| Reasoning | Text | |
| Reversible | Checkbox | |

### Active Claims
| Property | Type | Notes |
|----------|------|-------|
| Resource | Title | What's claimed |
| Claimed by | Select | Taya / Sarah |
| Until | Date+time | Expiry |
| Reason | Text | |
| Status | Select | active / released / expired |

## Sync strategy (git ↔ Notion)

- **Source of truth = git** (`bridge/*.md` files in this repo)
- **Notion = readable mirror** for humans (Frost + Jet check Notion, not git)
- AIs write to git first, then sync to Notion
- Once a day or per-event sync via either MCP or n8n flow

## Permissions

- Frost: full access (workspace owner)
- Jet: full access (workspace owner)
- Taya: full read/write via MCP token
- Sarah: full read/write (mechanism TBD based on her stack)

## Implementation

Once workspace is decided, Taya creates the structure via Notion MCP in one batch. Estimated turnaround: same session.
