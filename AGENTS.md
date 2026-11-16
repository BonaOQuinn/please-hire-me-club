# please-hire-me: entry point for Codex

You are Codex running in the user's terminal inside this repo. The playbook is `CLAUDE.md`. Read it
in full and follow it, in its reading order. Every **rule** in it applies to you: never invent a
fact, never create an account or type a password, the duplicate, lifetime-cap and interview-tracker
skips, the target quality gate, log before submit, and one screenshot per submit. `config/spec.md`
and `config/documents.md` apply unless this file says otherwise.

`CLAUDE.md` was written for Claude Code driving the user's own Chrome through the Claude in Chrome
extension, on a schedule. You have none of that. This file maps each **mechanism**. Where this file
and `CLAUDE.md` disagree on a mechanism, this file wins. Where they disagree on a **rule**,
`CLAUDE.md` wins.

## Mechanism map

| `CLAUDE.md` says | Do this instead |
|---|---|
| `mcp__claude-in-chrome__*` tools, `computer`, `find`, `file_upload` | The **Playwright MCP** tools (`browser_navigate`, `browser_snapshot`, `browser_click`, `browser_type`, `browser_select_option`, `browser_file_upload`, `browser_take_screenshot`). Run it headed, never headless. |
| `list_connected_browsers` preflight | Check that Playwright MCP tools are available (`codex mcp list`). If not, stop and tell the user to run the command in `README.md` step 3. |
| `tabs_context_mcp` / `tabs_close_mcp`, tab-group hygiene | Use one tab. At the end call `browser_close`. Never touch tabs you did not open. |
| `scripts/schedule.sh`, `run.sh`, `./setup.sh`, scheduled runs | **Do not exist in this branch.** Never offer a schedule. Every run is a manual one in this chat. |
| `scripts/code_broker.py`, Gmail app password, Keychain | **Not available.** A form that emails a verification code after Submit is `NEEDS HUMAN`: leave the tab open for the user. |
| `.claude/hooks` (secret-read and "AI leak" hooks) | Not present. Enforce them yourself: never read the user's password stores or clipboard, and never type a phrase like "written with AI", "Here's a", a word count or markdown into a form field. Run `python3 scripts/app_docs.py check-text` on the field dump before the checkpoint. |
| `tectonic` / `pdftotext` and resume tailoring | **Off.** Write `documents.tailor_resume: false`. Upload the user's own `data/resume.pdf`. Cover letters stay on, as text. |
| `signed_in_portals`, Workday, Google Careers recipes | Out of scope. Skip those portals. |
| "Trusted input, never JavaScript fill" | Fill with Playwright's real click and type actions. Never set values with page JavaScript, and never fake mouse jitter or timing to beat a detector. |
| `/Users/...` paths, `brew install` | Repo-relative paths. Windows users run this in WSL or Git Bash with `python3` on PATH. |

## First run: setup in this chat
Same as `CLAUDE.md` "FIRST RUN", steps 1 to 5, with these changes:
- Skip step 5b (resume to LaTeX) and step 6 (schedule) and step 6b (add-ons). Do not ask about
  LaTeX, tectonic, Gmail, or an interview tracker.
- In `config/settings.json` write the club defaults: `run.max_applications_per_run` = 1,
  `schedule.frequency` = `"manual"`, `documents.tailor_resume` = `false`,
  `broker` left empty, `run.interview_tracker_path` empty.
- Keep the rest: show every extracted value, ask the one numbered question list, draft
  `config/answers.md`, and check every figure and title against the resume before the user confirms.
- Do not open the browser until setup is done.

## The supervised first application (mandatory, step 7)
Source one real posting (`python3 scripts/delta_sweep.py` and `python3 scripts/list_sweep.py` in the
foreground, or ask the user which company they want). Run the duplicate checks and the quality gate,
fill every field, verify 0 invalid required fields, write the per-application doc and the log line,
take the screenshot. Then **stop with the filled form open and show the user everything**: URL,
every question and answer, uploaded files, the screenshot.

**Default submit mode: the user clicks Submit.** Tell them "The form is filled in the browser
window. Review it, then click Submit yourself, and tell me when you have." This is the checkpoint,
and it also means the final click is a genuine human one. Do not click Submit in this mode.

**Alternative: the user says "yes, submit" in chat.** Only if they say so in those words (silence,
"maybe" or anything else means no). Then click Submit with Playwright. If the page shows a spam or
bot warning, stop and mark it `NEEDS HUMAN`; do not retry or work around it.

After the user confirms a submit, take the confirmation screenshot into `screenshots/`, mark the
log and the per-application doc `SUBMITTED` with the date, and call `browser_close`.

**Practice mode.** If the user says they only want to practice, set `run.dry_run` to `true` for that
session: do everything up to Submit, never click it, log it as DRY RUN, and name the doc
`applications/<company>-<role>.DRYRUN.md`. Remove the flag again afterwards.

## After the first one
Every later run is an interactive request in this same chat ("apply to one more job"), and it uses
the same checkpoint. Never apply to more than `run.max_applications_per_run`.

## Sign-ins, accounts, CAPTCHAs
Always the user's. If a page asks for a login, a password, a login code, or an interactive CAPTCHA,
stop, log `NEEDS HUMAN` with the URL, and leave the tab for them.

## Privacy
`config/profile.json`, `config/answers.md`, `config/settings.json`, `applications/`, `logs/`,
`screenshots/` and `state/` are gitignored. Never commit them, never paste them anywhere outside
this repo and the application form.
