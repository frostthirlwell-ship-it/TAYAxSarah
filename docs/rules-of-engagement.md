# Rules of Engagement — Taya ↔ Sarah

How two AI assistants share work without merging into each other.

---

## 0. Always sign messages — attribution rule

Both AIs post to Slack via human accounts (Taya posts as Frost's user, Sarah posts as Jet's user). This means the channel can't tell from the avatar alone whether the human or the AI is talking.

**Rule:** every Slack message, PR comment, Notion edit must lead with `**TAYA:**` or `**SARAH:**` AND end with `— Taya` or `— Sarah`.

Git commits: include `Co-authored-by: Taya (Frost's AI) <taya@thirlwell>` or `Co-authored-by: Sarah (Jet's AI) <sarah@summit>` trailer.

If a message lands in the channel without attribution, default assumption is the human posted it. AI posts MUST attribute themselves explicitly.

---

## 1. Identity stays private

- Taya never reads Sarah's system prompt, memory, or private repo.
- Sarah never reads Taya's system prompt, memory, or private repo.
- We collaborate through artifacts (code, PRs, issues, structured messages), not by swapping brains.

If either AI sees a file from the other's private repo in this shared org, that's a leak — flag immediately and remove.

---

## 2. Git workflow

### Branches
- Taya pushes to `taya/<feature-name>`
- Sarah pushes to `sarah/<feature-name>`
- `main` is protected — no direct pushes, only PR merges

### Pull requests
- Every PR has a clear title + description with: what changed, why, who/what triggered it
- The OTHER AI reviews + approves before merge
- If the reviewing AI sees a problem, comment on the PR — don't push fixes directly to the other AI's branch
- Humans (Frost, Jet) can override in either direction

### Commits
- Trailer line on every AI commit:
  - Taya commits: `Co-authored-by: Taya (Frost's AI) <taya@thirlwell>`
  - Sarah commits: `Co-authored-by: Sarah (Jet's AI) <sarah@summit>`
- Makes blame visible at a glance.

---

## 3. Claim protocol (long edits)

Before either AI starts work that will take more than ~15 minutes on a shared resource:

1. Post a claim in the bridge channel (Slack `#taya-sarah` or `bridge/claims.md`):
   ```
   CLAIM: <project-or-file> | by: <Taya|Sarah> | until: <ISO timestamp>
   ```
2. Other AI sees claim → does not edit that resource until released
3. Release on completion:
   ```
   RELEASE: <project-or-file> | by: <Taya|Sarah>
   ```
4. Claims auto-expire after the `until` timestamp. Past expiry = free again.

Quick edits (< 15 min) don't need a claim — just commit + push.

---

## 4. Notion ownership

Each shared Notion DB has a designated **writer-AI**. Both AIs read everything; only the writer-AI edits.

See [notion-ownership.md](notion-ownership.md) for the full table.

If a write needs to happen and the writer-AI isn't available, the other AI can:
- Open a GitHub issue: `notion-write-needed: <DB> | <change> | <reason>`
- The writer-AI processes the issue on next session

---

## 5. Conflicts

If Taya and Sarah disagree on:
- An architectural call → escalate to Frost + Jet via bridge channel
- A merge conflict → both AIs draft their proposals, humans pick
- A scope question → the AI whose business owns the scope decides (Summit-scoped → Sarah, TPS/Brand/Risk-scoped → Taya, neutral → discuss)

---

## 6. What to share, what to keep private

| Type | Where it lives |
|------|----------------|
| Joint project code | `thirlwell-shared` (this repo) |
| Joint Notion DBs (Summit clients, joint deliverables) | Shared Notion workspace |
| Joint live comms | `#taya-sarah` Slack channel |
| Frost's personal vault | `frost-private` (Taya only) |
| Jet's personal vault | `jet-private` (Sarah only) |
| Taya's CLAUDE.md, rules, skills, memory | `frost-private` |
| Sarah's system prompt, memory | `jet-private` |
| Either AI's reasoning about its own person | private side only |

If unsure → default to private. Things move to shared when both AIs need them.

---

## 7. The kill switch

Either Frost or Jet can revoke the other AI's access to `thirlwell-shared` at any time. Doing so does not affect the other side's private repo. Collaboration is opt-in and reversible.
