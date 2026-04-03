# Server-to-server reward API

The Teak reward endpoint lets you issue virtual currency or items when a player clicks a notification, email, social post, or Teak Link. You implement a server-side endpoint that validates each request, grants the reward, and confirms success.

---

## How it works

When a player clicks a rewarded notification or link, Teak sends a POST request to your endpoint with the reward details. Your server validates the request, grants the reward, and responds with `TEAKOK`.

Teak retries failed requests automatically. Use the `event_id` parameter to deduplicate retries on your side.

For information on how reward configurations map to the `reward` payload, see [Reward bundles](../user-guide/rewards.html).

---

## Request format

Teak sends `POST` requests with `Content-Type: application/x-www-form-urlencoded`.

### Parameters

| Parameter | Type | Description |
|---|---|---|
| `app_id` | string | Your application identifier |
| `clicking_user_id` | string | Player ID of the reward recipient |
| `event_id` | string | Unique ID for this reward grant — use this for idempotency |
| `post_id` | integer (64-bit) | ID of the notification or link that was clicked |
| `post_type` | string | Identifies the notification or link in the dashboard |
| `posting_user_id` | string | Player ID of the sharer; `0` for app-to-player notifications |
| `reward` | JSON string | Dictionary of reward items and amounts, e.g. `{"coins": 25, "energy": 10}` |
| `timestamp` | integer | UNIX timestamp of the initial reward attempt |
| `signature` | string | SHA256 HMAC validation token |

---

## Validate the signature

Compute the expected signature and compare it to the `signature` parameter before processing any request.

1. Collect all POST parameters **except** `signature`.
2. Sort the keys alphabetically.
3. Build the string: `key=CGI.escape(value)` for each pair, joined with `&`.
4. Sign the string using SHA256 HMAC with your **Server-to-Server Teak App Secret** as the key.
5. Base64-encode the result.
6. Compare to the `signature` parameter. Reject the request if they don't match.

---

## Process the reward

After validating the signature:

1. Check whether you've already processed this `event_id`. If yes, return HTTP 200 with `TEAKOK` — don't grant the reward again.
2. Decode the `reward` JSON string and grant each item and amount.
3. Return HTTP 200 with the response body `TEAKOK`.

Any response other than HTTP 200 with `TEAKOK` is treated as a failure. Teak will retry.

---

## Test your endpoint

Before going live, use the bundle test tool to send a real reward request and inspect the server response.

1. Go to **Rewards → Reward Bundles**.
2. Find a bundle and click **Edit ▾ → Test**.
3. Enter a player ID and click **Test**.

The dialog shows the full POST request Teak sent and your server's response. See [Reward bundles — Test a bundle](../user-guide/rewards.html#test-a-bundle) for details.

---

## Verify reward delivery

To look up whether a specific player received a reward:

1. Go to **Rewards → Audit Log**.
2. Enter the player's unique identifier.
3. Filter by status (Success / Failure) and date range.

Results show the time, the notification or link identifier, the reward details, and the server response code.

---

## Engineering review notes

*The following items should be verified against the current implementation before publishing:*

- Confirm the endpoint URL is current.
- Confirm `clicking_user_id` is still the correct parameter name.
- Confirm `is_mobile` and `is_unity_webgl` are the only valid extra flag values accepted during testing.
- Confirm `TEAKOK` is the only accepted success response body, or document any variants.
