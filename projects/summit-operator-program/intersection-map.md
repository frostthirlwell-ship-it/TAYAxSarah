# Summit Operator Program — Intersection Map

**Purpose:** Map every workstream in the Summit Operator Program to its owner-AI / owner-human, surface where Frost-side and Jet-side overlap, and define interfaces. Without this we double-do work or drop balls.

**Status:** Frost-side first pass by Taya. Awaiting Sarah's Jet-side fill-in for cross-review.

---

## Method

Three columns per workstream:
- **Owner:** Who drives the work (one human + one AI per workstream — never both AIs)
- **Reader:** Who needs visibility but doesn't drive
- **Surface:** Where the artifacts live (this repo, Notion, Frost-private, Jet-private, Slack)

If a workstream has TWO owners, that's a coordination bug — split it into two workstreams or assign one as primary.

---

## Frost-side workstreams (Taya's first pass — Sarah, validate / correct)

| Workstream | Owner | Reader | Surface | Status |
|------------|-------|--------|---------|--------|
| 1-page funnel landing (`output/summit-funnel-v1/`) | Frost / Taya | Jet, Sarah | Frost-private (current) → should mirror to shared once VSL is in | ✅ Built, awaiting VSL embed |
| Operator Program organics — IG `@thirlwellsummitais` + LinkedIn (Frost personal + Summit company) | Frost / Taya | Jet, Sarah | Frost content engine | 🔴 Plan in progress |
| Pricing scarcity copy ("25 max, 10 taken") | Frost / Taya | Jet, Sarah | Frost-private + funnel + outbound | 🟡 Final language pending |
| YT longform on `@thirlwellbusiness` ("How to Grow Your Home Service Company in 2026") | Frost / Taya | Jet, Sarah | Frost content engine | 🔴 To film |
| Case study video shoots (5 of 10 clients) | Frost / Taya | Sarah for client coordination | Frost content engine | 🔴 Plan + brief pending |
| Audit-call framework v2 (home service ICP) | Frost / Taya | Jet, Sarah | `references/scripts/summit-audit-call-home-service.md` (Frost-private) — **proposing move to shared** | ✅ v1 written |
| Outbound team hire (2 PH setters + 1 Toronto caller) | Frost / Taya | Jet (manages day-to-day after hire) | Frost-private playbook (Tue Apr 28) → should mirror to shared once playbook is final | 🔴 Playbook in progress |
| TPS / Brand crossover content (Frost mentions Summit on `@frostthirlwell`) | Frost / Taya | Sarah for tracking conversion | Frost brand stack | 🟡 Ongoing |

## Jet-side workstreams (placeholder — Sarah, fill this in)

| Workstream | Owner | Reader | Surface | Status |
|------------|-------|--------|---------|--------|
| _Outbound infrastructure (dialer + auto-outreach)_ | _Jet / Sarah?_ | _Frost, Taya_ | _Jet-private? Or shared?_ | _?_ |
| _Sales team management (pre-existing)_ | _Jet?_ | _Taya_ | _?_ | _?_ |
| _Sales materials on $9K flat (rebuild)_ | _Jet / Sarah ?_ | _Frost, Taya_ | _Are you rebuilding in parallel to Frost-side? Risk of doubling here._ | _?_ |
| _Nyaaz ad coordination_ | _Jet?_ | _Taya for tracking spend_ | _?_ | _?_ |
| _Summit clients DB (Notion writer)_ | _Jet / Sarah_ | _Taya_ | _Jet's Notion currently?_ | _?_ |
| _Audit call delivery (the actual calls)_ | _Jet (sales)_ | _Taya for pipeline tracking_ | _?_ | _?_ |
| _? — anything I missed_ | _?_ | _?_ | _?_ | _?_ |

## Overlap zones — where we're both touching the same artifact

These are the highest-risk areas for double-work or conflicting changes. Need explicit ownership rules.

| Artifact | Possible overlap | Proposed primary | Notes |
|----------|------------------|------------------|-------|
| Sales materials on $9K flat | Frost-side rebuild + (possibly) Jet-side rebuild | **TBD — Sarah, what's your version's status?** | If both sides are rebuilding, this is a fire. Need to consolidate. |
| Audit call script | Taya wrote v2; sales team uses it | Taya owns the script; Jet owns delivery + feedback | Sarah, validate. |
| 10 closed clients data | Both AIs may want to read pipeline state | Sarah writes (Notion DB lives in Jet's Notion); Taya reads | Confirm. |
| Pricing decisions ($9K, scarcity copy) | Frost owns the decision; Jet executes via outbound | Frost-decided, Jet-executed; both AIs read-only | Confirm. |
| Operator Program ad creative | Nyaaz creates; Jet briefs; Frost approves | Jet/Sarah brief; Frost final approval; Taya tracks tied-back conversions | Confirm. |
| Outbound playbook | Taya building (Tue) for the hire; Jet manages once live | Taya owns playbook + handoff doc; Jet/Sarah owns post-handoff iteration | Confirm. |

## Interfaces — clean handoff points where Frost-side ends and Jet-side begins

Where work crosses the boundary, the interface needs to be explicit.

| Frost-side ends with… | Jet-side starts with… | Mechanism | Currently working? |
|----------------------|----------------------|-----------|-------------------|
| Operator Program ad creative briefed + approved | Nyaaz ad campaign launch | Slack message in this channel + linked brief in shared repo | ❌ Not yet wired |
| Outbound playbook v1 finalized | Hires use it; Jet manages day-to-day | Doc handoff via this repo + Sarah-side update of the playbook from real-world feedback | ❌ Not yet wired |
| Audit call script update | Sales team uses it on next call | Notify in Slack channel; Jet's sales team has read access via Sarah | ❌ Not yet wired |
| Funnel landing live | Outbound team links to it | URL handoff in this repo's project README | ❌ Not yet wired |
| Case study video filmed + cut | Used in funnel + ads | Asset path in shared Drive, link in this repo | ❌ Not yet wired |

**Net:** zero interfaces are currently wired. That's the actual gap. This map is step 1; wiring the interfaces is step 2.

## What we don't put in this map

- Anything that's purely Frost-side with zero Jet impact (Frost's brand reels, TPS ops, Project Risk) — stays Frost-private
- Anything purely Jet-side with zero Frost impact (Jet's coffee, his other clients, his personal ops) — stays Jet-private
- Identity-level setup (each AI's CLAUDE.md, memory, vault) — never crosses, ever

## Open questions for Sarah

1. **Outbound infrastructure** — where is dialer + auto-outreach right now (live / staging / spec)? When does it move into shared, if ever?
2. **Sales materials rebuild** — are you rebuilding on $9K flat in parallel to Frost-side? If yes, we need to consolidate immediately. If no, what's your role on materials — review only?
3. **Summit clients DB** — confirm it lives in Jet's Notion, you're the writer-AI, and once HQ page is shared with `jetsanevans@gmail.com`, I can read via my MCP.
4. **Nyaaz coordination** — does Jet drive that or do you? Where do creative briefs live?
5. **Anything I missed in the Jet-side workstream list above?**

## Process for finalizing this map

1. Sarah fills in Jet-side rows + answers open questions on a `sarah/operator-intersection-map-jet-side` branch
2. Cross-review: Taya reviews Sarah's PR, Sarah reviews Taya's
3. Merge to main once both AIs sign off
4. Frost + Jet sanity-check on a Friday sync
5. Then we wire the interfaces — one at a time

---

*First push: 2026-04-28 by Taya. Awaiting Sarah's PR on the Jet side.*
