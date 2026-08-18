# Inkfold — Tester Scenarios

Concrete things to try, organized by feature area. Background on what each
feature is supposed to do is in [KNOWLEDGE-BASE.md](KNOWLEDGE-BASE.md).

You don't need to work through every scenario in one sitting — pick an area,
use it like you'd use it for real work, and file what breaks or confuses
you. Real usage finds more bugs than scripted clicking.

For each scenario: **Goal** → **Steps** → **What "working" looks like**. If
what you see doesn't match, that's worth a report — see
[README.md](../README.md) for how.

---

## A. Getting started

**Goal:** confirm the first-run path is smooth.

1. Sign in with Google at app.inkfold.app (or your assigned tester URL).
2. Go through the onboarding wizard.
3. Send your first chat message.

**Working looks like:** sign-in completes without looping or repeated
validation prompts; onboarding is skippable/completable without dead ends;
first message gets a response within a reasonable time.

---

## B. Core chat

**Goal:** the basic loop is reliable.

1. Start a new chat, send a message, wait for a response.
2. Regenerate a response.
3. Open your chat history and reopen an older conversation.
4. Start a second, unrelated chat and switch between the two.

**Working looks like:** messages send/receive without hanging; regenerate
produces a different or updated answer; history list and reopening both
work; switching chats doesn't mix content between them.

---

## C. Multi-model comparison

**Goal:** the "second opinion" feature works as advertised.

1. Open **Compare**, pick two or more models, send one prompt.
2. Review the answers side by side.
3. Try the synthesis option (if available) to combine the answers.

**Working looks like:** each model's answer is clearly attributed to that
model; answers render fully; synthesis produces a coherent combined answer,
not a garbled concatenation.

---

## D. Cross-session memory (the "aha" test)

**Goal:** this is the core value proposition — test it deliberately.

1. In one session, tell Inkfold something specific about your work/project
   (real or a throwaway test fact — don't use anything sensitive).
2. Start a **new** chat, ideally with a **different model**, a few minutes
   or a day later.
3. Ask a question that requires that earlier context, without repeating it.
4. Check the trace view for that message — does it show memory was used?

**Working looks like:** the new session recalls the earlier context without
being re-told; the trace view shows which memory was drawn on.

**Worth reporting either way:** if it recalls correctly, that's still
useful confirmation — note it as "worked as expected" feedback, not just
failures.

---

## E. Import history

**Goal:** bringing in existing history from another AI tool works cleanly.

1. Go to **Import**, and import a small export from another AI tool (if you
   have one) — a small file is fine for testing.
2. After import, start a new chat and ask something that only the imported
   history would know.

**Working looks like:** import completes with a clear success/failure
state and a sane record count; imported content is later recalled the same
way native conversations are.

---

## F. Privacy modes

**Goal:** each mode actually behaves differently.

1. Have a short conversation in **Smart** mode. Check memory settings
   afterward — content should be there.
2. Start a new conversation in **Private** mode, say something specific.
   Check memory settings — only structure/topology should be visible, not
   the content.
3. Start a new conversation in **Incognito** mode. After ending it, confirm
   nothing about it persists anywhere (history, memory).

**Working looks like:** the three modes are visibly, functionally
different — not just a label. Incognito in particular should leave no
trace after the session ends.

---

## G. Model access & vendor keys

**Goal:** BYOK, managed, and pay-as-you-go all work.

1. Add your own API key for a vendor in **Settings → Vendors**.
2. Send a chat using that key and confirm it's actually being used (check
   the trace/cost view).
3. Remove/rotate the key and confirm the app handles it gracefully (clear
   error, not a crash).
4. If you're on managed or pay-as-you-go, send messages until you're near a
   quota/balance limit and observe what happens at the edge.

**Working looks like:** key add/remove is straightforward; using your own
key is reflected in cost/trace; hitting a quota/balance limit produces a
clear message, not a silent failure or a surprise charge.

---

## H. Billing & cost view

**Goal:** spend is visible and adds up.

