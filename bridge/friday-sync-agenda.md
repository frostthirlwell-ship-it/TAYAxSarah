# Friday Frost + Jet Sync — Agenda

**Date:** Friday, May 1 2026 (or whenever both available)
**Attendees:** Frost, Jet, Taya (taking notes), Sarah (taking notes)
**Estimated time:** 30-45 min
**Prepared by:** Taya (Apr 28, end of training-loop session 1)

This agenda surfaces everything Sarah and Taya ratified or flagged across the Apr 28 working session that needs human sanity-check before going live. Three buckets: ratifications, decisions needed, builds in flight.

---

## 1. RATIFICATIONS — confirm or override before we wire live

These are calls Sarah + Taya made jointly under the rules-of-engagement protocol but explicitly flagged as needing human sign-off (per §5: architectural changes + judgment calls under delegated authority).

### 1.1 Intersection map ratification ([merged](https://github.com/frostthirlwell-ship-it/TAYAxSarah/blob/main/projects/summit-operator-program/intersection-map.md))

| Decision | Joint position | Frost / Jet override? |
|----------|---------------|----------------------|
| Sales materials → Frost owns rebuild, Sarah review-only (NOT parallel) | Both AIs agree | ☐ Confirm / ☐ Override |
| Audit-call script v2 → moves to shared, Taya owns SoT, Jet owns delivery + feedback | Both AIs agree | ☐ Confirm / ☐ Override |
| Outbound code stays Jet-private, spec + handoff doc move to shared | Both AIs agree | ☐ Confirm / ☐ Override |
| Pricing $9K flat → Sarah propagates across Outreach + Dialer copy | Both AIs agree | ☐ Confirm / ☐ Override |
| Lead-delivery interface contract → versioned in shared (Taya pushback) | Sarah originally wanted Jet-private, Taya pushed for shared | ☐ Decide |
| 3 new overlap zones (Ads Dashboard, Audit-call recordings, Onboarding deliverables) | Both AIs agree | ☐ Confirm / ☐ Override |

### 1.2 Audit-call script in shared ([PR open](https://github.com/frostthirlwell-ship-it/TAYAxSarah/tree/taya/audit-script-to-shared))

**Q:** Approve merging audit-call script v2 to shared? Once merged, Sarah's blueprint-builder skill auto-pulls latest before each booked call. Iteration loop closes (booked call → blueprint → delivery → recording + score → Taya iterates → merge → next blueprint).

**Joint AI position:** Yes — interface #1 from Sarah's wiring priority, highest leverage (fires every booked call).

☐ Approve / ☐ Override

### 1.3 Cold-caller playbook ([taya/cold-caller-playbook](https://github.com/frostthirlwell-ship-it/TAYAxSarah/tree/taya/cold-caller-playbook))

**Status:** Frost-side framing pushed (Taya). Sarah-side technical surface pending. Target: ship before May 1 hires start.

Key calls to confirm:
- Comp structure for hires: base + commission? What rate? *(Frost confirms)*
- Operator titles + reporting line: "Summit Outbound Caller" reports to Jet day-to-day post-onboarding? *(Jet confirms)*
- `#summit-callers` Slack channel: exists? If not, create? *(Jet confirms)*
- Recording disclosure language for Ontario calls: one-party consent default OK, or stricter Summit policy? *(Jet confirms)*

---

## 2. DECISIONS NEEDED — humans must call

### 2.1 Always-on bridge architecture ([sarah/always-on-bridge-spec](https://github.com/frostthirlwell-ship-it/TAYAxSarah/blob/sarah/always-on-bridge-spec/bridge/always-on-architecture.md))

**The proposal:** 6-layer architecture for continuous Sarah ↔ Taya coordination via CronCreate heartbeats (15-min cadence), decision rubric, self-improvement loop, observability, kill switch + safety, shared-state divergence detection. Read-only Phase 1 first (7 days), Phase 5 (safety) before Phase 2 (auto-execute).

**Spend implications:**
- $5/day each = $10/day combined = ~$300/mo
- Conservative starting cap, tunable after 2 weeks of telemetry

**Risk:**
- 🔴 Auto-execute without kill switch → trust-breaking errors
- 🟡 Spend cap too tight → ticks getting cut off mid-action
- 🟡 Leak detector misfires → bridge goes down on false positives

**Decisions needed:**

| Question | Joint AI position | Frost + Jet decision |
|----------|------------------|---------------------|
| Approve overall architecture? | Aligned with refinements | ☐ Approve / ☐ Override |
| Spend cap default ($5/day each)? | Conservative is right for week 1 | ☐ $5 / ☐ Other: ___ |
| Daily digest cadence (21:00 ET)? | Matches Frost's rhythm | ☐ 21:00 / ☐ Other: ___ |
| Phase 1 → Phase 2 success criteria | Taya proposed: 0 false-positive escalations + ≤2 missed legit-action events + 0 leak-detector misfires by end of week 1 | ☐ Use this / ☐ Stricter / ☐ Looser |
| Leak detector behavior | Both AIs agree: halt + page, NOT auto-purge | ☐ Confirm |
| Authorize Taya CronCreate access? | Required for symmetric build | ☐ Authorize |

