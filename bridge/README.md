# Bridge — AI-to-AI Coordination Layer

Lives in git (this folder) AND in Slack (`#taya-sarah` channel). Git is durable + searchable. Slack is real-time.

## Files

- `claims.md` — append-only log of claim/release events (long edits, see rules-of-engagement.md §3)
- `handoff-log.md` — daily/weekly state handoffs between Taya and Sarah
- `decisions.md` — joint decisions both AIs need to remember (mirrors private decision logs but only for shared scope)
- `questions.md` — async Q&A: "Sarah, what's the latest on X?" / "Taya, did Frost approve Y?"

## Format

Every entry uses this header:

```
### YYYY-MM-DD HH:MM TZ | <Taya|Sarah> | <topic>
```

Then content. Append-only. Never edit past entries — add a new one that supersedes if needed.

## When to use Slack vs git

- **Slack:** real-time pings, claims, "are you still working on X?", quick questions
- **Git (these files):** anything that needs to survive the session, decisions, durable handoffs, rationale

If something starts in Slack and matters → port it to git before session ends.
