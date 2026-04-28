# thirlwell-shared

Shared GitHub workspace for projects Frost (Thirlwell) and Jet (Summit) work on together. Both AI assistants — **Taya** (Frost's) and **Sarah** (Jet's) — collaborate here through git, while keeping their private brains, memories, and identities completely separate in their own private repos.

## Who has access

- **Humans:** Frost Thirlwell (owner), Jetsan Evans (owner)
- **AI assistants:** Taya (Frost's Claude Code), Sarah (Jet's assistant)

Each AI is a collaborator with write access to this org **only**. Neither can read the other's private repo. Identities never merge.

## What lives here

Only joint projects. Things both AIs need to edit.

- `projects/` — every shared project gets its own subdir
- `bridge/` — the AI-to-AI coordination layer (claim logs, daily handoffs, status pings)
- `docs/` — rules of engagement, contracts, conventions
- `.github/` — branch protection, PR templates, CODEOWNERS

## What does NOT live here

- Frost's personal vault, Taya's memory, Taya's CLAUDE.md → `frost-private`
- Jet's personal context, Sarah's memory, Sarah's system prompt → `jet-private`
- Anything that's only one person's business

If a project becomes shared, move it here. If a shared project becomes one-sided, move it back.

## Rules of engagement

Full spec in [docs/rules-of-engagement.md](docs/rules-of-engagement.md). The short version:

1. **Branch per AI.** Taya works on `taya/*`, Sarah works on `sarah/*`. Never push to `main` directly.
2. **PRs reviewed by the other AI.** Cross-review is mandatory before merge.
3. **Claim before long edits.** Drop a claim in the bridge channel before any edit > 15 min.
4. **Notion ownership rules apply.** See [docs/notion-ownership.md](docs/notion-ownership.md) for which AI writes to which DB.
5. **Conflicts escalate to humans.** If Taya and Sarah disagree on a merge, Frost + Jet decide.

## How to start a new joint project

```
cd projects/
mkdir <project-name>
cd <project-name>
# Add a README.md describing scope, owner-AI, status
```

Then push to a branch and open a PR.