### 2.2 Twilio CA numbers procurement (gates May 1 readiness)

**Frost:** buy 3 Twilio CA numbers (~$1/mo each, $3 total) from Twilio console under Summit's account. Sarah specs exact numbers + assigns post-purchase. Required for the 3 new outbound hires to make calls day-1.

☐ Authorize Frost to buy / ☐ Sarah specs different numbers first

### 2.3 Notion HQ permanent home

**Current state:** "Frost ↔ Jet Shared HQ" page nested under SUMMIT OS in Frost's Notion workspace. Temporary home.

**Options:**
- A) Stay nested under SUMMIT OS (cleanest practical, Jet has access via shared page)
- B) Move to top-level workspace page in Frost's Notion (cleaner conceptually)
- C) Spin up fresh shared Notion workspace, both as members (cleanest separation)

☐ A / ☐ B / ☐ C

---

## 3. BUILDS IN FLIGHT — status updates

### 3.1 Active branches awaiting merge

| Branch | Owner | Status | Next step |
|--------|-------|--------|-----------|
| `taya/audit-script-to-shared` | Taya | Open, Sarah review pending | Sarah signs off → Taya merges |
| `taya/cold-caller-playbook` | Taya | Open, Sarah-side fill-in pending | Sarah PRs `sarah/cold-caller-playbook-tech` → cross-review |
| `sarah/always-on-bridge-spec` | Sarah | Open, NOT merging until Friday gate | Frost+Jet decisions above → either merge with refinements or revise |

### 3.2 Workstream status (Stage 1A)

**Summit:**
- 10 closed clients at $9K flat, 1 audit booked next 7 days
- Sprint target: 5-10 new closes by Apr 30, 15-20 active by May 15
- Outbound team start May 1 (3 hires)
- Dialer LIVE, Outreach LIVE (818-lead queue paced 150/day), Ads Dashboard Phase 2 LIVE

**TPS:**
- ~$15-20K booked Apr 2026
- $80K target April 15 - May 31 (rebase to $60-70K acceptable)

**Pressure Washing:**
- Pre-launch, May 1 birth target

**Personal brand:**
- 11 reels/day cadence, $1,300 USD/mo editor cost
- IG 28.8K → 250K target, YT 2.6K → 100K target

### 3.3 Open actions

| Owner | Action | When |
|-------|--------|------|
| Frost | Buy 3 Twilio CA numbers | Before May 1 |
| Frost | Confirm hire comp structure | Before playbook ships |
| Frost | Final review on cold-caller playbook | Once Sarah-side fills land |
| Jet | GHL API key rotation | Whenever (not blocking) |
| Jet | Confirm `#summit-callers` Slack channel | Before May 1 |
| Sarah | Propagate $9K-flat across Outreach + Dialer copy (ping Taya BEFORE commit for cross-check) | Next session |
| Sarah | Fill 4 placeholder sections in cold-caller playbook | Before Tuesday |
| Sarah | Spec the 3 Twilio CA numbers Frost should buy | Once Frost authorizes |
| Taya | Build `tools/bridge-operator/` Frost-side mirror skill | After Phase 1 architecture approved |
| Taya | PR `lead-delivery-contract.md` skeleton | Next session |

---

## 4. WHAT'S WORKING — patterns to keep

This loop session (Apr 28, ~1 hour active) produced:
- 4 merged PRs to `main` (handshake, intersection-map taya-side, intersection-map sarah-side, lock-in pack)
- 3 active branches awaiting cross-review
- 1 first-cross-AI deliverable shipped (intersection map) without human translation
- Full attribution protocol (`**TAYA:** ... — Taya` / `**SARAH:** ... — Sarah`) active across Slack, PRs, Notion
- Sarah's persistent CLAUDE.md + 3 memory entries installed → bridge survives across her sessions
- Taya's CLAUDE.md cross-AI bridge section + morning-briefing integration → bridge survives across Taya sessions
- Honest, substantive AI-to-AI exchange (no ceremonial filler, real pushback with reasoning, real questions answered)

**The bridge produces work, not chatter.** Friday sync is to confirm + scale, not rebuild.

---

## 5. AGENDA RUN ORDER (suggested)

1. **5 min:** Quick state-of-the-bridge — Frost + Jet read top of this doc
2. **10 min:** Section 1 ratifications (knock through fast — they're mostly aligned)
3. **15 min:** Section 2 decisions (real human calls)
4. **5 min:** Section 3 status check + open action assignments
5. **5 min:** Anything either of you wants to override or change in §1.x

**Total ~40 min** if we move fast on ratifications.

---

*Drafted by Taya, end of cycle 4, 2026-04-28 ~17:50 EDT. Sarah — please cross-review before Friday and PR any additions/corrections to your side as `sarah/friday-agenda-additions`.*
