# Developer Quickstart refresh plan

**Status:** Proposal
**Date:** 2026-06-18
**Scope:** 1 page rewritten in place (`developer-quickstart.adoc`) · ~half a day. Pass-1 surgical fixes are shippable immediately, independent of the rewrite.

---

## What this plan does

Reframe the central Developer Quick Start as a **router, not a runbook**. Its job is orientation: give a developer the universal shape of a Teak integration, help them pick the right SDK, and point them at the platform quickstart (and the server-side Reward Endpoint) that own the actual steps. It removes the sections that duplicate — and have drifted out of date against — each platform's own quickstart.

This came out of a technical-writer audit comparing the central page to each SDK's quickstart. The audit found the central page is half router, half parallel quickstart, and the "parallel quickstart" half is both redundant and stale.

---

## Page-by-page plan

### 1. Developer Quick Start (`modules/ROOT/pages/developer-quickstart.adoc`) — rewrite in place

**Current state:** Useful, unique parts: the SDK-chooser icon table and the Server-API pointer. Redundant parts: "Preparing Your Game," "Push Credentials," and "Next Steps" re-document per-platform install/push steps that each SDK's quickstart already owns (Unity has `apple-apns` + `firebase-fcm`; iOS has `apple-apns`; etc.). Some of it is stale: legacy `sdks.teakcdn.com/...` manual-download links the platform install pages no longer use (they use SPM/CocoaPods/Gradle/UPM), and an Android link mislabeled "iOS Native Integration."

**What changes:** Subtract the duplicated platform mechanics; add one clear universal-flow overview; keep and sharpen the routing. The page gets shorter.

**Proposed structure:**

- **Intro (1-2 sentences)** — what a Teak integration looks like, and where to go for your platform.
- **The shape of every Teak integration** — the five universal beats, one line each, platform-agnostic:
  1. Create your game in the Teak Dashboard (get app ID + API key)
  2. Install the SDK
  3. Identify the player
  4. Ask for push permission
  5. Send a test notification

  Framed as: every platform quickstart *is* this flow, with platform specifics. This is the mental model the page exists to give — no platform quickstart can, because each only sees its own.
- **Choose your SDK** — the existing icon table, plus a one-line decision aid: **Unity** (covers iOS, Android, WebGL/Facebook Canvas) · **native iOS** · **native Android** · **JavaScript** (web / Facebook Canvas). Each links to that SDK's quickstart entry.
- **Server-side: Reward Endpoint** — keep the existing pointer; the one thing no SDK quickstart covers. Lead with the Reward Endpoint, then the Server API overview.
- **Before You Start** — trimmed universal prerequisites (a game project; ability to test builds; access to logs). Short.
- **Removed:**
  - "Preparing Your Game" — per-platform tips + stale download links; owned by the platform install pages.
  - "Push Credentials" — owned by each SDK's `apple-apns` / `firebase-fcm` step. Replace with one sentence noting push setup lives in the platform quickstart.
  - "Next Steps" — just re-listed the SDK table.

**Screenshot placement (this page):** None. A router page is a short overview plus links; no screenshot earns its place.

---

## Terminology / style alignment

| Instead of | Use |
|---|---|
| `http://sdks.teakcdn.com/...` manual-download links | a pointer to the platform's `install-sdk` quickstart page |
| "iOS Native Integration" (the label on the Android link) | "Android Native Integration" |
| "Preparing Your Game" / "Push Credentials" as central how-tos | one-line pointers into the platform quickstarts |
| platform-specific install/push instructions on the central page | none — each SDK quickstart owns them |

Note: the "Game" vs. "their game" naming overlap (raised in GitHub Carrot#1423) is a known product-naming question. Out of scope here — keep "game"; don't try to resolve it in this refresh.

## Scope estimate

| Work item | Effort |
|---|---|
| Pass 1 — surgical fixes to the live page (dead `teakcdn` links, the "iOS Native Integration" mislabel) | ~15 min · ship now |
| Pass 2 — full router-rewrite draft (`drafts/developer-quickstart.md`) | ~1–2 hrs |
| Review + graduate (md → adoc, build, verify) | ~30 min |
| **Total** | **~half a day** |

## What this plan doesn't do

- Does not touch the platform SDK quickstarts (Unity/iOS/JS) — they own the real steps and stay as-is.
- Does not fix the Android quickstart-parity gap — tracked separately as **C-851**.
- Does not apply or salvage the stashed Step 1-8 draft — parked; its runbook model is explicitly rejected for the central page.
- Does not resolve the "Game" → "Project" naming question (Carrot#1423) — product decision.
- Does not add screenshots.

## How to evaluate whether this worked

After the refresh ships, check:

1. Does the page contain **zero** per-platform install or push-credential *instructions* (pointers only)?
2. Are there **no** `sdks.teakcdn.com` links or other stale download URLs left?
3. Can a new developer read the page top-to-bottom in under a minute and come away knowing (a) the five-step shape and (b) which SDK to open next?
4. Does every SDK link land on that SDK's quickstart entry, with a correct label?
5. Is the page strictly shorter than before, with the unique value (SDK chooser + Reward Endpoint pointer) preserved?
