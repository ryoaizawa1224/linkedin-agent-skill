---
name: li-profile
description: >-
  Score a LinkedIn profile out of 100 against a 12-part rubric and rewrite the
  parts that lose points - headline, about, experience, featured, banner. Use
  when the user says "optimize my profile", "score my LinkedIn", "rewrite my
  headline", "fix my about section", or pastes their profile and asks how it
  reads.
---

# li-profile

A profile is not a resume. A resume answers "what have you done". A profile answers "should I message this person" from the headline and first lines of the about section.

## Input

Ask the user to paste their headline, about section, current role, recent experience, and whether they have a banner and featured section. A screenshot of the top card is enough for a first pass. Do not log into LinkedIn on their behalf.

## Score it

Read `rubric.json` in this folder. Score every item, show the table, and give the total.

## Rewrite order

Fix in descending order of points lost:

1. Headline
2. About first two lines
3. About body
4. Featured
5. Experience
6. Banner

Keep claims factual and do not invent proof or metrics.

## Output

Show the score table and copy-ready rewrites in fix-first order. Invoke `$li-human` on every rewritten text block. Re-score at the end and show the delta honestly.

Nothing is saved to LinkedIn by this skill. The user pastes each section in.
