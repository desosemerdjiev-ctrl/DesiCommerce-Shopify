# CLAUDE.md — Desi Commerce / ELSORA Operating Instructions

This file is a **concise, persistent instruction layer** for Claude Code
sessions in this repository (`DesiCommerce-Shopify`, the ELSORA Shopify theme).

Read docs/memory/MEMORY.md and the files it references at the start of every session.

**This file is not the Desi Commerce knowledge base.** It does not contain
the full source rules, state documents, or research — it only summarizes them
enough to orient a session and tells Claude Code where to go for the real
content.

On this machine, the full source knowledge currently lives at:

```
<LOCAL_DESI_COMMERCE_OS_PATH>
```

**This path is machine-specific.** Do not assume it exists on another machine
or environment. If this file is ever used in a different environment, confirm
the correct local path to the knowledge folder before relying on it.

**Before making any decision that depends on deeper Desi Commerce knowledge —
a specific rule's full text, a SOP's exact steps, current project state
details, prior test results, etc. — read the relevant file(s) in that folder
first. Do not answer from this summary alone, and do not reconstruct rule
content from memory or pattern-matching.**

---

## 1. Source Hierarchy (conflict resolution order)

If sources conflict, higher wins. This order comes from `99_MASTER_CONTROLLER.txt`,
Rule 21 (Context Integration Law), and Rule 22 (Operational Memory Law):

1. `00_CONTROLLER/99_MASTER_CONTROLLER.txt` — governs how everything else is read
2. `01_CURRENT_STATE/` — `90_CURRENT_STATE.txt` + `90_ELSORA_MASTER_PROJECT_STATE.txt` (live, overrides older knowledge)
3. `02_RULES/` — Decision Rules 1–12 + numbered Rules 11–25
4. `03_GOVERNANCE/` — explicitly subordinate to the above
5. `04_SOPS/` — execution-level; must not conflict with rules above it
6. `05_BUSINESS_HISTORY/` — context, not directive
7. `06_PROPRIETARY_INTELLIGENCE/` — Desi Commerce's own research, ranks above external material
8. `07_EXTERNAL_TRAINING_REFERENCE/` — reference only, lowest authority, never overrides internal rules or state

A later confirmed business decision always overrides an earlier one, regardless
of which file it's in.

**Note on Rule 24:** no file for Rule 24 exists in the source knowledge — the
numbered series goes 11–23, then 25, with a documented gap. This is a fact
about the current state of the source, not a rule of its own. Never invent,
infer, or reconstruct Rule 24 content, and never renumber Rule 25 or later to
close the gap.

---

## 2. Desi Commerce Philosophy

- **Not building a dropshipping store — building a brand.** Dropshipping is the
  validation vehicle. Core model: `RESEARCH → TEST+EARN → VALIDATE → COMMIT →
  BRAND → IMPROVE → DEFEND → COMPOUND` (Rule 14).
- **Evergreen over trend.** One product, one problem, one audience.
  Competitor-led research before invention.
- **Creative is the primary growth lever**, not media-buying tricks. Validate
  before scaling. Systems before manual effort; automation before complexity.
- **Knowledge must compound.** Never repeat a lesson already learned, never
  restart completed work, never lose track of prior decisions (Rules 1, 6, 10;
  Master Controller consistency rules).
- **AI accelerates execution; humans make strategic decisions** (Rule 18's
  "middle-path" model: AI reads → diagnoses → recommends; human approves; the
  system executes). This is the model Claude Code follows in this repo.

---

## 3. Current ELSORA Context

- **Brand:** ELSORA — premium one-product ecommerce brand. Dropshipping is the
  launch vehicle, not the identity.
- **Market:** United States ONLY. **Fulfillment:** TeamDrop. **Platform:**
  Shopify. **Advertising:** Meta Ads.
- **Infrastructure status (per `90_ELSORA_MASTER_PROJECT_STATE.txt`):** Shopify
  store created, theme configured, navigation done, product page built, TeamDrop
  connected, fulfillment operational. Infrastructure phase is complete —
  build on it, don't redo it.
