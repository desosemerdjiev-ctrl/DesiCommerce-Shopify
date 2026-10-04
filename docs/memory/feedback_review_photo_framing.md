---
name: feedback-review-photo-framing
description: Standing rule for review-card photos on the ELSORA PDRN sandbox page — source photos must be shot wider so the fixed-ratio crop shows more background
metadata: 
  node_type: memory
  type: feedback
  originSessionId: 1e060f4a-c411-48ce-94d7-2b7473f42245
  modified: 2026-09-24T12:26:17.061Z
---

Future review photos uploaded to `reviews-grid.liquid` cards must be sourced as wider/further-back shots, not tight close-up selfies.

**Why:** the review card's image slot (`.cv-review-image-{{ sid }}`) is a fixed-ratio box — `width:100%; height:160px; object-fit:cover`. On desktop once the container hits its max-width (viewport ≳1244px), the effective visible window converges on a hard ceiling of about width/2.02 ≈ 470px tall, centered, regardless of what image is uploaded or how it's cropped. A tight selfie (subject filling the full source-photo width edge-to-edge) has no real background pixels left to reveal — repositioning the crop only trades cutting off the forehead for cutting off the chin, it can't add more surrounding room. Confirmed by testing multiple crop positions on a 941×1672px source photo (Jessica L. / r2 review card, 2026-09-24): every reposition sacrificed either the face or the product to gain background, none showed meaningfully more of the room.

**How to apply:** when the user supplies a NEW review photo, check whether the subject already leaves visible margin/background on the sides in the source photo. If the subject fills the frame edge-to-edge (like a close selfie), flag this before cropping — the fixed 2:1-ish slot will not be able to show much environment no matter how it's cropped, and the fix is to ask for (or the user to shoot) a wider-framed photo, not a smarter crop. Do not silently reach for AI outpainting/extension to manufacture more background — the user explicitly declined that (and declined a CSS/layout change to the card's fixed height) in favor of just sourcing wider photos going forward. See [[project_elsora_pdrn_sandbox]] for the sandbox's locked-state rules this sits under.
