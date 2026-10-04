---
name: text-animation-rendering
description: "Moving text must not use transform/will-change/mask-image, and the user reads literal weights against existing site text"
metadata:
  node_type: memory
  type: feedback
  originSessionId: 1e060f4a-c411-48ce-94d7-2b7473f42245
  modified: 2026-10-03T20:53:33.981Z
---

When animating text (e.g. the announcement-bar marquee) do NOT use `transform`, `will-change` or `mask-image`: the browser re-paints the text with grayscale anti-aliasing and the same font looks like a different, paler/bolder font. Animate `left` on a relatively positioned track instead, and set the font family/weight explicitly.

**Why:** the user rejected several "different font" results before the cause was found; they were right that the font looked different.
**How to apply:** match weight to existing page text (hero eyebrow = 400) instead of cycling 300/500; when the user says a colour is "grey", fix glyph rendering/weight rather than only changing the colour value. Apply the saturated black only where asked (bar), never to other headings.

Related: [[elsora-pair-only-and-header-polish]]
