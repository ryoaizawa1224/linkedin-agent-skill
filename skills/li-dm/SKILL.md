---
name: li-dm
description: >-
  Write connection notes and DM follow-ups that get replies - the invite note,
  the first message, and the follow-ups. Use when the user says "write a
  connection request", "DM this person", "outreach message", "how do I follow
  up", or is reaching out to someone specific on LinkedIn.
---

# li-dm

Get the specifics first: who the person is, the real reason to reach out now, and what the user ultimately wants.

Write a short invite note, then a concise first message that references the same specific context and gives something before asking. Follow-ups should add new value rather than just bumping the thread.

Never fabricate a mutual connection, shared history, or having read something the user has not read. Never automate sending or connection requests.

## Output

Return the invite note with character count, the first message, and follow-ups with suggested timing. Invoke `$li-human` on all outbound text. The user sends every message manually.
