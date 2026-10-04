---
name: feedback-visual-verification
description: "User requires actual rendered/visual verification for UI-visible work, not source-code-only confirmation"
metadata: 
  node_type: memory
  type: feedback
  originSessionId: 1e060f4a-c411-48ce-94d7-2b7473f42245
  modified: 2026-09-27T15:55:16.013Z
---

Never claim a visual/UI fix is "verified" or "done" based only on reading deployed source code or config values — even when the code is unambiguously correct. This user has repeatedly rejected reports that read "confirmed via re-reading deployed files" as insufficient proof, because the actual Shopify Theme Editor render still showed the old broken result (stale cache, wrong architecture assumption, etc. — reading the file doesn't catch every real-world rendering gap).

**Why:** During the [[project-elsora-pdrn-sandbox]] work, multiple "completion reports" claimed a fix landed based on re-fetching the theme file via the Admin GraphQL API and confirming the text/values were correct. The user pushed back hard each time with real screenshots proving the rendered page still showed the old behavior — root causes turned out to be real architectural bugs (e.g., a global Liquid variable hardcoded instead of routed per-template, a wave-loop animation that wasn't actually seamless despite looking correct on paper) that only became visible by comparing the actual render against source.

**How to apply:** For any task with a user-visible/rendered outcome (UI, animation, layout, color), explicitly state whether the reported fix was visually confirmed in a real browser/render, or only confirmed via source inspection. If browser-based verification is blocked (auth, tooling), say so plainly and don't imply visual success. When the user says "do not claim X is fixed simply because a token/value exists in the file," take that literally — describe the code change and its intended effect, but do not use words like "fixed," "resolved," or "done" for the visual outcome itself unless it was actually seen rendering correctly.

**Update 2026-10-04 — storefront is password-protected; visual checks are done by the user:** the storefront (elsora.store) is password-protected (pre-launch). Claude never enters or searches for the storefront password and cannot view the rendered storefront or preview URLs itself. All visual checks are done by the user, who sends screenshots. Report what was changed in code and state plainly that the visual result is not verified until the user confirms it from a screenshot.
