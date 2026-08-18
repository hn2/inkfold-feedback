# Opening a tester report as a GitHub issue

Paste this whole prompt as your first message in Claude Code, then paste the
raw tester text from Discord right below it (one tester report per run).
Anyone can use this — just needs `gh` authenticated as whichever GitHub
account is running it.

## Setup (one-time)

```bash
gh auth login
gh auth status
gh repo view hn2/inkfold-feedback
```

If the last command fails, `gh` isn't authenticated against the right
account yet — fix that before using this prompt.

## The prompt

```
You are opening a tester report as an issue on hn2/inkfold-feedback (a
public, issue-tracker-only repo — no source code lives here).

Repo rules (from README.md and SECURITY.md — do not violate these):
- Every issue must fit one of three templates: Bug report (label: bug),
  Feature request (label: enhancement), UX feedback (label: ux).
- NEVER file a public issue that contains prompts, conversation content,
  personal data, API keys, access tokens, or a security/privacy report.
  If the tester text contains any of that, STOP — do not draft an issue.
  Tell me to route it through the private support channel instead, and
  quote only the minimal non-sensitive part needed to explain why.

Below the "---TESTER TEXT---" marker is a raw, possibly messy message (or
thread) copied from Discord. Do this:

1. Extract the actual bug/feature/UX report from the noise (chit-chat,
   emoji reactions, unrelated messages).
2. Search hn2/inkfold-feedback for anything similar, covering BOTH open
   and closed issues:
   gh issue list -R hn2/inkfold-feedback --state all --search "<keywords>" --limit 30
   Read titles/bodies of plausible matches with `gh issue view` before
   deciding — keyword search misses paraphrases, so use judgment, not
   just exact string matches.
3. Decide one of three outcomes:
   a. NO MATCH → draft a NEW issue using the matching template's exact
      section headings (Bug report / Feature request / UX feedback).
      Fill every field you have evidence for; leave others blank rather
      than inventing detail. Add a closing line "Reported via Discord by
      <tester name/handle>." for traceability.
   b. MATCH, issue is OPEN → do NOT create a new issue. Draft a comment
      to add to the existing issue: brief note that another tester hit
      the same thing, any new repro detail this report adds that the
      original lacked, and the reporter attribution line.
   c. MATCH, issue is CLOSED → do NOT create a new issue and do NOT try
      to reopen it (some accounts only have Read access and reopening
      can fail with a permission error). Draft a comment noting it has
      recurred, then tell me explicitly to reopen it myself if it needs
      it — don't attempt `gh issue reopen`.
4. Show me the exact draft (title + body, or comment text) and the exact
   `gh issue create` / `gh issue comment` command you'd run, with the
   issue number for (b)/(c). Do NOT run it.
5. Wait for me to say "go" (or give edits) before executing anything.

---TESTER TEXT---
<paste the tester's Discord message(s) here>
```

## Notes

- Search is intentionally `--state all` so closed-and-fixed reports get
  caught and turned into "already fixed, here's the issue" instead of a
  duplicate.
- The permission note in step 3c exists because `hn2/inkfold-feedback` is
  a personal-account repo: an account with only Read access can comment
  but not close/reopen/label others' issues (personal repos have no
  Triage tier). The `hn2` account has full access and can reopen
  directly if needed.
