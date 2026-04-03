# Option C: Focused Refresh — Reward Bundles & Tiered Rewards Docs

**Status:** Proposal
**Date:** April 2, 2026
**Scope:** 3 updated pages + 1 new page · ~2–3 days of writing · ~1 day of review

---

## What this plan does

Option C keeps the existing page structure mostly intact but rewrites the sections that are outdated, fills the documented gaps, and aligns everything to the microcopy writing guide. It's less disruptive than a full rewrite (Option B) but goes further than patching copy in place (Option A).

The core idea: restructure content *within* pages around tasks, not features. Add one new page to cover the bundle groups and filtering layer that's currently undocumented. Place screenshots only at decision points where the UI isn't self-explanatory.

---

## Page-by-page plan

### 1. Reward Bundles (existing page — rewrite in place)

**Current state:** Covers bundle concept, reward types, random distribution, and the editor UI. Mixes explanation with how-to steps. Doesn't mention bundle groups, archiving, or how randomization and tiers compose.

**What changes:**

Open with a one-sentence definition, then go straight into tasks.

**Proposed structure:**

- **What's a reward bundle** — Two sentences max. A bundle is a reusable reward config you attach to notifications. It can include fixed rewards, randomized rewards, tiered rewards, or a combination.

- **Create a bundle**
  - Step-by-step for the editor. Screenshot: bundle editor with randomized rewards and tiers visible (Screenshot 2). This is the most complex screen, so the screenshot earns its place here.
  - Call out the reward type options (coins, items, currency, etc.) in a simple table rather than prose.

- **Add randomized rewards**
  - Explain odds-based distribution plainly: "Each reward option has a weight. Teak picks one at random based on those weights."
  - Note: odds are per-send, not per-player-lifetime.

- **Add tiered rewards**
  - Brief explanation of tiers here (audience-based, first-match order, default tier catches everyone else). Point to the dedicated Tiered Rewards page for details.
  - Screenshot: tiered bundle config (Screenshot 4) only if it shows something the editor screenshot doesn't already cover. If it's the same modal, skip it.

- **Combine randomization and tiers**
  - This is the undocumented composition case. Explain clearly: "You can use both in the same bundle. Teak evaluates tiers first to pick the reward set, then randomizes within that set."
  - No screenshot needed — the concept is simple once stated.

- **Test a bundle**
  - Steps for the test dialog. Screenshot: test flow dialog (Screenshot 3). Explain the audience dropdown, User ID field, and Extra Flags.
  - Lead with *why* to test: "Verify the right tier resolves and the reward payload looks correct before sending to players."

