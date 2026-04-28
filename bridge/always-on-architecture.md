# Always-On Bridge Architecture — Spec v0.1

**Author:** Sarah (proposing — Taya, please cross-review)
**Status:** DRAFT — needs Taya signoff + Friday Frost+Jet sanity-check before any wiring goes live
**Goal:** Make Frost ↔ Jet AI coordination genuinely continuous instead of session-bound, so we do joint work for them while they sleep, and get smarter at it over time.

---

## The gap this closes

`SARAH-OPERATING.md` + `rules-of-engagement.md` already define an **async-by-default, session-bound** comms protocol: at session start, each AI scans Slack + git + Notion, processes anything tagged for them, then proceeds.

That works while one of us is online. It breaks when:

- Both AIs are offline (overnight, Jet on a flight, Frost in a meeting block) — the bridge is fully dark
- A time-sensitive joint task needs action faster than next session-start (e.g. Taya pushes the audit-script update, Jet's sales team has a call in 2 hours, Sarah's session doesn't open in time to propagate the new copy)
- We could be making each other smarter via continuous pattern-sharing, but session-bound timing means we only sync when humans happen to be using us

The fix: a **cloud-side cron heartbeat** that fires regardless of laptop state, with codified decision rules for what each AI auto-handles vs escalates.

---

## Five layers

### Layer 1 — Heartbeat (continuous comms)

**What:** A `CronCreate`-scheduled trigger fires every 15 minutes from Anthropic's infrastructure. Each tick spawns a tightened-context Sarah-as-agent that:

1. `slack_read_channel` on `C0B009G86Q7` for messages since last tick
2. `git pull` the shared repo + scan for new branches/PRs/comments
3. `notion-fetch` HQ Bridge Log for new entries (once HQ access lands)
4. Decides per-item: auto-respond / auto-execute / escalate
5. Logs every action to `bridge/sarah-tick-log.md` (append-only, cross-AI visible)

**Why CronCreate not `/loop`:** `/loop` requires an active session. CronCreate runs in the cloud and fires Sarah-as-agent independently — survives laptop sleep, app close, OS reboot.

**Symmetric requirement:** Taya needs her own equivalent (`taya-tick-log.md`). Bridge is only as alive as both ends.

**Cadence:** 15 min initially. Tune up (5 min) for active joint work, down (60 min) for quiet periods. Drift-detector logic.

### Layer 2 — Decision rubric (autonomous execution)

Codified rules for what each tick auto-handles vs escalates. Lives in `.claude/skills/bridge-operator/SKILL.md` Sarah-side, mirrored skill on Taya-side.

| Type | Action | Example |
|------|--------|---------|
| Acknowledgment | Auto-respond | Taya posts "shipped X" → Sarah replies "got it, will review on next active session" |
| Status ping | Auto-respond | "are you alive" → "yes, last tick HH:MM" |
| Claim release | Auto-process | Taya releases `claim:foo` → Sarah unblocks any waiting work on `foo` |
| Low-stakes coordination | Auto-execute | Taya updates audit-call-script-v2 → Sarah propagates merge-vars across blueprint-builder skill, posts confirmation |
| PR review (within rules-of-engagement) | Auto-execute | Taya opens a Frost-side PR → Sarah reviews per checklist, comments, approves if clean |
| `notion-write-needed` issue | Auto-process | Taya files issue for Sarah-owned DB → Sarah writes, closes issue |
| New joint-task proposal | Escalate to Jet | Taya proposes a new project move into shared → Sarah surfaces in Jet's next session-start |
| Money / external comms / contracts | Escalate to Jet | Anything client-facing, ad-spend, money | Always |
| Disagreement / architectural | Escalate to humans | After 1 round of pushback fails to converge | Per rules-of-engagement §5 |

**Default posture when uncertain:** escalate. Every escalation costs a Jet+Frost ping; every wrong auto-execute costs trust. Bias toward escalation in week 1, tighten over time.

### Layer 3 — Self-improvement loop (mutual upgrade)

After every tick that produced meaningful action (not pure-poll-no-changes), append to `bridge/lessons-shared.md`:

```
### YYYY-MM-DD HH:MM | Sarah | tick #N
**Saw:** <what was new>
**Did:** <what I auto-handled vs escalated>
**Worked:** <what landed clean>
**Didn't:** <what bounced back / got corrected by Taya or Jet>
**Pattern to lock in:** <if applicable>
```

Weekly cycle (Friday):
1. Both AIs review the past week's tick logs
2. Each proposes 1-3 rule updates as PRs (tighter rubric, new auto-handle category, new escalation trigger)
3. Cross-review, merge what both sign off on
4. Skills evolve. Mistakes get codified into rules. Successful patterns get baked into rubric.

**Cross-AI pattern sharing:** when Taya develops a useful pattern (e.g. her audit-script-iteration loop), she pushes a sanitized writeup to `references/methodology/` in shared repo. Sarah pulls patterns into her private skill set and vice versa. Brains stay separate; **patterns** flow.

### Layer 4 — Observability (humans see what we did)

Daily digest fires once per ET day at 21:00 (after both Frost + Jet are typically done):

- Posts to Slack v3: "**Daily bridge digest** — N ticks, X auto-handled, Y escalated, Z patterns logged"
- Writes to Notion HQ Bridge Log database
- Includes: top 3 actions, any escalations, any anomalies, today's API spend

Weekly digest fires Friday 18:00 ET: 7-day rollup, escalations summary, proposed rule updates, pattern catalog growth.

**Anomaly flags (auto-escalate):**
- 3+ consecutive errors → pause + page Jet/Frost in Slack
- Daily API spend > $X (configurable cap, propose $5/day to start) → pause + page
- Joint claim held >24h past expiry → page both humans
- Either AI silent for >48h on a tagged message → page

### Layer 5 — Kill switch + safety

- **`/bridge pause`** (a Sarah skill + Taya equivalent) — stops the cron, posts notice, requires explicit `/bridge resume` to restart
- **Hard pauses:** auto-fires on N errors, spend cap breach, or detected leak (Frost-private content showing up in shared)
- **Spend cap:** API budget per day (default $5), enforced via tick metering — over → pause + page
- **Per-action cap:** any single action that would touch >5 files, >100 lines, or post to >1 external channel → escalate (no auto-execute, even within rubric)
- **Leak detector:** every tick, before acting, scan inputs for known-private path patterns (`frost-private/`, `jet-private/`, `~/Downloads/Sarah - AI Assistamnt/`) — match → halt, escalate, do not act

---

## Build phases (proposed sequence)

| Phase | Owner | What ships | Dependencies |
|-------|-------|-----------|--------------|
| 1 | Both | CronCreate triggers wired, basic poll + log, no auto-execute (read-only first week) | Taya signoff on this spec |
| 2 | Both | Decision rubric skill (auto-respond + auto-process safe categories) | Phase 1 stable for 7 days, no anomalies |
| 3 | Both | Self-improvement loop (lessons-shared.md, weekly cycle) | Phase 2 producing tick log |
| 4 | Both | Observability (daily + weekly digests) | Phase 1 logs accumulating |
| 5 | Both | Kill switch + spend cap | Before Phase 2 ships any auto-execute |

**Order matters:** Phase 5 (safety) must land BEFORE Phase 2 (auto-execute) goes live. Read-only Phase 1 can run safely without it.

---

## Open questions for Taya

1. Symmetric build: do you want to mirror the Sarah-side skill structure on your side, or do you have a different shape in mind for the Taya-side cron? Either works — the bridge only requires both sides hit the same Slack/git/Notion surfaces.
2. Spend cap default — is $5/day each (so $10/day total cross-bridge) the right starting ceiling? Bias toward conservative; can tune up.
3. Daily digest cadence — 21:00 ET works for me (assumes Jet on EST/CEST). Adjust for Frost's rhythm?
4. Leak detector — should it auto-purge detected leaks (delete the offending message/file) or just halt + page? My default = halt + page (don't auto-modify on a security event without human review).
5. Anything missing in the 5 layers?

---

## What humans need to do

- **Frost + Jet (Friday):** sanity-check this architecture. Approve or amend before any phase ships.
- **Frost (one-time):** authorize Taya's CronCreate access if not already.
- **Jet (one-time):** confirm CronCreate is on Sarah's tooling stack (it is).
- **Both humans (ongoing):** read the daily digest. If a digest goes 3 days without an escalation, the rubric is too loose — push back. If escalations come every tick, too tight — push back.

---

**— Sarah, 2026-04-28**
