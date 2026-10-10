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
- Same day, round 4 (NOT yet visually verified): final CTA button reads "GET YOUR PAIR — $price" (`sections/final-cta.liquid`; its JS only updates the price span); hero button stays "Add to Cart — $price". Risk-reversal line "Free storage case · Free U.S. shipping · 30-day money-back guarantee" (`.cv-risk-line-<sid>`) sits directly under both buttons (`sections/hero-banner.liquid`, `sections/final-cta.liquid`). /collections/* shows the ice globes as two cards, Silver Pair and Gold Pair ("Our Pick"), with live variant prices, linking to the sandbox page with `?variant=<id>`; the hero JS reads `?variant=` and clicks the matching Silver/Gold card (final CTA follows via its aria-pressed sync). Product stays one product with two variants.
- Same day, round 5 (NOT yet visually verified): Jost removed everywhere in the draft (no Google Fonts import in `snippets/elsora-design-tokens.liquid`); all ELSORA font variables now use `"Helvetica Neue", Helvetica, Arial, sans-serif` (tokens, `layout/theme.liquid`, header, announcement bar, footer, cart drawer) to match the approved theme-editor look. Hero big price follows the selected Silver/Gold card (Gold default, `?variant=`, every click). Selector card renamed "Premium Gold Pair" -> "Gold Pair". Benefit cards in `templates/page.pdrn-sandbox.json` got the new de-puff / sculpted look / glow texts. Admin: Files `elsora-ref-silver-pair.webp` (MediaImage 74677795946821) and `elsora-ref-gold-pair.webp` (74677796012357) attached to the product and set as Silver/Gold variant images (checkout image); the hero gallery skips those two media IDs. Variant IDs, prices, SKUs and option "Set" unchanged.
- Upload lesson: large theme files can be pushed without pasting their content: `stagedUploadsCreate` (resource FILE, text/plain, PUT) -> `curl -X PUT -H "Content-Type: text/plain" --data-binary @file <url>` (no x-goog-acl header, it returns 400) -> `themeFilesUpsert` with `body: {type: URL, value: <resourceUrl>}` (async job) -> verify `checksumMd5`.
- Same day, round 6 (NOT yet visually verified): option value renamed "Gold Pair" -> "Premium Gold Pair" via productOptionUpdate (value 14157939573061; variant IDs 59209490235717 / 59209490268485, prices, SKUs unchanged). This reverses the round-5 "Gold Pair" naming: the gold variant is "Premium Gold Pair" everywhere. The hero now matches Silver/Gold by variant ID first (title match is only a fallback). Health wording softened in `templates/page.pdrn-sandbox.json`: "Cooling Ritual", "calm the look of puffiness or wake up tired-looking skin", "lasts a full session", "The cool touch is gentle on most skin types, including sensitive skin." No "inflammat", "circulation", "therapy" or "treatment" text left in the draft (only the product handle contains "therapy").
- Same day, round 7 (pre-launch copy audit, NOT yet visually verified): sandbox page SEO title/description set via page metafields `global.title_tag` / `global.description_tag` (Page 727843144005). Hero gallery hides media 74886235324741 (mixed silver + gold, the product's featured image) and 75084847153477 ("Crafted to Last", unconfirmed 304 / sealed core / anti-freeze claims) plus the two variant images; the first visible media is the main hero image. Gallery alt texts rewritten without claims (media 74859462197573 still has no alt: its content is unknown because cdn.shopify.com is blocked here). Copy fixes in `templates/page.pdrn-sandbox.json` (timing = about 5 minutes, chilling = 3–4 hours or overnight, no 304 / 2+ hours stats, sentence-case labels, "Ways to use it" + "Illustrative images." caption via new `subheading` setting in `sections/reviews-grid.liquid`). Policies NOT changed: the connector still lacks `write_legal_policies`; the edited HTML is prepared for the user to paste.
- 2026-10-09, round 8 (final pre-launch fixes, NOT yet visually verified): correction of round 7. Media 74886235324741 is a single silver globe and is now the first hero image. The silver + gold photo is 74859462197573 (ChatGPT_Image_Sep_12_2026_02_16_06_PM.png); it is hidden from the hero together with before/after 75085145571653, "Crafted to Last" 75084847153477 and the two variant images. Hero dormant fallbacks removed (1/2/3-bottle bundle, qty-only Single/Pair cards, compare-at defaults, "Save X%", rating/review_count/price-note settings). Product description: five-minute ritual, fridge or freezer, no sealed-core / anti-slip claim. Cart and drawer show "Free U.S. shipping. Taxes calculated at checkout."; /collections/all heading is "Shop ELSORA Ice Globes"; contact form labels "Your message" / "Send message" (locales/en.default.json).
- 2026-10-09, round 9 (NOT yet visually verified): hero gallery restored to the original 7 product images in product-media order (only the two variant images stay hidden). Eyebrow is "304 Stainless Steel Ice Globes for Face & Neck". Heading CSS checked against backup 208089940293: weight, size, letter-spacing, line-height and text-shadow are identical; only the font family changed (Jost -> Helvetica Neue stack), so the heavier look comes from Helvetica Neue's real 500 (Medium) cut. Not changed without approval. Stats strip uses a 3-column grid (equal columns, centered, max 900px).
- 2026-10-09, round 9b (approved by the user): black headings set to `font-weight: 400` to match the approved editor look (with the Helvetica Neue stack, weight 500 renders as the heavier Medium cut). Changed: hero H1 (`.cv-hero__title`), and the h2 in lifestyle-row, difference-grid, how-to-steps, reviews-grid and faq-accordion. Unchanged: final CTA h2 (purple, not black), bridge line (already 400), sizes, line-height, letter-spacing, H1 text-shadow, eyebrows, body, buttons, prices, stats strip.
- 2026-10-09, round 10 (NOT yet visually verified): three new Files attached to the product (appended; product media order and featured image unchanged): 75332843635013 (6f5190f6-….png, assumed morning-ritual), 75332834951493 (af9b0c58-….png, assumed choose-your-pair), 75332405625157 (e6956338-….png, everything-you-need, confirmed). A/B mapping is a guess; to swap, exchange the first two IDs in `cv_gallery_order` in `sections/hero-banner.liquid` and swap their alts. The hero gallery order now comes from `cv_gallery_order` (explicit media IDs), not product media order.
- 2026-10-09, round 10b: the user deleted 75332843635013; the new morning-ritual image is 75333096014149 (0989a466-3906-4fcd-ab4c-93ded4589d73.png). It is attached to the product (appended), has the alt "Woman using an ELSORA stainless steel ice globe on her cheek", and is position 1 in `cv_gallery_order`. Positions 2–7 are unchanged.
- 2026-10-09, round 11 (304 copy): the cart and drawer tax line is now "Taxes calculated at checkout."; the FAQ steel answer and the benefits subtitle now say "304 stainless steel" (the FAQ adds "with a soft silicone grip"); the product description now reads "Made from durable 304 stainless steel with a soft silicone grip — …". The stats strip and eyebrow are unchanged.
- 2026-10-09, round 12: media 75333096014149 (morning-ritual) moved to position 1 with productReorderMedia, so it is now the product's featured image. No media was deleted. The hero is unaffected because it uses `cv_gallery_order`. The product URL move (/products/ice-globes) and the catalog cleanup are only planned/listed and are waiting on the user's approval.
- 2026-10-09, round 13 (theme part of the product URL move, NOT yet visually verified):
  - New `templates/product.ice-globes.json` is a 1:1 copy of the sandbox page sections. It has no product setting; hero, reviews and final CTA use `section.settings.product | default: product`, so it survives a handle change.
  - `template.suffix == 'ice-globes'` is now accepted wherever 'pdrn-sandbox' was checked (theme.liquid palette + 8 sections; header and announcement bar were already global).
  - Product JSON-LD is output in hero-banner, on product pages only.
  - Cart, drawer and collection links look up handle 'ice-globes' or the old handle. They point to the product page only once `product.template_suffix == 'ice-globes'`, otherwise to the sandbox page.
  - Admin cleanup: "Gentle Hair Removal Body Mousse" archived; collections deleted: audio, construction, kitchen-dining, building-materials, clothing-accessories, household-supplies, novelty-special-use, hair-removal.
  - Publish-day Admin steps are still pending.

## Round 14 — background finish TEST (draft 205328908613, 2026-10-09)
- New snippet `snippets/elsora-bg-finish.liquid`, rendered in theme.liquid right after elsora-design-tokens. Active only on template suffix pdrn-sandbox / ice-globes and template `cart`.
- Grain = inline SVG feTurbulence tile (160px), soft-light blend, opacity = intensity %. Satin sheen = 115deg white gradient, peak 7%, wave backgrounds only.
- Applied as extra background LAYERS on the section's own background (CSS vars `--elsora-finish-wave*` / `--elsora-finish-flat*`, fallback none/auto/repeat/normal) — not an overlay, so images/text/buttons/cards/cart drawer are untouched.
- Wave: hero, difference-grid, how-to-steps, elsora-wave-bg. Flat: faq-accordion, reviews-grid, proof-strip, final-cta (only when no bg image). Cart: `body.gradient` grain.
- Settings (Theme settings → "ELSORA background finish"): `elsora_bg_grain` (default on), `elsora_bg_grain_intensity` 0–6 % (default 3), `elsora_bg_sheen` (default on). To turn the test off: untick both.
- Not visually verified (storefront unreachable from the session).

## Round 15 — mobile menu drawer restyle (draft 205328908613, 2026-10-09)
- New snippet `snippets/elsora-menu-drawer.liquid`, rendered as the first child of `#menu-drawer` in `snippets/header-drawer.liquid` (only change in that file: one render line).
- Active only on pdrn-sandbox / ice-globes / cart, and only at max-width 989px (desktop menu type is "dropdown", so desktop is unchanged).
- Renders `elsora-wave-bg` inside the drawer: same wave ribbons, an aqua-only gradient (#F0F8F8 → #58E8F0 → #D0F0F8, no white top fade) and the round-14 finish layers (grain + sheen) via `--elsora-finish-wave*`.
- Utility-links grey band made transparent. Items #0D0D0D; hover/focus = rgba(255,255,255,.32); active = 1px #706FCB underline (no grey background).
- The header (X, logo, cart) and open/close JS/CSS are untouched. Not visually verified.
- Round 15b: the drawer gradient now ends in white (#D8F8F8 92% → #FFFFFF 100%). #menu-drawer gets `overflow: visible` plus an `::after` white fade (64px) just below the panel, so there is no line where the panel ends over the page (seen in the editor's mobile preview, where the drawer is shorter than the screen). Only snippets/elsora-menu-drawer.liquid changed (md5 fb71b91b…).
- Round 15c: removed the 64px white `::after` fade below the drawer and `overflow: visible`, because the fade covered the purple hero eyebrow. The drawer's own gradient still ends in white. The drawer style now applies on EVERY page (the template check was removed; the header is global; e.g. /pages/contact was still white). Grain/sheen inside the drawer still only appear where elsora-bg-finish is active (sandbox / ice-globes / cart). md5 5cf26ddd…
- Round 15d: the white fade below the drawer is back but SHORT: `::after` height 22px (#FFF → rgba(255,255,255,.5) at 40% → transparent), plus `overflow: visible`. The 64px version washed out the purple eyebrow, so keep it short. md5 8e715f82…

## Round 16 — FAQ "How long do they stay cold?" (draft 205328908613, 2026-10-09)
- In templates/page.pdrn-sandbox.json (md5 72fd391a…) and templates/product.ice-globes.json (md5 3005e4e6…), block f3:
  - Answer changed from "Chill them, roll, and pop them back in to re-chill anytime." to "Long enough for a relaxed 5-minute ritual. For a longer session, simply pop them back in the fridge or freezer for a few minutes and continue."
  - block_order changed from f1,f2,f3,f4,f5,f6,f7 to f1,f2,f4,f5,f6,f3,f7, so the question now sits directly above "Why are there no reviews yet?".

## Round 17 — satin depth on the wave ribbons (draft 205328908613, 2026-10-10)
- Reference image used for the surface finish only (not its colours or shapes).
- New settings in "ELSORA background finish" (existing ones kept): `elsora_bg_satin_depth` "Satin depth" (checkbox, default on) and `elsora_bg_satin_intensity` "Satin intensity" (0–100 %, step 1, default 50).
- snippets/elsora-bg-finish.liquid (md5 ebb03d61…):
  - With part: 'svg', it outputs a 0×0 SVG holding filter #elsoraSatinDepth.
    - Mask = SourceAlpha ×4, so the strength follows each ribbon's own opacity.
    - Soft shadow under each band: blur 3, dy 4, #0A3A46 at 0.22·k.
    - Upper-edge light: #FFF at 0.6·k.
    - Lower-edge deeper tone: #0A3A46 at 0.18·k.
    - k = intensity / 100.
  - In head, it adds CSS `filter: url(#elsoraSatinDepth)` on `.elsora-wave-lines > g`, `.elsora-wave-bg__lines > g`, `[class*="cv-diff-wave-lines-"] > g` and `[class*="cv-howto-wave-lines-"] > g`.
  - Same gating as the rest of the finish: sandbox / ice-globes / cart, including the mobile menu on those pages.
- layout/theme.liquid (md5 10aa3a46…): `{% render 'elsora-bg-finish', part: 'svg' %}` right after `<body>`.
- config/settings_schema.json (md5 929ac7f8…).
- Wave shapes, positions, colours and the sections themselves are unchanged. Grain is unchanged (still governed by "Background grain intensity"). Not visually verified.
- Round 17b fix: the user reported that the waves looked zoomed and thicker, worst on mobile.
  - Geometry was never changed: the hero, difference-grid, how-to-steps, elsora-wave-bg and menu-drawer md5s are identical to pre-17.
  - Cause: the satin filter's drop shadow (blur 3 + dy 4 user units, mask ×4) spread outside every band. The mobile viewBox 400×1200 is stretched about 2× vertically, which doubled the effect.
  - Fix in elsora-bg-finish.liquid (md5 40dad5d6…): the shadow is now `feComposite in="shadowfull" in2="m" operator="in"`, so every filter layer stays inside the original band edges. Light, deep tone and grain are unchanged. Lesson: SVG filter effects on the wave ribbons must never paint outside the band shape.
- Round 17c: the user said the waves must look EXACTLY as before the SVG filter.
  - Before the filter, the top bands faded in from the white top and different sections showed different band sizes. With the filter, the bands ran edge to edge and looked stretched.
  - Cause: the filter's darker tone (#0A3A46) and shadow make the white-on-white bands visible. Any darkening filter changes the look, even with the 17b clipping.
  - Fix: in config/settings_schema.json (md5 784be921…), `elsora_bg_satin_depth` now defaults to false. settings_data was never saved, so the default applies and the filter is not output, giving exactly the pre-17 waves (round-14 grain + sheen kept).
  - The settings "Satin depth" and "Satin intensity" remain. Switching Satin depth on brings the filter back, with the same look change.
  - Lesson: do not add darkening layers on the wave ribbons.

## Round 18 — audit fixes (draft 205328908613, 2026-10-10)
- Homepage:
  - templates/index.json is now a byte-for-byte copy of templates/page.pdrn-sandbox.json (md5 72fd391a…). Old index (md5 ef35bbe5…) was the hair-removal content; a copy still exists in the backup themes.
  - `or template.name == 'index'` was added to the template checks in: theme.liquid (palette; the header comment was updated too), hero-banner, faq-accordion, reviews-grid, difference-grid, lifestyle-row, how-to-steps, proof-strip, footer and elsora-bg-finish. The mobile menu was already global.
  - Publish-day note: the hero/reviews/final-cta `product` settings in index.json and the sandbox template reference the product handle. If the handle changes to ice-globes, re-check them.
- Hero gallery: the main image srcset is now 600/800/1000/1200/1400w (sizes unchanged). Thumbs carry `data-srcset` with the same widths (`data-full-2x` with its 2000px 2x was replaced), and the JS sets `mainImg.srcset` from it. Thumbnails stay at 150px.
- Variant URL: an offer-card click does `history.replaceState` with `?variant=<id>` (in try/catch).
- Thumbnail img alt is now `media.alt | default: product.title`.
- Mobile:
  - `.cv-trust-dot` is hidden at max-width 749px.
  - At ≤900px the offer card padding changed from 10px 8px to 10px 12px, and the title wraps (white-space normal, line-height 1.25) instead of hitting the edge.
- md5s:

| File | md5 |
|---|---|
| theme.liquid | f728842c… |
| hero | 87324e3f… |
| faq | 4d2ad39d… |
| reviews | 383c9ed4… |
| difference | e72be2bf… |
| lifestyle | 15d0bf66… |
| how-to | 5fe3a616… |
| proof-strip | d69ecf66… |
| footer | 2cf50a4a… |
| bg-finish | a549b632… |
- Round 18b (mobile ≤900px only, hero-banner md5 40cc4e56…):
  - Offer card padding changed from 10px 12px to 16px 12px 10px in BOTH cards, so the "Our Pick" badge (top −9px) has clear space above the title.
  - Card title is now 12px (was 12.5) with min-height 2.5em (2 lines reserved in both cards), so title / Pair / price line up.
  - Measured: "Premium Gold Pair" needs about 101px at 12px, while the text space is 78–93px on 360–390px phones, so one line is not possible there.
  - Desktop untouched.

## Round 19 — proof strip middle stat (draft 205328908613, 2026-10-10)
- In the proof_strip stat_2 block, "number" changed from "Durable" to "304". The label "stainless steel" is unchanged (shown uppercase by CSS).
- Templates:
  - page.pdrn-sandbox.json and index.json are still identical (md5 4b203ad0…).
  - product.ice-globes.json is md5 d9141a90….

## Round 20 — product title (Admin, 2026-10-10)
- Product 16150614507845 title changed from "ELSORA Ice Globes — Stainless Steel Facial Roller (Pair)" to "ELSORA Ice Globes (Pair)" (productUpdate, title only).
- Handle, variants, prices, SKUs, description, media and product SEO (still null) are unchanged. Page SEO metafields were not touched.
- Theme 205328908613 search (428 files): no hardcoded "Stainless Steel Facial Roller" / "Facial Roller". Cart, cart drawer, collection cards, JSON-LD and alts all read product.title / item.product.title, so they show the new title automatically.
