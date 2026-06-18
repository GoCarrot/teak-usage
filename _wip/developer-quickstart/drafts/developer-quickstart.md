# Developer Quick Start

Teak runs through a platform SDK on the client, plus a couple of server-side touchpoints. This page gives you the shape of an integration and points you to the right guide for your platform.

---

## The shape of every Teak integration

However your game is built, a Teak integration is the same five steps. Each platform's quickstart walks you through them with the specifics for that platform:

1. **Create your game in the Teak Dashboard.** You get an app ID and an API key.
2. **Install the SDK** for your engine or platform.
3. **Identify the player** so Teak knows who's playing and can target and reward them.
4. **Ask for push permission** so you can reach players when they're not in the game.
5. **Send a test notification** to confirm the integration end to end.

Keep these five beats in mind as you follow your platform's quickstart — each one is just this flow with the platform's details filled in.

---

## Choose your SDK

Pick the SDK that matches how your game is built, then follow its quickstart.

<!-- GRADUATION NOTE: reuse the existing `[.iconblock]` nav-table from the current page
     (Unity / JavaScript / iOS / Android SVG icons). Keep the icons; add the one-line
     decision aid under each. Links below are the xref targets to use. -->

- **[Unity SDK Quickstart](xref:unity::page$quickstart/index.adoc)** — one SDK for iOS, Android, and WebGL / Facebook Canvas. Start here if your game is built in Unity.
- **[JavaScript SDK Quickstart](xref:javascript::page$quickstart/index.adoc)** — for web and Facebook Canvas games.
- **[iOS Native SDK](xref:ios::page$integration.adoc)** — for native iOS apps.
- **[Android Native SDK](xref:android::page$integration.adoc)** — for native Android apps.

> Push setup (Apple APNs, Android FCM) is part of each platform's quickstart — you don't need to gather credentials before you start.

---

## Server-side: the Reward Endpoint

Most of Teak is client-side, but rewarding runs through your backend. Start with the **[Reward Endpoint](xref:server-api::page$rewards/endpoint.adoc)** (players love free coins), then see the **[Server API overview](xref:server-api::page$index.adoc)** for the full set of backend features.

---

## Before you start

Make sure you have:

- A game project (iOS, Android, or Facebook).
- The ability to test new builds on devices or simulators/emulators.
- Access to logs (device console or Unity console) so you can review Teak's debug output.
