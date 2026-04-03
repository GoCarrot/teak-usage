# Reward bundles

A reward bundle is a reusable reward configuration you attach to notifications and links. A bundle can give players fixed rewards, randomly selected rewards, tiered rewards based on audience membership, or any combination of those.

Bundles live in **Rewards → Reward Bundles**.

---

## Create a bundle

You can create a bundle from the Rewards page, or directly from the notification editor while setting up a notification.

**From the Rewards page:**

1. Select **Rewards** from the left navigation.
2. Click **New Reward Bundle**.
3. Enter a name.
4. Add at least one reward: select the reward type and enter the amount.
5. Set how many days players have to claim the reward under **Reward expires**.
6. Click **Save**.

**From the notification editor:**

Open or create a notification, find the **Reward Bundle** field, and click to create a new bundle inline. The same editor opens and the bundle is saved to your library when you save.

### Reward types

Items and currency must be defined in code by your engineering team before they appear in the bundle editor. To add or review them, go to **Rewards → Items & Currencies**, enter a display name, and enter the internal ID that matches the code name exactly.

Display names appear in the dashboard only — they don't appear in notifications.

### Claim window

The **Reward expires** field sets how many days a player has to claim the reward after receiving the notification. After this window closes, the reward is no longer available. Set this based on how long you expect players to wait before opening a notification — one to seven days is typical.

---

## Add randomized rewards

The same reward every day gets boring. Check **Use Random Rewards** to give players a reason to wonder what they'll get — you can offer a range from a modest base reward up to a high-value jackpot, while keeping your average payout exactly where you want it.

Teak picks one option per claim, selected at random based on weighted chances.

1. Check **Use Random Rewards** in the editor.
2. Add each reward option with its amount.
3. Set the **Chance** percentage for each option. All chances in a tier must add up to 100%.

Teak shows the average claim value at the bottom of each tier. This is the number to check for economy balancing — a random bundle where options range from 1M to 100M coins can have the same average payout as a fixed 5M coin bundle, so you can add excitement without changing what you're actually spending on rewards.

**Non-randomized bundles deliver all rewards.** When **Use Random Rewards** is off, players receive every item in the bundle — all reward types and all amounts at once.

![The bundle editor with both Use Reward Tiers and Use Random Rewards enabled. Tier 1 is assigned to a specific audience and has three randomized reward options with weighted chances. The Default Tier applies to everyone else and has two randomized options.](images/2_bundle_editor_randomized.jpg)

---

## Add tiered rewards

For high-spend or deep-progression players, a reward that excites a typical player might barely register. Tiers let you send one notification and still give each player an offer that's meaningful at their level — without creating separate notifications for each segment.

Check **Use Reward Tiers** to assign different rewards to different segments of players.

Teak evaluates each tier from top to bottom. The first tier whose audience includes the player applies — that player receives only that tier's reward. Players who don't match any tier receive the **Default Tier** reward. The Default Tier is always present and can't be removed.

1. Check **Use Reward Tiers** in the editor.
2. Click **Insert Tier** to add a custom tier above the Default Tier.
3. Select an audience for the tier.
4. Add the rewards players in that audience should receive.
5. Use the reorder buttons on each tier to set evaluation priority. Put your most specific audiences at the top — if a broad audience like "All spenders" sits above a narrow one like "Big spenders," big spenders match the broader tier first and never receive the higher-value reward.

For full details on evaluation timing and template tag integration, see [Tiered rewards](tiered-rewards.md).

---

## Combine randomization and tiers

Both features can be active on the same bundle. Check **Use Reward Tiers** and **Use Random Rewards** together.

Teak evaluates tiers first to select the reward set for that player, then randomizes within that set. Each tier can have its own reward options with independent chances.

---

## Test a bundle

Test a bundle to verify the right tier resolves and the reward payload is correct before attaching it to a live notification.

1. Find the bundle on the Rewards page and click **Edit ▾ → Test**.
2. Under **Test Reward for Audience**, select the tier to simulate.
3. Enter the **User ID** — the game-assigned ID of the player who should receive the reward.
4. Set **Posting User ID** to `0` for app-to-player notifications, or to the sharing player's ID for social rewards.
5. Select any applicable **Extra Flags** (`is_mobile`, `is_unity_webgl`).
6. Click **Test**.

Teak sends a real POST request to your reward endpoint. The dialog shows the full request and your server's response so you can confirm the integration is working.

![The Test Reward Bundle dialog showing the audience selector, User ID field, Posting User ID field, and Extra Flags options](images/3_bundle_test_flow.jpg)

---

## Duplicate a bundle

To copy an existing bundle as a starting point:

1. Click **Edit ▾ → Duplicate**.

Teak creates a copy with a new name and opens it in the editor. The copy is independent — changes to it don't affect the original. Duplicating is especially useful when adding tiers to an existing non-tiered bundle: duplicate first, add the tiers to the copy, and keep the original as a fallback.

---

## Archive a bundle

Archiving removes a bundle from the active list without deleting it. Archived bundles can be restored at any time.

**To archive:**
1. Click **Edit ▾ → Archive**.

**To restore:**
1. On the Rewards page, open the **Filter** dropdown and enable **Show archived**.
2. Find the bundle and click **Restore**.

If a bundle is attached to an active notification or link, Teak won't delete it — it will offer to archive it instead. This preserves the bundle's reward configuration for reference even after it's no longer in active use.
