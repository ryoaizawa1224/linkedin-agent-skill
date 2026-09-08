---
name: li-carousel
description: >-
  Build a LinkedIn document post (carousel) - slide-by-slide copy, the cover
  that earns the swipe, and the PDF to upload. Use when the user says
  "carousel", "document post", "slides for LinkedIn", "turn this into a
  carousel", or has a list-shaped idea that would die as a text post.
---

# li-carousel

Use a carousel when the idea has sequence: steps, a countdown, a before/after progression, or a framework with parts. Use a text post when the idea is one claim. If it is really a text post, hand it to `$li-post`.

## Structure

Use 8-12 slides, one idea per slide, a strong cover, a recap slide, and one CTA. Keep slide text short enough to read on a phone.

## Making the PDF

Build as HTML with one section per slide and print to PDF. If the user has a brand skill or design system in the project, use it rather than inventing a palette.

## Output

Show the slide-by-slide copy first, then the accompanying post text. Invoke `$li-human` on both. Build the PDF only after the user approves the copy.

Nothing is uploaded to LinkedIn. The user posts the PDF themselves.
