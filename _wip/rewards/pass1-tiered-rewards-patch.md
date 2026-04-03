# Pass 1 patch — Tiered Rewards page

Minimal surgical fixes for the live page at https://docs.teak.io/user-guide/tiered-rewards.html.

---

## Fix 1 — Remove unsupported marketing claim

**Current (Using With Notifications section):**
> This approach increases click-through rate by 10–15% relative to baseline.

**Delete this sentence.** It's an unattributed claim and doesn't belong in reference documentation. If the data is worth sharing, it belongs in a case study or marketing asset with a source.

---

## Fix 2 — Add note about tier ordering

In the Creating a Tiered Reward Bundle section, after mentioning that tiers are evaluated in order, add:

> To change evaluation order, drag tiers up or down in the editor. Put your most specific audiences at the top.

---

## Fix 3 — Clarify what happens when you edit a bundle after sending

In the Editing Tiered Rewards section, the current text says:
> Changes to notifications invalidate original send-time rewards; future clicks evaluate current audience membership (behaves like link clicks)

Rewrite as:
> If you edit a bundle after a notification has been sent, the original send-time reward locks are invalidated. Any player who hasn't yet clicked will have their tier re-evaluated at click time using their current audience membership — the same behavior as a link reward.

---

## Fix 4 — Terminology

Do a global find-and-replace:

| Find | Replace |
|---|---|
| user | player |
| message | notification |
| push | notification |