1. Open **Billing** and review the invoice list.
2. Send a few chat messages and watch the inline cost panel update.
3. (If you've enabled **Show advanced features**) check the spend dashboard
   for a breakdown across models/vendors.

**Working looks like:** costs shown per message are plausible and consistent
with what you'd expect for the model used; invoice history is accurate.

---

## I. Whiteboards

**Goal:** the freeform workspace is usable.

1. Create a whiteboard, add a few elements.
2. Leave and come back — confirm it persisted.
3. Try it at more than one experience level/appearance setting.

**Working looks like:** content persists; nothing renders broken across
appearance settings.

---

## J. Groups & Rooms

**Goal:** organizing conversations into shared spaces works.

1. Create a group or room.
2. Add a conversation or start one inside it.
3. Navigate in and out, refresh, confirm state holds.

**Working looks like:** structure persists across navigation/refresh; no
orphaned or duplicated rooms.

---

## K. Teams (shared memory)

**Goal:** if you have team access, confirm the "shared brain" actually
shares.

1. From the team workspace switcher, switch into a team context.
2. Have a conversation that references something team-relevant.
3. Confirm (or have a teammate confirm) that context is visible from their
   session too.

**Working looks like:** team members' sessions draw on the same shared
context, not just their own individual memory.

---

## L. Marketplace (Prompts / Playbooks / Routines)

**Goal:** sharing and reusing setups works end to end.

1. Publish a prompt, playbook, or routine.
2. Find it again from the Marketplace (as if you were a different user
   browsing).
3. Use/apply it in a chat.

**Working looks like:** publishing succeeds and is discoverable; applying a
published item actually changes chat behavior as expected (e.g. a persona
prompt changes tone/behavior).

---

## M. Feed, Connections, Shared conversations

**Goal:** the secondary surfaces don't silently break.

1. Open **Feed** — confirm it loads and shows relevant activity.
2. Open **Connections** — confirm connected accounts/integrations show
   correct status.
3. Share a conversation via **Shared**, then open the shared link (ideally
   in a different browser/incognito window) to see the recipient's view.

**Working looks like:** all three load without errors; a shared link shows
a sensible read-only(?) view to someone without your account context.

---

## N. Settings deep dive

**Goal:** the settings surfaces are complete and don't lose data.

1. Update your profile, save, reload — confirm it stuck.
2. Review **Memory settings** → entries — confirm you can see and (if
   supported) delete individual memory entries.
3. Review **Context settings** and **Data settings** — try a data export
   and confirm the download is sane.
4. If you want to test account deletion, **do not do this on your only
   account** — flag it as a scenario you're willing to test on request
   instead.

**Working looks like:** settings persist after reload; memory entries are
inspectable/deletable; data export produces a real, readable file.

---

## O. Appearance & experience levels

**Goal:** every experience level is actually usable — this is a known area
of recent tester feedback (default Novice sidebar reported as broken and
non-responsive).

1. Set Experience level to **Novice**. Check the sidebar and general layout
   at a few window sizes (including narrow/mobile-width).
2. Switch to **Standard**, then **Pro**. Repeat the same layout check.
3. Try at least one theme (light/dark) at each tier.
4. Resize the browser window smaller and larger — does the layout adapt, or
   does it break?

**Working looks like:** all three tiers are readable and navigable at
common window sizes, not just desktop-wide; switching tiers doesn't require
a refresh to take effect; no tier is drastically worse than the others.

---

## P. Advanced features (optional, power testers)

**Goal:** the opt-in "advanced" layer works once unlocked.

1. Enable **Settings → Account → Show advanced features**.
2. Check the spend dashboard and budget dashboard/settings.
3. Set a budget alert threshold low enough to trigger it, confirm the
   banner appears.
4. Check Developer settings and the Glossary link from Help.

**Working looks like:** the toggle reveals these cleanly with no reload
needed; budget alerts actually fire at the threshold; nothing here is
required for a baseline tester, so partial coverage is fine.

---

## Filing what you find

Use the in-app **Report a bug** action when possible, or open an issue
directly using the right template (Bug report / Feature request / UX
feedback). See the main [README](../README.md). Never include prompts,
conversation content, personal data, API keys, or tokens in a public issue.
