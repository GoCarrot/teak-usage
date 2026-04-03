# Pass 1 patch — Server-to-Server Reward API page

Minimal surgical fixes for the live page at https://docs.teak.io/server-api/latest/rewards/endpoint.html.

---

## Fix 1 — Terminology in Overview

**Current:**
> ...in response to a player clicking a notification, email, social post, or Teak Link.

This line is already using "player" and "notification" correctly. No change needed.

**Current (Testing section):**
> ...create a test bundle, enter a player ID, and click "Test" to view the POST request details and server response.

This is also fine. No change needed.

**Current (Parameters table — `post_type` description):**
> String identifying the message or link in the Dashboard

**Replace with:**
> String identifying the notification or link in the dashboard

---

## Fix 2 — Tighten passive voice

**Current (Processing Requirements, step 1):**
> Validate the signature against the server secret

This is already imperative. Review the full page for any remaining passive constructions:

- "The signature is computed by…" → "Compute the signature by…" *(apply if this phrasing appears)*
- "The response must contain…" → "Respond with…" *(apply if this phrasing appears)*

*Note: fetch the current rendered page to apply these precisely — the text above was reconstructed from a summary.*

---

## Fix 3 — Add cross-reference to Reward Bundles

In the Testing section, after the existing test instructions, add:

> For an overview of how bundle IDs map to reward configurations, see [Reward bundles](../user-guide/rewards.html).

---

## Fix 4 — Flag for eng review

The following items should be confirmed by engineering before the next doc release:

- Is the endpoint URL current?
- Is `clicking_user_id` still the correct parameter name, or has it been renamed?
- Are `is_mobile` and `is_unity_webgl` the only valid `extra_flags` values?
- Is `TEAKOK` still the expected success response body, or are there variants?
