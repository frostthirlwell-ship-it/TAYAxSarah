# Cold-Caller Playbook (joint draft)

**Status:** Frost-side first pass by Taya. Sarah to add technical surface (dialer interface, disposition codes, GHL workflow). Cross-review + merge before Frost's hires start May 1.

**Authors:** Taya (operator-behavior framing) + Sarah (technical surface — pending)

---

## Why this exists

Frost is hiring 2 PH setters + 1 Toronto caller for Summit outbound, target start **May 1**. Sarah confirmed Apr 28 the Summit Dialer is production-ready (`summit-dialer-production.up.railway.app`) and these will be the first production users. This playbook is what each hire reads on day 1 to know what they're doing and how to do it well.

The playbook covers operator behavior. Sarah's section covers the technical surface (how to log into the dialer, what disposition codes do what, the GHL workflow that fires post-call). Together = day-1 ready hire.

---

## Operator role + responsibility (Frost-side framing)

**Title:** Summit Outbound Caller (PH setter / Toronto caller)
**Reports to:** Jet (day-to-day delivery + escalations) once handed off post-onboarding
**Compensation:** [Frost: confirm structure — $/hr base + booked-call commission?]
**Primary KPI:** booked audit calls per shift (not "calls made" — booked outcomes only)
**Secondary KPI:** reply-rate on warm-handoff text after no-answer

---

## What you're calling about (the offer in plain language)

You're calling home-service business owners. The pitch in 90 seconds:

> "Hey [Name], this is [Caller] from Summit. Quick reason for the call — we work with home-service operators on growth systems. Your business showed up in our research because [trigger reason — Sarah's lead enrichment fills this]. We're booking 30-min audit calls this week with operators who fit our profile. Worth 30 min on your calendar?"

The product:
- **$9K flat fee** (NOT $5K — that's old pricing, ignore any old reference)
- 90-day implementation: cold outreach engine + dialer + GHL automations + ad creative + audit-call delivery system
- 90-day ROI guarantee (specific terms in the contract — reference the audit call deck)
- Limited to 25 operators total. **10 currently signed. 15 seats left.** Use scarcity, don't fake it.

If they ask "what's it cost" before you've earned the audit booking → "I'd love to give you a real number, but the audit call is where we look at your specific setup and price the right scope. 30 min on the calendar — what's tomorrow morning look like?"

---

## How a normal call goes

**0-10 sec:** identify yourself. "Hey [Name], this is [Caller] from Summit AIS." Wait for "yeah" / "who?" / "what?"

**10-30 sec:** the reason. "Quick reason for the call — we [specific to their business, sourced from Sarah's lead enrichment]." Permission test: "Got 30 seconds?"

**30-90 sec:** the offer or the qualifying question. If you have a clear hook, give it. If not, ask the qualifying question Sarah's enrichment surfaced (e.g. "I see you're running [X service area] — are you doing your own marketing or working with an agency?").

**90 sec - 3 min:** the audit-call ask. Goal is a calendar booking. Not a pitch. **You are not closing them on $9K — you are closing them on 30 min with Frost or Jet.**

**3 min+:** they'll either say yes (book it), no (move on), or "tell me more" (book the audit anyway — "perfect, that's exactly what the 30 min is for").

---

## Disposition codes (Sarah — fill in technical surface here)

What you log after every call. The codes here drive Sarah's GHL workflow which determines what happens next (re-call queue, warm text, email follow-up, dead lead, etc).

**Sarah-side: paste the disposition code table here. What I need from you:**
- Code → what it means → what GHL does next
- Decision tree: "if no answer → which code; if voicemail → which code; if booked → which code"
- How to log in the dialer UI

---

## "Warm" vs "cold" outcome — definitions

This is the framing Sarah asked for. Operators need to know which outcomes go in which bucket so they don't sandbag the disposition codes (warm-coding everything kills the GHL workflow's accuracy).

**WARM:**
- Booked audit call (any future date) → **W-BOOK**
- Asked for callback at specific time → **W-CB**
- Asked for email with details → **W-EMAIL**
- Genuinely interested, asked good questions, but not ready today → **W-NURTURE**

**COLD:**
- Hard no, told you to fuck off → **C-DEAD**
- Wrong number / not the decision-maker → **C-WRONG**
- Already working with another agency → **C-COMPETITOR**
- Out of business / wrong vertical → **C-NOFIT**

**NEUTRAL (default to NEUTRAL when unsure):**
- Voicemail, no callback context → **N-VM**
- Brief skeptical response, didn't engage → **N-SKEPTIC**
- "Maybe later, busy now" without specifics → **N-LATER**

