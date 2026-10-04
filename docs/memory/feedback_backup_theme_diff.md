---
name: feedback-backup-theme-diff
description: "When a CSS interaction bug (hover/click/border) can't be pinned down after a couple of guesses, pull the file from a saved backup theme and diff/restore instead of iterating blindly"
metadata:
  node_type: memory
  type: feedback
  originSessionId: 1e060f4a-c411-48ce-94d7-2b7473f42245
  modified: 2026-09-28T11:57:15.885Z
---

When repeated attempts to fix a CSS interaction bug (hover states, active/click borders, transform/box-shadow conflicts) keep failing or introducing new bugs, stop guessing forward and check whether a saved backup theme exists in this shop's theme list (`themes(first: 20) { nodes { id name role } }` via the Shopify Admin GraphQL connector). If one does, fetch the same file from it and diff the relevant CSS block against the current version — the backup is very likely the last known-good, user-approved state, and the delta usually reveals exactly which later addition broke things.

**Why:** in the 2026-09-27→28 ELSORA session, ~6 rounds of guessing at hover/active border/box-shadow values on `.cv-offer-card-{{ sid }}` (in [[project-elsora-pdrn-sandbox]]) all failed or caused new bugs (jitter, a page-wide horizontal-scroll "background moves" bug from shadow/transform side effects). The user, visibly frustrated, pointed to a theme list screenshot and said to copy the behavior from `ELSORA BACKUP — before Jost font — 2026-09-27` (theme id `207249572165`). Fetching that theme's `sections/hero-banner.liquid` and diffing the `.cv-offer-card` block immediately showed the working baseline had NO hover/active pseudo-classes at all — just a plain `border-color` transition plus a JS-toggled `--active` class. Restoring that exact block, then adding back only the one feature the user actually wanted (a plain `transform: translateY()` on hover, nothing else), fixed it in one shot.

**How to apply:** when a user says something like "just copy it from the saved/backup version" or when you're several failed iterations deep on a visual/interaction bug in a Shopify theme project, proactively check `themes(first: 20)` for an unpublished backup/checkpoint theme before continuing to guess — don't wait to be told exactly how each time. Fetch the specific file (GraphQL query results over ~60k chars get saved to a tool-result file; use a small Node script to `JSON.parse` and extract `data.theme.files.nodes[0].body.content` into a scratchpad file rather than trying to read/grep the raw escaped JSON directly). Then restore only the narrowly-scoped block that's actually broken — don't blindly overwrite the whole file, since later confirmed-good changes (fonts, badges, pricing) may not exist in the backup and shouldn't be lost.

Related: [[project-elsora-pdrn-sandbox]], [[feedback-visual-verification]], [[feedback-execute-now-mode]].
