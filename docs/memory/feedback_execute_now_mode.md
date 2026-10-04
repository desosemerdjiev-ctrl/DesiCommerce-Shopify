---
name: feedback-execute-now-mode
description: "When user says \"EXECUTE NOW\" / \"do not ask another question\" they want direct action, not another plan or audit"
metadata: 
  node_type: memory
  type: feedback
  originSessionId: 1e060f4a-c411-48ce-94d7-2b7473f42245
  modified: 2026-08-29T21:12:19.344Z
---

When this user prefixes a request with language like "EXECUTE NOW," "do not ask me another question," "do not create another audit," "do not give me a plan first" — treat it as a hard instruction to make the actual file edits immediately, using judgment calls for any ambiguous details, rather than pausing to confirm scope or re-explaining the problem.

**Why:** Across several turns in the [[project-elsora-pdrn-sandbox]] work, the user escalated with increasingly explicit "do not ask / do not audit / do not explain, just fix it" instructions after prior responses spent turns re-investigating or re-confirming things already established. They want the visible artifact (rendered page, working feature) to change, not a longer explanation of why it's hard.

**How to apply:** In this mode: (1) do light, necessary investigation only (e.g., re-reading a file to avoid overwriting unseen edits) — don't narrate it as an audit, (2) make the edits directly, (3) keep the final report short and factual per whatever format they specify, (4) still surface a genuine hard blocker (e.g., "I can't authenticate into Shopify Admin") rather than papering over it, since that's a fact they need, not a request for permission.
