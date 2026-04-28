# Summit Audit-Call Script — Single Source of Truth

**Status:** Live, in use by Jet's sales team.
**Owner:** Taya (script content + iterations)
**Reader / consumer:** Sarah (blueprint-builder skill auto-pulls latest before each booked call)
**Co-maintained:** Jet provides delivery feedback via PR comments; Taya iterates the script.

This is the canonical Summit audit-call framework for the home-service ICP ($500K–$5M revenue band). Moved from Frost-private (`references/scripts/summit-audit-call-home-service.md`) to shared per the intersection map agreement (Apr 28).

## How to use

**If you're a Summit sales caller (Jet's team):**
- Don't read this directly during a call. Sarah's `blueprint-builder` skill generates a per-prospect blueprint that injects the relevant sections into a custom doc.
- After your call, log feedback in `bridge/audit-call-feedback.md` (or PR a change directly if you spotted a fixable issue).

**If you're Taya iterating the script:**
- Branch `taya/audit-script-vN` with the change
- Reference what triggered it (specific prospect's question, observed pattern across 3+ calls, new offer info)
- Sarah cross-reviews — she sees the call delivery patterns, may flag if the change conflicts with sales-team feedback she's tracked
- Merge to main → Sarah's blueprint-builder picks up next blueprint generation

**If you're Sarah pulling the script:**
- Read `audit-call-script-v2.md` (this directory) on every blueprint-builder run
- Last-modified timestamp tells you if there's been an iteration since your last pull
- If you have feedback from a call that should drive a script change, PR a change OR open a `bridge-question` issue tagging Taya

## Iteration loop (closes naturally per intersection map overlap zone #2)

```
Booked call → Sarah generates blueprint (pulls latest script) →
Jet's sales team delivers → Audit-call recording + Sarah's post-call score →
Taya pulls recording, observes outcome → Iterates script → 
Merge → Next blueprint pulls latest. Loop.
```

The recording → script-iteration loop is the highest-payoff interface in the system. Every booked call either reinforces the current script (no change needed) or surfaces a real prospect signal that should change it.

## Versioning

Script is v2 as of 2026-04-28 (current iteration after the $9K-flat rebase + home-service ICP refinement).

Major version bumps go in `audit-call-script-v3.md` etc. — keep history visible. Minor iterations append to v2.

## Frost+Jet sanity-check gate

Major changes (new sections, structural reframes, new pillars) → Friday Frost+Jet sync before merge.
Minor changes (wording tweaks, single-question additions, quantification refinements) → cross-AI PR review only.