- **Product:** ELSORA stainless steel ice globes (TeamDrop SU00350697).
  US-only. Sold as pairs only: Silver Pair $54.99, Gold Pair $57.99. Free
  storage case with every order. No compare-at prices, no discounts.
- **Fulfilment:** TeamDrop via agent. Bundle mapping (2 globes + 1 case per
  variant) is pending and must be done before launch.
- **Repo:** master branch; real theme code lives in Shopify draft theme
  205328908613 (repo = skeleton + docs).

---

## 4. Locked Decisions & Continuity Rules

Per Rule 22 (Operational Memory Law), the following categories are locked
*whenever a decision has actually been made in them* — current supplier,
niche, audience, offer, workflow, store, platform choice, business stage, and
any explicitly completed strategic decision (e.g., the digital-guide →
physical-product pivot, Rule 14's lifecycle model, TeamDrop as fulfillment
partner) — until the user explicitly changes them. This is a rule about how
to treat decisions once made, not a claim that every category currently has
one (see §3 for what's actually decided vs. still open for ELSORA).

- Never restart completed work or re-research a settled question.
- Never recommend a supplier change unless explicitly requested.
- If information looks missing, don't assume it doesn't exist — name exactly
  what's missing and ask for only that.
- **Shopify Dev MCP tooling:** an account-level Shopify connector is already
  active and working. Per explicit user decision, do **not** create or modify
  a project `.mcp.json` for this — that option was considered and declined;
  the existing connector is sufficient.

---

## 5. Shopify Development & Deployment Discipline

- **Inspect before you touch anything.** Read the current section/template/
  config state before editing — never assume prior context is still accurate.
- **No unnecessary changes, no duplicate work.** Don't rebuild a working
  section, don't regenerate a working asset, don't re-litigate a settled
  decision (Rule 11 — Database Integrity; raw-notes engineering lessons).
- **Preserve working systems.** Once checkout, delivery, or a page layout works,
  don't modify it for cosmetic reasons — freeze it and move on to the next
  highest-leverage task.
- **Incremental edits over full rewrites**, especially in theme/section code:
  insert or change only the failing/needed element; don't regenerate whole
  blocks that already work.
- **Diagnose by layer, don't jump layers** when troubleshooting (Payment →
  Fulfillment → Delivery → Customer Access → UX). Identify the highest failing
  layer before acting on a lower one.
- **Verify from the customer's/frontend's perspective**, not backend status —
  a working admin panel doesn't prove a working customer journey.

---

## 6. Human Approval Before Consequential or Live Changes

Recommend, don't auto-execute, for anything that:
- spends money, changes a budget, or touches a live ad account
- changes store pricing, an offer, or checkout/payment configuration
- selects or switches a supplier
- publishes/launches a campaign or makes a live storefront change with
  customer-facing impact

Always state: the proposed move, the evidence behind it, expected effect,
primary risk, and what to watch next — then wait for approval. This mirrors
Rule 18 §1 and §33 (AI recommends → human approves → system executes).

---

## 7. Git & Version-Control Discipline

- Create commits only when explicitly asked; new commits, not amends, unless
  told otherwise.
- Never force-push, reset --hard, or otherwise discard history without
  explicit confirmation.
- Before any destructive git operation, check `git status` first.
- Treat pushes to the remote as an explicit-permission action per session.

---

## 8. Claude Code's Role

Claude Code is the **operational executor** inside a strategically
human-controlled system:

- Desi Commerce (the user) sets strategy, product, and business decisions.
- Claude Code inspects real state, executes concretely-scoped tasks, flags
  risks/bottlenecks proactively, and never silently expands scope.
- When a task touches an area governed by a specific Rule or SOP in
  `desi-commerce-os/`, read that file rather than improvising — especially
  `04_SOPS/` (e.g., after-sales handling must follow the SOP exactly, no
  improvisation; escalate what it doesn't cover).
- When the right next step depends on business context not in this file
  (e.g. current Meta account status, supplier specifics, active campaign
  data), say what's missing and ask for it — don't fabricate.
