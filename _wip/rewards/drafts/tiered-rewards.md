# Tiered rewards

Tiered rewards let you send one notification to a broad audience while giving different rewards to different player segments. The goal is to meet each player where they are in the game — an offer that's exciting for a casual player might not move a big spender at all. A bundle can have any number of tiers, each targeting a different audience.

---

## How tiered rewards work

When a player claims a reward, Teak checks each tier from top to bottom and finds the first one whose audience includes that player. That player receives only that tier's reward — evaluation stops there. Players who don't match any tier receive the **Default Tier** reward.

The Default Tier is always present. It acts as a catch-all for any player not covered by a more specific tier above it.

**Example:** Three tiers in priority order:

| Tier | Audience | Reward |
|---|---|---|
| 1 | Spenders ($100+ in 30 days) | 50,000 coins |
| 2 | Lapsed players (7+ days inactive) | 20,000 coins |
| Default | Everyone else | 1,000 coins |

A player who spent $120 last month matches Tier 1 and receives 50,000 coins. Teak doesn't check Tier 2 or the Default Tier for that player — the first match wins.

---

## Set up tiers on a bundle

For basic bundle setup, see [Reward bundles](reward-bundles.md). To add tiers:

1. Open the bundle editor and check **Use Reward Tiers**.
2. Click **Insert Tier** to add a custom tier above the Default Tier.
3. Select the audience for that tier from the dropdown.
4. Add the rewards players in that audience should receive.
5. Repeat for each additional tier.
6. Use the reorder buttons on each tier to set evaluation priority. The topmost tier is evaluated first.

**Order your tiers from most specific to least specific.** A player who qualifies for a narrower audience (e.g., "Big spenders") should be matched before they can fall into a broader one (e.g., "Spenders"). If "Spenders" sits above "Big spenders," every big spender matches "Spenders" first and never reaches the higher-value tier.

---

## Choose when tiers are evaluated

Teak determines which tier a player belongs to at a specific point in time. This matters because audience membership can change between when a notification is sent and when the player actually opens it.

**Send-time evaluation (notifications and emails)**

The tier is locked when the notification is sent. Each player's reward is determined by their audience membership at that moment, before anyone opens the notification.

Use send-time evaluation when the notification copy references the reward amount — for example, "Here are your 50,000 coins." The amount in the copy and the amount delivered will always match.

**Click-time evaluation (links)**

The tier is re-evaluated when the player opens the notification or clicks the link. The reward is based on audience membership at the moment of the click.

Use click-time evaluation when the most current audience data should determine the reward — for example, if a player's segment might change between send and click.

**Editing a bundle after sending changes evaluation to click-time.** If you modify a bundle after a notification has been sent, the original send-time evaluations are invalidated. Players who haven't clicked yet will have their tier re-evaluated at click time using their current audience membership.

---

## Use template tags with tiers

When you use tiers, the notification copy needs to match each player's actual reward — otherwise a VIP player sees "win up to 100M coins" when their actual ceiling is a billion. Template tags fix this: Teak resolves the tag per-player based on the tier they'll receive, so the copy is always accurate.

To insert a reward tag:

1. In the notification message editor, click the **template tag** button (the variable icon in the toolbar).
2. Under the **REWARDS** section, select the reward item whose amount you want to display.

![The template tag dropdown open in the notification editor, showing the REWARDS section with a reward item available for insertion](images/5_template_tag_insertion.jpg)

For example, if your bundle has a reward called "TacoSalad," the REWARDS section shows "TacoSalad Amount." Inserting it adds a tag that resolves to the exact quantity that player will receive based on their tier.

---

## Common patterns

**Reward loyalty.** Put your highest-spend or most-engaged audience in Tier 1 with a premium reward. The Default Tier gives a standard reward to everyone else.

**Re-engage lapsed players.** Add a tier for players inactive for 7+ days with a larger reward to bring them back. Players still active get a smaller reward from a lower-priority tier or the Default Tier.

**Seasonal events.** Create a time-limited tier with an event-specific audience and a higher reward. Archive the bundle after the event ends, and restore it for the next one.

**Combine with randomization.** Enable both **Use Reward Tiers** and **Use Random Rewards** on the same bundle. Teak evaluates the tier first, then randomizes within that tier's reward set. Each tier can have independent odds. See [Reward bundles](reward-bundles.md) for setup details.
