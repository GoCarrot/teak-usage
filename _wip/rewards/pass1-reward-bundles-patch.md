# Pass 1 patch — Reward Bundles page

Minimal surgical fixes for the live page at https://docs.teak.io/user-guide/rewards.html.
These patches correct terminology, a wrong UI label, and two undocumented features.
No structural changes to the page.

---

## Fix 1 — Terminology in the Overview section

**Current:**
> Rewards can be integrated into Links and Messages as incentives or prizes.

**Replace with:**
> Reward bundles attach to notifications and links to deliver items or currency to players.

---

## Fix 2 — Terminology throughout

Do a global find-and-replace pass:

| Find | Replace |
|---|---|
| Messages | notifications |
| incentive | reward |
| prize | reward |
| users | players |

---

## Fix 3 — Wrong checkbox label in Randomized Rewards section

**Current:**
> Check "Randomize Rewards"

**Replace with:**
> Check **Use Random Rewards**

---

## Fix 4 — Clarify what randomized vs. non-randomized bundles deliver

**Current (end of Randomized Rewards section):**
> Note: Randomized bundles provide a single item or currency per claim.

**Replace with:**
> When **Use Random Rewards** is on, Teak picks one reward option per claim based on weighted chances. When it's off, players receive every reward in the bundle — all items and all amounts.

---

## Fix 5 — Add missing section: Testing a bundle

Add after the Randomized Rewards section:

### Test a bundle

Use the Test action to send a real reward request to your endpoint before attaching a bundle to a live notification.

1. Find the bundle on the Rewards page and click **Edit ▾ → Test**.
2. Select the tier to simulate under **Test Reward for Audience**.
3. Enter the **User ID** of the player who should receive the reward.
4. Set **Posting User ID** to `0` for app-to-player notifications.
5. Click **Test**.

The dialog shows the full POST request and your server's response.

---

## Fix 6 — Add missing section: Archiving a bundle

Add after the Bundle Creation section:

### Archive a bundle

Archiving removes a bundle from the active list without deleting it. Archived bundles can be restored at any time.

To archive: click **Edit ▾ → Archive**.
To restore: enable **Show archived** in the Filter dropdown, find the bundle, and click **Restore**.

If a bundle is attached to an active notification or link, Teak offers to archive it instead of deleting it.

---

## Fix 7 — Add missing note about combining randomization and tiers

Add to the end of the Tiered Rewarding section:

> You can enable both **Use Reward Tiers** and **Use Random Rewards** on the same bundle. Teak evaluates tiers first to select the reward set, then randomizes within that set.
