# please-hire-me: Track 3, Free Codex

For people with a **free ChatGPT account** who can run OpenAI's **Codex CLI**. Codex reads your
resume, writes your config, finds a live opening, and fills the company's real application form in
a browser window you can watch. It stops before Submit, so **you review every answer and click
Submit yourself.**

Based on [alecswang/please-hire-me](https://github.com/alecswang/please-hire-me) (MIT). The other
tracks are on the [`main`](../../tree/main) (paid Claude Code) and
[`free-claude`](../../tree/free-claude) (chat only) branches.

## What you need
- A ChatGPT account (free is fine for the club; the free tier has usage limits, so a long session
  can run out. Check OpenAI's current Codex limits before the meeting.)
- Node.js 20+ and Python 3, plus Git
- Chrome or Chromium installed
- Your resume as a PDF
- **Windows:** run everything in WSL (recommended) or Git Bash. **macOS and Linux:** any terminal.

## What is in this branch

| Path | Why it is here |
|---|---|
| `AGENTS.md` | Tells Codex how to run the playbook with Playwright and the checkpoint. |
| `CLAUDE.md` | The playbook itself (the file name is historical; Codex follows it via `AGENTS.md`). |
| `config/*.example.*`, `config/spec.md`, `config/documents.md` | Templates and rules for your config and for answers and cover letters. |
| `data/` | Live company boards, field notes, sourcing lists, and the posting queue template. |
| `scripts/` | Sweeps that find postings, the duplicate checker, and the answer-quality checker. |

Left out on purpose: the scheduler, the Gmail code broker, the LaTeX resume tailoring and the
Claude-only hooks.

## The track

**1. Install Codex (2 min).**

```bash
npm install -g @openai/codex
codex
```

Choose **Sign in with ChatGPT** when it asks.

**2. Get the repo (1 min).**

```bash
git clone --branch free-codex --single-branch <this-repo-url> please-hire-me
cd please-hire-me
```

**3. Add the browser (3 min).** Codex needs a browser it can drive. Add the Playwright MCP server:

```bash
codex mcp add playwright -- npx @playwright/mcp@latest
codex mcp list
```

If that command is not in your Codex version, add the same server to `~/.codex/config.toml`:

```toml
[mcp_servers.playwright]
command = "npx"
args = ["@playwright/mcp@latest"]
```

Playwright opens a visible browser window. Leave it visible so you can watch and sign in to sites
yourself when needed.

**4. Set up (10 min).** Start Codex in the repo folder (`codex`) and send:

> Follow AGENTS.md. Set me up with my resume at <path to your PDF>.

Codex shows every value it read off your resume for you to correct, asks **one numbered list** of
questions, drafts `config/answers.md` from your real work, and asks you to check the exact numbers
and titles it used. It writes your three config files. It does not open the browser or apply to
anything during setup.

**5. The supervised application (10 min).** Codex finds one real posting, runs the duplicate checks,
fills the form in the browser window, and writes everything down. Then it stops and shows you:
the URL, every question and answer, the files it uploaded, and a screenshot.

**6. Checkpoint.** Review the form in the browser. When it all looks right, **click Submit
yourself** and tell Codex you did. It records the confirmation. If anything is wrong, say so and it
corrects it, or tell it not to send and it sends nothing. Prefer Codex to click? Say "yes, submit"
in chat. A human click is the default because it also avoids bot-detection problems on some forms.

**Just practicing?** Tell Codex you only want a practice run. It does everything except submit and
logs it as a dry run.

## Limits to know about
- **No scheduled runs.** Each application is a request you make in this chat.
- **Bot detection.** Playwright is an automated browser, so some forms may flag it. When one does,
  Codex stops and marks it for you instead of retrying.
- **Some forms are out.** Anything needing an account, a login code, an interactive CAPTCHA, or an
  emailed verification code after Submit is handed back to you.
- **No tailored resume PDF.** It uploads your own resume and writes a text cover letter.
- **Untested combination.** This branch adapts a playbook written for Claude Code to Codex.
  Run a practice application before the meeting.
- **Privacy.** Your config and logs stay on your machine and are gitignored. Do not commit them to
  a public repo.
- **Real applications.** Only apply to roles you want.
