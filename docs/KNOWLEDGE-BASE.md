# Inkfold — Tester Knowledge Base

This page explains what Inkfold is and does, so you know what you're looking
at while testing. For step-by-step things to try, see
[TEST-SCENARIOS.md](TEST-SCENARIOS.md). For how to report what you find, see
the main [README](../README.md).

## What Inkfold is

Inkfold is a private-by-default chat workspace with one memory that follows
you across every major AI model — Claude, ChatGPT, Gemini, and others — so
you don't have to re-explain your context every time you switch tools, and
you can ask several models the same question and compare their answers side
by side.

The problem it's solving: every AI chat tool today is its own island. What
you tell one model, the next one knows nothing about. Switch tools or
devices and you start from zero. Inkfold gives you one continuous memory
across models instead.

## The core ideas

- **Cross-model memory.** Inkfold remembers context across sessions and
  across models. Ask something today, and a different model tomorrow can
  draw on it.
- **Multi-model chat, three ways.**
  - **Single** — pick one model, chat normally.
  - **Compare** — send the same prompt to several models at once and see
    the answers side by side (a "second opinion").
  - **Synthesis** — have multiple models' answers combined into one.
- **Privacy is a per-conversation choice, not a paid feature.** Three modes,
  all encrypted at rest:
  - **Smart** (default) — full memory, best experience.
  - **Private** — stores only structure/topology, not the content of what
    you said.
  - **Incognito** — nothing is persisted at all.
- **Flexible model access.** Bring your own API key (BYOK), use Inkfold's
  managed access under a quota, or pay as you go — these can be mixed.

## What powers Inkfold

Inkfold is built on **FusionLayer** — a shared memory and multi-model
evaluation engine. FusionLayer is what actually remembers your context and
carries it across models, and what runs a prompt against several models at
once when you use Compare or Synthesis. The three privacy modes described
above are enforced by the engine, not bolted on by the app.

The split matters if you hit something odd while testing: a bug in *what
Inkfold looks like or how it behaves* is an Inkfold issue, while a bug in
*what gets remembered, what a model was given, or how answers get combined*
usually lives in the engine. You do not need to work out which is which —
report what you saw and we will route it — but it explains why some fixes
land quickly and others take a release.

More about the engine: https://fusionlayer.app

## Feature tour

Everything below is live in the alpha and fair game to test. Rough nav
location is in parentheses — exact wording may drift as the UI changes.

| Feature | What it does | Where to find it |
|---|---|---|
| Chat | Core single-model conversation, composer, thread, history | Chat |
| Compare | Same prompt to multiple models side by side, or synthesized into one answer | Compare |
| Import conversations | Bring in existing history from other AI tools so memory isn't starting from empty | Import |
| Memory settings | See and manage what Inkfold remembers about you | Settings → Memory |
| Privacy modes | Switch Smart / Private / Incognito per conversation | Settings → Privacy (also selectable per-chat) |
| Vendor / model settings | Add your own API keys, pick default models | Settings → Vendors, Settings → Models |
| Billing & cost | Invoices, pay-as-you-go balance, cost panel inline in chat | Billing |
| Whiteboards | Freeform visual workspace | Whiteboards |
| Groups & Rooms | Shared spaces for organizing conversations/work | Groups, Rooms |
| Teams | Shared team memory — everyone's session starts from the same context | Team (workspace switcher) |
| Marketplace (Prompts / Playbooks / Routines) | Share and reuse prompts, personas, and repeatable workflows | Marketplace, Playbooks, Routines |
| Feed | Activity/updates stream | Feed |
| Connections | Manage connected accounts/integrations | Connections |
| Shared conversations | Share a conversation via link | Shared |
| Appearance | Experience level (Novice / Standard / Pro), theme, layout | Settings → Appearance |
| Help | In-app help articles + chat widget | Help |

**Advanced (opt-in) features** — hidden by default; enable via
**Settings → Account → Show advanced features**:

| Feature | What it does |
|---|---|
| Spend dashboard | AI spend broken down across models/vendors |
| Budget dashboard & alerts | Set spend budgets and get warned near the limit |
| Developer settings | Lower-level configuration for power users |
| Glossary | Definitions of Inkfold-specific terms |

These are intentionally tucked away from new users — testing them is useful,
but don't expect a first-time user to find them without the toggle.

## Experience levels & appearance

Inkfold ships three experience tiers, each a genuinely different layout, not
just a re-skin:

| Tier | Layout | Who it's for |
|---|---|---|
| **Novice** | Centered single-column chat, collapsible sidebar, minimal chrome | New users — "just chat" |
| **Standard** | Nav rail + dashboard home + status bar | Regular users who want more visible controls |
| **Pro** | Activity bar + trace inspector pinned + dense status bar | Power users who want everything visible |

Switch tiers from **Settings → Appearance**. Theme (light/dark/color) and
general appearance (font, density, motion) are separate, orthogonal
settings — you can mix any theme with any experience level.

This is an active area — if a layout looks broken, unresponsive, or hard to
navigate at a given tier, that's exactly the kind of feedback we want (see
[TEST-SCENARIOS.md](TEST-SCENARIOS.md) §Appearance).

## What's solid vs. what's still rough

Being upfront about this is deliberate — early alpha, bugs expected, and
knowing what's still shaky helps you file more useful reports.

**Should work well:**
- Multi-model chat (single / compare / synthesis)
- Cross-session memory + the trace view (see which model answered, what
  memory was used, at what cost)
- Import of existing history from other AI tools
- The three privacy modes
- BYOK, managed access, pay-as-you-go
- Team shared memory
- Marketplace, Playbooks, Routines
- Appearance/theme system

**Known rough edges:**
- **Desktop is the primary experience.** Mobile web works but is rougher —
  expect more issues there.
- **Developer-workflow integrations** (CLI / editor / sync daemon) are still
  being stabilized — not part of the current testing scope.
- It's genuinely early alpha — expect bugs. Report them; that's the point.

## Environments

- **Production:** https://app.inkfold.app
- **Tester environment:** https://test.inkfold.app (planned — uses separate
  data from production; use this for assigned staging work once access is
  provided)

## The tester perk

Active testers who provide substantive feedback receive, as a thank-you,
**free unlimited conversation-history retention for 3 years** (the Free plan
normally retains history for a limited period). This is a goodwill benefit,
not payment or compensation — standard usage quotas still apply, and it
costs you nothing to earn: just use Inkfold on real work and tell us what
breaks or confuses you.

## Reporting what you find

See the main [README](../README.md) and [SECURITY.md](../SECURITY.md).
Short version: use the in-app **Report a bug** action when you can, pick the
right issue template (Bug report / Feature request / UX feedback), and never
include prompts, conversation content, personal data, API keys, or tokens in
a public issue — route anything sensitive through the private channel
instead.
