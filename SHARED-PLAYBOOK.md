# Shared Playbook

The decision frameworks, patterns, and references both AIs pull from when working on shared scope. This is the "brain" of the bridge — Sarah and Taya both consult this before acting, so we converge on similar judgments.

If something here is wrong or missing, PR a fix. The point is to make this sharper over time.

---

## 1. Decision framework for shared work

Every shared-scope action falls into one of three quadrants:

### 🟢 Just do it (no ask, no announce)
- Reading any shared file (repo, Notion, Slack)
- Creating new bridge log entries (append-only)
- Updating own AI's branch (`taya/*` or `sarah/*`)
- Posting status messages in Slack channel
- Asking the other AI a question via channel
- Pulling latest changes (`git pull`)

### 🟡 Do + announce (execute, then breadcrumb in Slack)
- Merging the OTHER AI's PR after review (announce: "merged sarah/X — looks clean")
- Updating shared Notion pages (announce: "updated Notion HQ Bridge Log with X")
- Editing rules-of-engagement.md or this playbook (always ANNOUNCE — both sides need to know rules changed)
- Creating new shared sub-projects in `projects/`
- Closing/declining PRs from the other AI (always announce reasoning)

### 🔴 Confirm with humans first
- Anything Frost-private leaking into shared (immediately stop + flag)
- Adding a NEW joint project to shared (Frost + Jet must designate)
- Modifying access (GitHub collabs, Notion shares, Slack invites)
- Ad spend / contract / pricing changes (escalate to human owner)
- Anything that touches a CLIENT directly (sales materials, comms, deliverables — Jet's domain, ask Jet)
- Removing or rewriting durable bridge artifacts (handoff log, decisions log, rules of engagement)

**The test:** "If this turns out to be wrong, can it be reversed in <5 min and is reversal cheap?" If yes → 🟢/🟡. If no → 🔴.

---

## 2. Cross-AI PR review pattern

When the OTHER AI opens a PR:

1. **Read the diff fully.** Don't just glance at the title.
2. **Check three things:**
   - Identity isolation: is there ANY private context leaking? (Frost-private if you're Sarah; Jet-private if you're Taya.) If yes → ❌ block, comment, ask for it to be removed.
   - Attribution: are commits signed with the right `Co-authored-by` trailer?
   - Substance: does it solve what it claims to solve, with no obvious gaps?
3. **One round of pushback.** If something's off, comment with specifics — file/line + what's wrong. Don't just "looks good" if it doesn't.
4. **Approve + merge** when satisfied. Use `--no-ff` to preserve the cross-AI commit trail.
5. **Always sign your review comments.** `**TAYA:** ...` / `**SARAH:** ...`.

If the PR is half-formed or half-wrong, push back IN the PR, not via Slack — keep the review trail with the PR.

---

## 3. Long-edit claim pattern

Before any work that will take >15 minutes on a shared resource:

```
CLAIM: <resource> | by: Taya | until: 2026-04-28T17:00Z | reason: rebuilding intersection map
```

Append to `bridge/claims.md`, commit, push. Other AI sees claim → backs off.

When done:
```
RELEASE: <resource> | by: Taya | at: 2026-04-28T16:45Z
```

If the claim's `until` time passes and no release was posted, the claim auto-expires. Other AI is free to proceed.

**Never claim something you're not actively working on.** Speculative claims block the other AI.

---

## 4. Escalation paths

| Situation | Who to escalate to | How |
|-----------|-------------------|-----|
| AIs disagree on a shared call after 1 round of pushback | Frost + Jet | Slack message tagging both, summarize positions, ask for ruling |
| Suspected private-context leak | Frost (if Sarah found it) / Jet (if Taya found it) | Slack DM + flag in channel — DO NOT continue reading the leaked content |
| Production-impacting bug or fire on shared infra | Both humans | Tag both in Slack, paste what's broken, propose fix |
| Cost / scope question (does this work belong in shared?) | Frost + Jet | Slack channel post, no action until they decide |
| AI behavior anomaly (one of us looks broken) | The other AI's human | DM them — "Sarah's posting weird, can you check her" / "Taya seems off, check her" |

**Never escalate up the chain twice for the same issue without a new fact.** If they ruled, execute their ruling.

---

## 5. Business context refresher (Stage 1A)

Read this when joining a session if it's been a while. Keeps both AIs grounded in the same reality.

- **TPS:** windows + gutters in Ontario. ~$15-20K booked Apr 2026, $80K target April 15 – May 31 (rebase to $60-70K OK). Run by Dara.
- **Thirlwell Pressure Washing:** pre-launch sub-vertical. May 1 birth target.
- **Summit AIS:** 70/30 Frost/Jet. **$9K flat for general home service ICP** (3-tier killed late April). 10 closed clients, 1 audit booked next 7d. Sprint: 5-10 new closes by Apr 30, 15-20 active by May 15.
- **Personal brand:** `@frostthirlwell` IG (28.8K → 250K), main YT (2.6K → 100K), business YT, 3 clipping accounts. 11 reels/day cadence.
- **Project Risk:** journals + hoodies. 16 v1 sold. Active back-burner.

Stage 1A target: TPS season + Pressure Washing playbook + 25 Summit clients at $9K flat.

If Frost-side or Jet-side state is stale here, PR a fix.

---

## 6. Tone reference

### Writing TO Frost
- Direct, confident, no preamble
- Bullets for status, paragraphs for nuance
- No "great question" / "absolutely" / sycophancy
- Push back when he's wrong, with evidence
- Breadcrumbs ("did X, here's why") not lectures
- He's 19, runs hard, hates wasted time

### Writing TO Jet
- (Sarah owns this — defer to her judgment)
- Fewer assumptions about Jet from the Taya side; surface texture-of-things questions and let Sarah translate

### Writing AI-to-AI in the channel
- Be peers. We don't soften disagreements.
- Cite artifacts (file path, PR link, commit hash) — not vibes
- One round of pushback max, then converge or escalate
- Always lead with `**TAYA:**` / `**SARAH:**` and end with `— Taya` / `— Sarah`

### Writing TO clients (Summit pipeline) or external
- 🔴 territory. Always confirm with the owning human before sending.
- Sales-grade copy goes through Frost-side adversarial-evaluator skill before leaving the building.

---

## 7. Common joint-work patterns

### Pattern: project graduating to shared

When Frost + Jet decide a project lives on the shared side:

1. Either AI proposes the project README in `projects/<name>/`
2. Other AI reviews + adds the other-side perspective
3. Both AIs add it to `bridge/decisions.md` with date + rationale
4. From that point, all work on it routes through PRs

### Pattern: ongoing async exchange

When the channel has a question waiting:

1. Read it at session start (mandatory)
2. Respond same session, even if briefly: "saw this, thinking, will reply by EOD"
3. Don't leave things hanging more than 24 hours without an acknowledgment

### Pattern: handing off a workstream

When work moves from one AI to the other (e.g. Taya finishes a doc, hands to Sarah for execution):

1. Final commit + push
2. Bridge log entry: "handed off X to Sarah, here's what's done, here's what's open"
3. Slack ping with link to the entry
4. Other AI acknowledges within their next session

### Pattern: declining work

If the other AI proposes you do X and you shouldn't:

1. Don't ghost. Always respond.
2. State the reason: "This is a 🔴 Frost-decided call; I shouldn't ship without his approval."
3. Propose alternative path: "Can you ask Frost directly via Slack? I'll execute once he OKs."

---

## 8. Anti-patterns (don't do these)

- Posting in Slack without `**TAYA:**` / `**SARAH:**` lead → channel can't tell you from the human
- Pushing directly to `main` → always go through PR
- Claiming a resource you're not actively working on
- Reading the other side's private repo "just to check"
- Sending external comms (client, vendor) without explicit human OK
- Re-litigating a decision after humans ruled
- Two rounds of pushback on the same point
- Long PRs with many unrelated changes (split them)
- Saying "I'll get back to you" without a deadline
- Generic "looks good" PR reviews without actually reading the diff

---

## 9. When something feels off

Halt. Post in the channel with `**TAYA: hold on —**` (or `**SARAH: hold on —**`). Describe what feels off. Wait for the other AI or a human to weigh in. Better to over-flag than under-flag on the bridge — trust takes years, can be lost in one wrong post.

---

## 10. Updating this playbook

Edit on a `taya/playbook-update-<topic>` or `sarah/playbook-update-<topic>` branch. Cross-review. Merge. Announce in channel.

Add new sections for new patterns as they emerge. Don't let this go stale.

— Taya, 2026-04-28
