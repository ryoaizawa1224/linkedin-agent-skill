---
name: li-audit
description: >-
  Post-mortem on what the user has already published - which posts actually
  worked, why, and what to stop doing. Use when the user pastes their LinkedIn
  analytics or past posts and asks "what's working", "why did this flop", "read
  my analytics", "audit my content", or wants to know what to double down on.
---

# li-audit

The only honest source of what works for an account is that account. Every rule in every LinkedIn guide, including the ones in this pack, is a prior. The user's own last 30 posts are the evidence.

## Input

Ask for whichever the user has:

- The post analytics export (LinkedIn: Analytics -> Content -> Export). CSV.
- Or a screenshot per post with impressions, reactions, comments, reposts.
- Or just the posts and their reaction counts, which is enough for a first pass.

Also read `~/.codex/linkedin/log.md` if it exists, since it records which hook formula each post used.

## What to actually measure

Compute and show engagement rate, comment ratio, reach multiple, and save/send rate when available. Rank by engagement rate and reach multiple, not raw impressions.

## Then find the pattern

Compare the top 5 and bottom 5 across hook formula, format, length, theme, day/time, and first-hour replies. State findings as claims with evidence and confidence. With too few posts, say the sample is too small rather than inventing a pattern.

## Output

Summarize the strongest signals, what to stop doing, and what to do more of. Then hand the conclusions to `$li-plan` so next week's plan is built on the user's own evidence rather than defaults.