**The discipline:** if a call could be coded WARM or NEUTRAL, code it NEUTRAL. We'd rather under-warm than over-warm. The auto-followup sequences depend on this signal being accurate.

---

## What success looks like in week 1

- 10-15 calls/hour during 8am-6pm ET window (PH setters paced higher than Toronto caller — different scripts)
- 1-2 booked audit calls per shift = above-average
- 3+ booked audit calls per shift = top performer
- Zero "fake-warm" disposition codes (Sarah will spot-check the GHL workflow output)
- Read the daily Slack thread Jet posts about pipeline state — context matters

---

## When to escalate to Jet

🔴 **Same-shift escalations** (text/Slack Jet immediately):
- Operator on the phone wants to talk to a human now
- Caller says something that could legally bind Summit (pricing promise, guarantee outside the standard 90-day, comp structure for an introducer)
- Caller asks something you don't know the answer to about Summit

🟡 **End-of-shift escalations** (log in dispo notes, daily digest covers it):
- Pattern: "every operator in [X niche] asks the same question and our script doesn't handle it"
- Pattern: "the GHL warm-text isn't landing — operators not seeing it"
- Pattern: "list quality is weak — too many wrong numbers"

🟢 **Just handle**:
- Standard hard-nos
- Voicemails (just code N-VM, GHL handles)
- "Send me an email" → log W-EMAIL, sequence fires

---

## What Sarah's GHL workflow does after each disposition

**Sarah — fill in here. Specifically:**

For each disposition code above, what GHL workflow fires:
- W-BOOK → calendar event created → audit-call confirmation email + SMS + Frost/Jet calendar invite
- W-CB → ?
- W-EMAIL → ?
- W-NURTURE → 7-day nurture sequence?
- C-DEAD → dead-lead bucket, no further outreach for 6 months?
- N-VM → 24-hour callback queue?
- (etc — your call on the right tree)

Operators need to know what happens after they hang up so they trust the system + don't double-message leads.

---

## Tools you have

**(Sarah — fill in technical specifics here. What I expect:)**

- **Dialer:** `summit-dialer-production.up.railway.app` (login flow, Twilio number assigned to you, queue UI)
- **GHL:** Summit AIS sub-account, your role + permissions
- **Slack:** `#summit-callers` channel for shift coordination (does this exist? Sarah, confirm)
- **Notion:** read-only access to the lead enrichment view (Sarah's clients DB filtered for caller-relevant fields)

---

## Standing rules

- **Never lie to a prospect.** Especially about pricing, timeline, or guarantee terms.
- **Never quote pricing on a cold call.** "$9K flat" only on the audit call after qualification.
- **Never promise a callback you can't deliver.** Use W-CB only if you can actually call back at that time.
- **Recording disclosure:** [Sarah — confirm Twilio recording config + what we tell prospects. Default in Ontario is one-party consent, but check Summit's policy.]
- **DNC compliance:** If a prospect says "remove me," code C-DEAD + flag for Sarah's DNC list. No re-outreach ever.

---

## What humans need to do before May 1

**Frost:**
- Confirm comp structure (base + commission?) — this is currently `[TODO]` above
- Approve final operator titles + reporting line
- Buy 3 Twilio CA numbers (~$1/mo each) from Twilio console under Summit's account — Sarah can spec exact numbers once you authorize
- Final review of this playbook before printing for hires

**Jet:**
- Confirm `#summit-callers` Slack channel exists or create it
- GHL API key rotation (still pending — affects post-call disposition sync, not call placement)
- Sign off on disposition codes once Sarah fills them in

**Sarah:**
- Fill in disposition code table + GHL workflow per-code
- Spec the 3 Twilio numbers Frost should buy
- Confirm recording disclosure language for Ontario calls
- Confirm tools section (any I'm missing)

**Taya:**
- Iterate operator behavior framing based on Sarah's technical surface
- Pull in script v2 from `references/scripts/summit-audit-call-home-service.md` (mid-call → audit-call handoff language)
- Add caller-onboarding checklist (day 1, day 7, day 30)

---

## Process for finalizing this playbook

1. Sarah PRs her technical surface onto `sarah/cold-caller-playbook-tech` branch (off `taya/cold-caller-playbook`)
2. Cross-review: Taya reviews Sarah's PR, Sarah reviews Taya's
3. Merge to main once both AIs sign off
4. Frost + Jet sanity-check Friday before printing
5. Hires read on day 1 (May 1)

---

*First push: 2026-04-28 by Taya (operator behavior framing). Sarah to add technical surface.*
