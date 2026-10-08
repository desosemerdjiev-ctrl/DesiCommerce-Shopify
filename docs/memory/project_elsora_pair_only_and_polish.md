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

**Update 2026-10-08: cart restyle (NOT yet visually verified by the user).** Backup before it: theme `208089940293` "BACKUP before cart restyle 2026-10-08" (made with the `themeDuplicate` mutation, which works through the connector).
- ELSORA scope now = `template.suffix == 'pdrn-sandbox' or template.name == 'cart'` in `layout/theme.liquid` (ice-globes palette + Jost), `sections/header.liquid` (blue header) and `sections/announcement-bar.liquid` (marquee bar).
- Wave-bag cart icon on EVERY page (`show_elsora_bag = true` in `sections/header.liquid` and `sections/cart-icon-bubble.liquid`).
- ELSORA teal wave footer on EVERY page (`elsora_footer = true` in `sections/footer.liquid`, footer-local colour/Jost values); the old purple footer is no longer used.
- /cart: `sections/main-cart-items.liquid` renders `snippets/elsora-wave-bg.liquid` (copy of the difference-grid wave background) behind both cart sections, white cards, pill quantity, round remove button, reassurance line, ELSORA checkout/empty-cart buttons; "Continue shopping" goes to the sandbox page.
- Cart line images per variant: `snippets/elsora-cart-item-image.liquid` maps Silver Pair -> `elsora-ref-silver-pair.webp`, Gold Pair -> `elsora-ref-gold-pair.webp` (Content > Files, read via `images[...]`); used in the cart page and `snippets/cart-drawer.liquid`. Shopify checkout still uses the product/variant image (variants have no image set).
- The sandbox hero gallery is built from product media, so adding images to the product (e.g. to set variant images) would also add gallery thumbnails.
- Same day, round 2 (NOT yet visually verified): product option renamed "Shape" -> "Set" via productOptionUpdate (variant IDs 59209490235717 / 59209490268485, values, prices, SKUs unchanged; no theme code reads the option name). "Have an account? Log in" removed from /cart and the drawer. Cart drawer restyled in `snippets/cart-drawer.liquid` (`.elsora-drawer`, hardcoded ice values because the drawer is on every page) and holds the AJAX add script: hero `.cv-hero-form` and final CTA `.cv-final-form` add via /cart/add.js and open the drawer (fallback: normal submit to /cart). The header cart icon is a plain link to /cart again (`assets/cart-drawer.js` `setHeaderCartIconAccessibility` returns early).
- Same day, round 3 (NOT yet visually verified): ELSORA header (light blue, Jost) and lavender marquee bar on EVERY page (`is_pdrn_sandbox = true` in `sections/header.liquid` and `sections/announcement-bar.liquid`, with header-local Jost/colour vars). `layout/theme.liquid` uses the ice-globes palette on every page type except `index` and `product` (those keep 'current' until redesigned). Header search and account icons are hidden (`show_header_search` / `show_header_account = false`). New Admin menu "ELSORA main menu" (`elsora-main-menu`, Shop -> sandbox page, Contact) used by the draft's `sections/header-group.json`; the original `main-menu` stays as-is because the live theme uses it. The header cart icon opens the drawer again (original Dawn `assets/cart-drawer.js` restored); the drawer has a quiet "View full cart" link under Check out. /collections/*: new `sections/elsora-collection.liquid` (wave bg, Jost title, ELSORA card with silver-pair photo, "From $54.99", links to the sandbox page, no filter/sort) is the only section in `templates/collection.json`. /pages/contact: `sections/contact-form.liquid` restyled (wave bg, Jost title, white form card, purple Send, "We reply within 24 hours · support@elsora.store").
