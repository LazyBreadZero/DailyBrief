# Frontier Intelligence — Routine Setup

The daily briefing is produced by a **Claude Code Routine** (a scheduled automation). Routines run in Anthropic's cloud on a schedule — no machine of yours needs to be on. A routine **cannot be created by a tool/agent**; you create it once yourself in the Claude Code web or desktop app. It takes about a minute.

> **Important — branch note:** All files for this system were committed to the branch
> `claude/frontier-intelligence-setup-q6iqK`. Routines read a repository's **default branch (`main`)**.
> **Merge this branch into `main` before (or right after) creating the routine**, otherwise the
> routine won't see `briefing_system_prompt.md` / `briefing_archive.md`.

---

## Create the routine

**Where:** Claude Code on the web (https://claude.com/code) or the desktop app → **Automations / Routines** → **New routine** (also called a scheduled task).

Use these exact settings:

### Name
```
Frontier Intelligence Daily Briefing
```

### Repository
```
LazyBreadZero/DailyBrief   (branch: main)
```

### Connectors
```
Gmail
```

### Schedule
```
Daily at 08:00, timezone Europe/Vienna
```

### Network access
```
Full (required for web searches)
```

### Prompt
```
Read briefing_system_prompt.md from the repository for full instructions. Then:

1. Read briefing_archive.md fully from the repository
2. Run 5–8 web searches (follow-up threads from archive first, then fresh news)
3. Write the full Frontier Intelligence HTML briefing following all instructions in briefing_system_prompt.md
4. Save the HTML as briefings/YYYY-MM-DD.html in the repository (use today's actual date)
5. Update briefing_archive.md by appending today's edition block before the summary table, then update the table. Commit both files.
6. Send an email via Gmail to angelo.gunther@gmail.com with subject "Frontier Intelligence — [today's date]" and the full HTML as the email body
```

---

## After creating it

1. **Run it once manually** (the "Run now" / "Test run" button) to confirm the email arrives and a `briefings/YYYY-MM-DD.html` file plus an updated `briefing_archive.md` get committed.
2. The seed memory is **Edition 1 (2 June 2026)**, so the first real run will produce **Edition 2** and build on Edition 1's open follow-up threads (Science Corp CE mark, Samsung Galaxy XR ship date, Meta case management conference, etc.).
3. Leave it on the daily 08:00 Europe/Vienna schedule and it will self-extend the archive each morning.
