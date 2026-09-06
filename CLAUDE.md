# claude-cert-prep-p — Rules & Gates

## What this repo is

Exam prep quiz SPA for CCAR-P (Claude Certified Architect – Professional).
- `quiz.html` — live file; contains all questions + CHEATSHEET_MD
- `offline.html` — must always be an exact copy of quiz.html
- Deployed at: https://xxc2xx.github.io/claude-cert-prep-p/offline.html

---

## NEVER

- Commit without an explicit **"yes"** from Winston — "looks good" is not a yes
- Write to `quiz.html` without first stating the coverage summary (see gate below)
- Commit `quiz.html` without syncing `offline.html` first (`cp quiz.html offline.html`)
- Push to remote without Winston's explicit approval of the commit content
- Invent question content, answers, or cheatsheet facts — source only from official Skilljar course or Anthropic docs

---

## ALWAYS

- Before ANY write to quiz.html, state:
  ```
  Artifact: quiz.html — [section name]
  Content: [what is being written — screens/topics covered]
  Coverage: [what is included vs. what exists in source but is NOT included]
  Gaps: [explicitly list anything left out and why]
  Confirm: yes to proceed?
  ```
  Then wait. Do not write until Winston says yes.

- Before ANY commit, state:
  ```
  Artifact: [file(s)]
  Target: master → GitHub Pages (public)
  Changes: [summary of what changed]
  Confirm: yes to proceed?
  ```
  Then wait.

- After any crawl or content extraction, surface a **coverage report** before writing:
  - How many source screens exist
  - How many are being written to the cheatsheet
  - Which screen types are included (Lesson / Watch Out / Checkpoint / Recap)
  - Which are excluded and why

- Run `cp quiz.html offline.html` before every commit

---

## Content gates for cheatsheet additions

When adding official Skilljar content to CHEATSHEET_MD:

| Screen type | Must be included? |
|-------------|------------------|
| Lesson (teaching) screens | Yes — key frameworks and rules |
| Watch Out screens | Yes — anti-patterns are high-frequency exam distractors |
| Checkpoint screens | Yes — the tested decision scenario |
| Recap / Takeaway screens | Yes — the numbered rules the exam tests directly |
| Module Intro / Complete | No — orientation only |

If any required type is excluded, state the gap explicitly and get approval before writing.

---

## Stack

- Single HTML file — all JS/CSS inline, no build step
- Question bank stored as `const QUESTIONS = [...]`
- Cheatsheet stored as `const CHEATSHEET_MD = \`...\``
- `mdToHtml()` renders markdown to HTML at runtime
- GitHub Pages serves `offline.html` as the public URL

## Question quality rules

- Each question must have a plausible distractor set (no obviously short wrong answers)
- Multi-select questions must use `answerSet` array, not a single `answer` string
- Elimination button (✕) must be present on all choices pre-lock
- Correct answer must not be identifiable by length alone
