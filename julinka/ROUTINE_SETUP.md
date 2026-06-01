# Appetite (Julinka's Brief) — Routine Setup

The daily briefing is produced by a **Claude Code Routine** (a scheduled automation). Routines run in Anthropic's cloud on a schedule — no machine needs to be on. A routine **cannot be created by a tool/agent**; you create it once yourself in the Claude Code web or desktop app. It takes about a minute.

> **Note:** This system lives entirely in the `julinka/` folder of the `LazyBreadZero/DailyBrief` repository and is independent of the original *Frontier Intelligence* briefing. Once this folder is on the default branch (`main`), the routine can read it directly and the published pages go live.

---

## Create the routine

**Where:** Claude Code on the web (https://claude.com/code) or the desktop app → **Automations / Routines** → **New routine**.

Use these exact settings:

### Name
```
Appetite — Julinka's Daily Briefing
```

### Repository
```
LazyBreadZero/DailyBrief   (branch: main)
```

### Connectors
```
Gmail (with send permission — see note below)
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
Read julinka/briefing_system_prompt.md from the repository for full instructions. Then:

1. Read julinka/briefing_archive.md fully from the repository
2. Run 5–8 web searches (follow-up threads from the archive first, then fresh news across Venture Capital, Food, Art and Nature)
3. Write the full "Appetite" HTML briefing following all instructions in julinka/briefing_system_prompt.md
4. Save the HTML as julinka/briefings/YYYY-MM-DD.html in the repository (use today's actual date)
5. Update julinka/briefing_archive.md by appending today's edition block before the summary table, then update the table. Commit both files.
6. Send an email via Gmail to julinkacannes@gmail.com with subject "Appetite — [today's date]". The body should be a short HTML email (NOT the full briefing) containing: the lead headline, a 3–4 bullet summary of the edition's top stories, and a single prominent link to read the full briefing at https://lazybreadzero.github.io/DailyBrief/julinka/briefings/YYYY-MM-DD.html (substitute today's actual date). Do NOT paste the full briefing HTML into the email body.
```

---

## Gmail send permission

When you add the **Gmail connector** to the routine, grant it **send** scope (not just read/compose-draft) during the Google OAuth consent screen. If the connector only has draft scope, the routine will create a Gmail draft each morning instead of sending — still useful, but someone has to press send.

---

## Publishing (GitHub Pages)

The email links to `https://lazybreadzero.github.io/DailyBrief/julinka/briefings/YYYY-MM-DD.html`. For that link to resolve, GitHub Pages must be enabled for the repository and the `julinka/` folder present on the published branch (`main`). The HTML files are fully self-contained and render the same standalone or via Pages.

---

## After creating it

1. **Run it once manually** (the "Run now" / "Test run" button) to confirm the email arrives and a `julinka/briefings/YYYY-MM-DD.html` file plus an updated `julinka/briefing_archive.md` get committed.
2. The seed memory is **Edition 1 (1 June 2026)**, so the first real run will produce **Edition 2** and build on Edition 1's open follow-up threads (Calm/Storm's next cheque and nutrition-tech mandate, Art Basel read-out, Gourmey's EFSA progress, EU nature-credit methodology, etc.).
3. Leave it on the daily 08:00 Europe/Vienna schedule and it will self-extend the archive each morning.
