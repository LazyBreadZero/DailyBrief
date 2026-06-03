# How This Repo Works (read me first)

This repository is the **brain** for two daily email briefings. It is the single source of truth: instructions, memory, layout, and output all live here. Nothing else carries state.

## The three "Claudes" (and why the repo is essential)
- **claude.ai chat** and a **Claude Code session** are *ephemeral* — they forget everything when closed and do **not** share memory with each other or with the routine.
- A **Claude Code Routine** is a Claude Code session that runs on a schedule. **Every run starts in a brand-new, empty cloud container** with zero memory of previous runs.
- Therefore the only thing that persists between mornings is **what gets committed to this repo.** The repo *is* the memory.

```
  Routine (08:00 daily, fresh empty container)
        │ reads instructions box → reads THIS repo → web-searches
        │ writes briefs → commits → emails via Gmail
        ▼
  GitHub repo (this) ──► GitHub Pages (public URLs the emails link to)
```

## Two briefs, one routine, separate data
A single routine produces **both** briefings each morning and sends **two** emails. Their data is kept completely separate by folder:

| | Frontier Intelligence (Angelo) | Appetite (Julinka) |
|---|---|---|
| Mission / goal | `briefing_goal.md` | `julinka/briefing_goal.md` |
| House style + rules | `briefing_system_prompt.md` | `julinka/briefing_system_prompt.md` |
| Memory (auto-grows) | `briefing_archive.md` | `julinka/briefing_archive.md` |
| Email layout | `email_template.html` | `julinka/email_template.html` |
| Outputs | `briefings/YYYY-MM-DD.html` | `julinka/briefings/YYYY-MM-DD.html` |
| Recipient | angelo.gunther@gmail.com | julinkacannes@gmail.com |
| Public URL | `…github.io/DailyBrief/briefings/<date>.html` | `…github.io/DailyBrief/julinka/briefings/<date>.html` |

The routine config itself (schedule, the instructions prompt, Gmail connector) lives in **Claude Code → Routines**, *not* in this repo. The instructions there are the copy in **`ROUTINE_SETUP.md`**.

## If you ever want to change something
- **Topics / writing style / what a great edition is** → edit the `*_goal.md` and `*_system_prompt.md` files.
- **What the email looks like** → edit the `*_email_template.html` files.
- **Schedule / recipient / the daily instructions** → edit the Routine in Claude Code (see `ROUTINE_SETUP.md`).
- **The running memory** → leave it; the routine appends to the archive files automatically.

You can ask any Claude Code session to make repo edits for you. You cannot change the brief by talking to a normal claude.ai chat — it isn't connected to any of this.

## How the routine saves its work (the one setting that matters)
A scheduled routine gets the repo checked out with an **authenticated remote**, and pushes with **plain git** — the platform proxy signs the push (no SSH key or token needed). Two rules:
- **Read** files from the local working copy (exact). Don't use `WebFetch`/raw URLs — they *paraphrase* files.
- **Commit** with `git add -A && git commit && git push origin main`.

The push to `main` only works if **one setting** is enabled on the routine:
- **"Allow unrestricted branch pushes"** for this repo. Without it, a routine may only push to `claude/*` branches — never `main` — and the run fails at push with "No SSH available."

Note: GitHub *push* access comes from selecting the **repository** on the routine + that checkbox — **not** from any "connector." The "GitHub Integration" connector in claude.ai is a read-only API tool and is irrelevant here.

(`.nojekyll` at the repo root tells GitHub Pages to serve the HTML as-is.)
