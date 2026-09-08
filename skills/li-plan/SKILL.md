---
name: li-plan
description: >-
  Build the week on LinkedIn - what to post, when to post it, and who to engage
  with. Use when the user says "plan my week", "what should I post", "content
  calendar", "I have nothing to post about", or wants a posting schedule and an
  engagement list.
---

# li-plan

The control room. Everything else in this pack executes; this decides what gets executed. Run it once a week, on the same day.

## Input

If `~/.codex/linkedin/voice.md` and `~/.codex/linkedin/log.md` exist, read them. The plan should not repeat a theme from the last fortnight. If they do not exist, ask for:

1. What the user sells, and to whom.
2. The three or four themes they want to be known for.
3. What actually happened this week: a client call, a number, a mistake, a thing they built, an argument they had.
4. Ten to twenty people or companies worth being visible to.

## What to post

Use a balanced mix of proof, opinion, teach, story, and offer. For each slot give the theme, the specific angle drawn from what actually happened this week, and the hook formula number from `li-post/hooks.json` that fits it. Not a topic, an angle.

## When to post

Anchor times to the audience's timezone. Treat timing as secondary to the quality of the hook and the post itself.

## Who to engage with

Build a list of 10 split across reach, peers, and buyers. The goal is useful, genuine engagement, not automated activity.

## Output

Produce a weekly schedule and engagement list. When the user says something like "write Tuesday", invoke `$li-post` for that slot.

Write the plan to `~/.codex/linkedin/plan.md` so the other skills can read it. Nothing is scheduled or posted anywhere; this is a plan and the user runs it.
