## What this repo is

Antora documentation source for **docs.teak.io** — the user guide, FAQ, and 3rd-party integration guides. AsciiDoc only, no application code. SDK reference content (Unity / iOS / Android / JS / server-api) lives in sibling repos and is composed in at build time via the navigation includes in `modules/ROOT/nav.adoc`.

## Build & preview

There's no local build step in this repo. CircleCI runs `teak/build-antora-playbook` from the `teak/sdk-utils@0.7.0` orb (see `.circleci/config.yml`).

Local preview lives in `../antora-ui-teak` (sibling checkout). Its `Procfile` runs a `live-server` on the built site plus a `chokidar` watcher that already includes `teak-usage/**/*` — so edits here trigger a rebuild against the dev playbook (`playbook/antora-playbook-dev.yml`). Start it with `foreman start` (or `npx foreman start`) from `antora-ui-teak`. Don't try to run Antora from inside `teak-usage`.

## Layout

Three Antora modules under `modules/`:

- `ROOT/` — landing page, developer quickstart, FAQ, support, newsletters. **All site navigation lives in `ROOT/nav.adoc`** (there's no `user-guide/nav.adoc`); that file also `include::`s nav partials from the SDK repos.
- `user-guide/` — dashboard usage (audiences, scheduling, notifications, email, rewards, links, reporting, settings, glossary).
- `integrations/` — 3rd-party setup guides (APNs, FCM, ADM, SendGrid).

Cross-references use `xref:<module>:page$<file>.adoc[Title]`. When you add or rename a page, update `modules/ROOT/nav.adoc` — Antora won't surface orphan pages.

`_wip/` is scratch space for drafts and planning docs. Antora ignores anything outside `modules/`, so nothing in `_wip/` ships. Don't link to it from published pages.

## Writing conventions

Match the surrounding page's voice — task-oriented, short sentences, sentence case headings. Recent reward-page history (see `git log -- modules/user-guide/pages/rewards.adoc`) shows the terminology is contested and context-dependent:

- "notifications" for push specifically; "messages" when the text covers push + email together
- "rewards" generally, but "incentives" / "prizes" are fine when describing the player-facing value proposition
- "players" not "users" in game-facing copy

When in doubt, read the page you're editing and the most recent commits touching it before changing terminology globally.

## Branching

Per global conventions: `docs/`, `feat/`, `fix/`, `maint/` prefixes, single-purpose branches. Most work here is `docs/<topic>`.

## Committing

When making a commit, ensure you include a human/claude interaction log. This is mandatory, and captures the human intent of actions you perform. Make the humans accountable.

```
## Human-Claude Interaction Log

### Human prompts (VERBATIM - include typos, informal language, COMPLETE text):
**Include EVERY prompt since last commit - even short ones, corrections, clarifications**
1. "[Copy-paste ENTIRE first prompt since last commit]"
   → Claude: [What Claude did in response]

2. "[Copy-paste ENTIRE second prompt - including [Request interrupted] if present]"
   → Claude: [How Claude adjusted]

[Continue numbering ALL prompts - don't skip any or judge importance]

```

Be sure to end your commit with Claude attribution

```
🤖 Generated with Claude Code
Co-Authored-By: Claude <noreply@anthropic.com>
```
