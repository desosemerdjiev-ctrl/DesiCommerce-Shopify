---
name: feedback-direct-instructions-preferred
description: User now writes instructions directly in this chat instead of pre-processing them through ChatGPT first
metadata: 
  node_type: memory
  type: feedback
  originSessionId: 1e060f4a-c411-48ce-94d7-2b7473f42245
  modified: 2026-09-18T12:25:41.127Z
---

The user will write task instructions directly here from now on, instead of typing them into ChatGPT first to get a "precise prompt" and relaying that prompt to Claude Code.

**Why:** the ChatGPT-relay workflow only produced a correct/complete result "in ~20% of cases" (per the user's own words) — the intermediary rewriting apparently lost or distorted intent. In this session (2026-09-18), a long string of direct, literal instructions typed straight into this chat — hero gallery vertical alignment, How-To-Use image replacement + mobile sizing, header mint background + shadow gradient + shadow reduction — were all executed with the user confirming zero misses ("njama neshto koeto da ne napisah tuk i da ne be izpalneno" — there's nothing I wrote here that wasn't done). The user explicitly attributed this to reading their own exact wording directly, without a paraphrasing layer in between.

**How to apply:** treat the user's literal message text in this chat as the authoritative, primary instruction — not a summary or reinterpretation of it. This reinforces (doesn't replace) the existing working discipline already established and validated this session: inspect the actual current code/state before touching anything, never guess a pixel value or color when an exact one already exists in the codebase to reuse, verify every push byte-for-byte against intended content before reporting success, and ask a clarifying question when genuinely blocked by ambiguity (e.g. which of several plausible referents a short follow-up message means) rather than guess and risk another correction round. See [[project-elsora-pdrn-sandbox]] for the concrete architecture/state this discipline has been applied to, and [[feedback-visual-verification]] / [[feedback-execute-now-mode]] for related standing behavioral rules.
