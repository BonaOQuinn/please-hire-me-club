# please-hire-me: Track 2, Free Claude

For people with a **free claude.ai account** and nothing else. No Claude Code, no browser
extension, no installs. Claude is the brain in a chat, and **you are the hands**: you paste in the
posting and the form, Claude writes the answers, and you copy them into the real form and click
Submit yourself. That makes the review checkpoint automatic: nothing is sent unless you send it.

Based on [alecswang/please-hire-me](https://github.com/alecswang/please-hire-me) (MIT). The other
tracks are on the [`main`](../../tree/main) (paid Claude Code) and
[`free-codex`](../../tree/free-codex) branches.

## What you need
- A free account at [claude.ai](https://claude.ai)
- Your resume (PDF or text)
- A real job you want to apply to, on a company's own Greenhouse / Lever / Ashby / Workable form

## What is in this branch

| File | What it is |
|---|---|
| `CHAT.md` | The playbook. Claude follows it for the whole track. |
| `config/profile.example.json` | Checklist of every fact a form asks for. |
| `config/answers.example.md` | Template for your free-text answers and fact sheet. |
| `config/settings.example.json` | What counts as a good job for you. |
| `data/boards.md` | Company boards that were live when last checked. A place to find postings. |

## The track

**1. Start a chat (2 min).** Open claude.ai and make a new chat. If your plan has Projects, create
one and add the five files above to its knowledge, so you can reload them next session. Otherwise
attach them to the chat. Free plans have message limits, so keep the files attached rather than
re-pasting them.

**2. Set up (10 min).** Send this, with your resume attached:

> Follow CHAT.md. Here is my resume. Set me up, then walk me through one application.

Claude shows every value it read off your resume for you to correct, then asks **one numbered
list** of questions, drafts your answer templates from your real work, and asks you to verify the
exact numbers and titles it used. At the end it prints three files: `profile.json`, `answers.md`,
`settings.json`. Save them somewhere private, and add them to the Project knowledge. They contain
personal data, so do not post them or commit them to a public repo.

**3. Pick a posting (5 min).** Find one live opening, from `boards.md` or a company's careers page.
Paste the URL and the posting text. Claude says **APPLY** or **SKIP** and why.

**4. Get the answer sheet (5 min).** Open the application form, select all, copy, and paste it
into the chat. Claude returns a table of every field, the answer to type, where the answer came
from, and a status of `READY`, `CHECK` or `NEEDS HUMAN`. It drafts a cover letter if the form has a
place for one.

**5. Checkpoint.** Paste each answer into the form. Compare every field to the table, especially the
`CHECK` and `NEEDS HUMAN` rows and every number. Only when everything matches, click Submit.

**6. Log it.** Tell Claude "submitted" and it writes a log entry. Save that in a file called
`applications-log.md` and paste it into later chats so Claude can catch duplicate applications.

## Limits to know about
- **You do the typing.** There is no agent clicking for you. That is the cost of a free account.
- **No automatic job search or scheduling.** You find the posting.
- **No tailored resume PDF.** Claude can suggest which bullets to lead with, but you edit your own
  resume.
- **Claude can be wrong.** It is told never to invent facts, but you are the final check. That is
  what step 5 is for.
- **Privacy.** You are pasting your resume into a chat. Remove anything you would not want there.
- **Sign-ins, 2FA and CAPTCHAs are yours.** Never paste a password or a login code into the chat.
- **Real applications.** Only apply to roles you want.

## Want more automation?
Pair up with a club member on the Claude Code track or the Codex track for step 4 and 5, or move
to the [`free-codex`](../../tree/free-codex) branch if you can install the Codex CLI.