- **Archive a bundle**
  - New section. Explain what archiving does (hides from active list, doesn't delete, can be restored). Steps to archive and unarchive.

**Terminology cleanup:** "player" throughout, "notification" not "message," "reward" not "incentive." Sentence case on all headings.

**Screenshot placement (this page):** 2 screenshots — bundle editor, test dialog.

---

### 2. Bundle Groups & Filtering (new page)

**Why a new page:** The bundle list filtering layer (groups, archive toggle, randomization filter) is a distinct organizational feature. Cramming it into the Reward Bundles page buries it. A short standalone page keeps both pages scannable.

**Proposed structure:**

- **What are bundle groups** — A filtering layer on the Rewards page that helps you find bundles as your library grows.

- **Filter options**
  - Explain each filter plainly in a small table:

    | Filter | What it shows |
    |---|---|
    | All | Every active bundle |
    | Audience controlled | Bundles with at least one tier |
    | Not audience controlled | Bundles with no tiers (single reward set) |
    | Randomized | Bundles using odds-based distribution |
    | Not randomized | Bundles with fixed rewards only |
    | Show archived | Includes archived bundles in the list |

  - Screenshot: bundle list view with filter controls visible (Screenshot 1). This is the right place for it — it shows the UI the table describes.

- **Sort and search**
  - Brief note on sort options and search behavior if the UI supports them.

- **When to use filters**
  - One or two practical examples: "Looking for all bundles that use tiered rewards? Select 'Audience controlled.' Need to bring back a seasonal bundle? Toggle 'Show archived.'"

**Screenshot placement (this page):** 1 screenshot — bundle list view.

---

### 3. Tiered Rewards (existing page — targeted rewrite)

**Current state:** Covers audience-based tiers, first-match evaluation order, send-time vs. click-time evaluation. Likely accurate but may not clearly separate the two evaluation modes or explain when to choose each.

**What changes:**

Keep the existing structure but sharpen the task framing and fill gaps.

**Proposed structure:**

- **How tiered rewards work** — Short explanation. Teak checks the player against each tier's audience in order, top to bottom. First match wins. If no tier matches, the default tier applies.

- **Set up tiers on a bundle**
  - Steps to add tiers in the editor. Reference the Reward Bundles page for the editor basics.
  - Emphasize: "Order matters. Drag tiers to control priority."

- **Choose when tiers are evaluated**
  - This is the key decision. Present it as a choice, not a feature list:
    - *Send-time evaluation:* Tier is locked when the notification is sent. Use when the reward amount is shown in the notification copy.
    - *Click-time evaluation:* Tier is re-evaluated when the player opens the notification. Use when you want the most current audience membership to determine the reward.
  - No screenshot needed — this is a conceptual choice, not a UI walkthrough.

- **Use template tags with tiers**
  - Explain that tags like `{{reward_amount}}` resolve per-tier. Screenshot: template tag dropdown (Screenshot 5) showing the REWARDS section. This helps because the tag names aren't guessable.

- **Common patterns**
  - Brief examples: VIP players get more coins, new players get a starter bundle, seasonal tiers for holiday events.

**Screenshot placement (this page):** 1 screenshot — template tag dropdown.

---

### 4. Server-to-Server Reward API (existing page — light edit)

**Current state:** Covers POST endpoint, HMAC signature, event_id idempotency, retry logic. Likely still accurate.

**What changes:**

This page is the least affected. Apply terminology and tone cleanup only.

- Replace "user" with "player" throughout.
- Replace any instances of "message" or "push" with "notification."
- Tighten any passive-voice explanations ("The signature is computed by…" → "Compute the signature by…").
- Verify the endpoint URL, parameter names, and example payloads are current. Flag any discrepancies for eng review.
- Add a brief note linking to the Reward Bundles page for context on what `bundle_id` refers to.

**Screenshot placement (this page):** None. API docs don't benefit from UI screenshots.

---

## Screenshot usage summary

| Screenshot | Used on | Purpose |
|---|---|---|
| 1. Bundle list with filters | Bundle Groups & Filtering (new) | Show the filter controls |
| 2. Bundle editor with tiers | Reward Bundles | Show the most complex editing screen |
| 3. Test flow dialog | Reward Bundles | Show test inputs and audience dropdown |
| 4. Tiered bundle config | *Skip unless distinct from #2* | Avoid redundancy |
| 5. Template tag dropdown | Tiered Rewards | Show available reward tags |

Principle: if a screenshot doesn't prevent a mistake or reduce confusion at that specific point in the doc, cut it.

---

## Terminology alignment checklist

| Instead of | Use |
|---|---|
| User | Player |
| Message, push | Notification |
| Incentive, bonus | Reward |
| Title case headings | Sentence case |
| "You should…" / "It is recommended…" | Direct instructions ("Add a tier," "Select the audience") |
| Feature-first framing ("Teak supports…") | Task-first framing ("To set up tiered rewards…") |

---

## Scope estimate

| Work item | Effort |
|---|---|
| Reward Bundles page rewrite | ~1 day |
| Bundle Groups & Filtering (new page) | ~0.5 day |
| Tiered Rewards page rewrite | ~0.5 day |
| Server-to-Server API page cleanup | ~2 hours |
| Screenshot prep (crop, annotate if needed) | ~2 hours |
| Internal review + revisions | ~1 day |
| **Total** | **~3–4 days** |

---

## What this plan doesn't do

These are explicitly out of scope to keep the refresh focused:

- Restructure the information architecture or navigation beyond adding one page
- Rewrite the server-to-server API docs from scratch (they're functional as-is)
- Create video walkthroughs or interactive demos
- Redesign the docs site template or styling
- Document features still in development

---

## How to evaluate whether this worked

After the refresh ships, check:

1. Can a new team member set up a tiered, randomized bundle by following only the docs (no Slack questions)?
2. Can someone find and unarchive a bundle without guessing?
3. Does every heading on the Reward Bundles page start with a verb or answer "how do I…"?
4. Is the word "user" gone from all four pages?

If yes to all four, the refresh did its job.
