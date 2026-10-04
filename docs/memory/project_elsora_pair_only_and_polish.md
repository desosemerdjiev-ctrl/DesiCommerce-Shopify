---
name: elsora-pair-only-and-header-polish
description: "State of the ELSORA draft theme (205328908613) after pair-only conversion, marquee bar, heading shadows and cart-bag icon; what is approved vs. unverified"
metadata:
  node_type: memory
  type: project
  originSessionId: 1e060f4a-c411-48ce-94d7-2b7473f42245
  modified: 2026-10-03T20:53:30.039Z
---

Draft theme `gid://shopify/OnlineStoreTheme/205328908613` only (never live/backups; publish is manual by the user). Backup "PREDI PAIR-ONLY" = 207703572805.

Done and approved by the user (2026-10-03):
- Product has only 2 variants, now "Silver Pair" $54.99 / "Gold Pair" $57.99 (no compare-at, both automatic discounts deleted). Hero shows 2 cards, Gold pre-selected, final-cta initialises with Gold variant 59209490268485. TeamDrop mapping is the user's job.
- Sandbox-only polish: scrolling announcement bar (`sections/announcement-bar.liquid`), soft heading text-shadows via tokens in `snippets/elsora-design-tokens.liquid`, wide beach-tote cart icon `assets/icon-bag-elsora.svg` (colours `#9F9DF5` outline/top band/outer arc, mint `#C7EFE0` animated wave; alt variant `#8C8AF2` was tried and rejected).
- Hero image vertical alignment compensates for the removed second card row (alignGalleryBottom in hero-banner.liquid).

**Why:** the storefront is password-protected, so Claude cannot view it; the user checks visually and sends screenshots.
**How to apply:** never claim a visual result as verified; judge fonts on the real storefront preview URL, not the theme editor (editor falls back to Arial instead of Jost). Pending text-audit items (e.g. "Keep both globes together", FAQ wording) are for the user to reword.
