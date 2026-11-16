# please-hire-me: club edition

A club-meeting kit built on [alecswang/please-hire-me](https://github.com/alecswang/please-hire-me)
(MIT). The original is an agent that fills out real job applications from your resume, using the
company's own Greenhouse / Lever / Ashby form. It needs a paid Claude Code plan. This repo adds two
branches so people on free accounts can follow the same track.

## Pick your track

| You have | Track | Branch | Who clicks Submit |
|---|---|---|---|
| Paid Claude (Pro/Max) with Claude Code + the Claude in Chrome extension | **1. Claude Code** | `main` (this branch) | The agent, after you say yes at the checkpoint |
| A free claude.ai account, nothing else | **2. Free Claude** | [`free-claude`](../../tree/free-claude) | You. Claude is the brain, you are the hands |
| A free ChatGPT account (Codex CLI) | **3. Free Codex** | [`free-codex`](../../tree/free-codex) | You (recommended) or Codex, after you say yes |

Every track ends in the same place: **one real application, reviewed by you before it is sent.**

```bash
# Tracks 2 and 3: clone only your branch
git clone --branch free-claude --single-branch https://github.com/BonaOQuinn/please-hire-me-club.git
git clone --branch free-codex  --single-branch https://github.com/BonaOQuinn/please-hire-me-club.git
```

## The shared meeting flow

| Step | What happens |
|---|---|
| 1. Setup (about 10 min) | The AI reads your resume, asks one list of questions, and drafts your three config files. It never invents a fact about you. |
| 2. Pick a posting | One real, live opening that matches your targets. |
| 3. Answer sheet | Every question on the form, answered only from your config. Unknown facts become `NEEDS HUMAN`. |
| 4. **Checkpoint** | You review every answer before anything is submitted. |
| 5. Log | The application is recorded so you never apply to the same company twice by accident. |

## Track 1: Claude Code (this branch)

**You need:** [Claude Code](https://claude.com/claude-code) on a paid plan, Chrome with the
[Claude in Chrome](https://claude.ai/chrome) extension signed in to the same account, and your
resume as a PDF.

```bash
git clone https://github.com/BonaOQuinn/please-hire-me-club.git please-hire-me
cd please-hire-me
claude
```

Then type **"set me up"**. Claude reads your resume, shows you every value it extracted, asks one
numbered question list, drafts `config/answers.md`, and writes your config. At the end it fills one
real posting, shows you every answer, and **submits only after you say yes** (say no and it closes
the tab and sends nothing).

For the club, set `schedule.frequency` to `manual` and do not install the scheduler: scheduled runs
submit with no checkpoint. To get a checkpoint on every run, ask Claude in chat for "one
application, stop before submitting".

The full upstream documentation is in [`docs/UPSTREAM-README.md`](docs/UPSTREAM-README.md), and the
agent's playbook is [`CLAUDE.md`](CLAUDE.md).

## Track 2: Free Claude

No Claude Code, no extension. See the [`free-claude`](../../tree/free-claude) branch.
You paste a playbook into a claude.ai chat; Claude drafts your config and your answer sheet, and you
paste the answers into the form and click Submit yourself.

## Track 3: Free Codex

OpenAI's Codex CLI with a ChatGPT sign-in and a Playwright browser. See the
[`free-codex`](../../tree/free-codex) branch.

## Good to know

- **Your data stays local.** `config/profile.json`, `config/answers.md`, `config/settings.json`,
  `applications/`, `logs/` and `screenshots/` are gitignored. Do not commit them to a public repo.
- **Sign-ins, 2FA and CAPTCHAs are always yours.** No track creates accounts or types passwords.
- **Applications are real.** Only apply to roles you actually want.
- Credit: all the playbook and scripts are from
  [alecswang/please-hire-me](https://github.com/alecswang/please-hire-me), MIT licensed.
