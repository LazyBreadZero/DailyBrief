# Frontier Intelligence — Routine Setup

The daily briefing is produced by a **Claude Code Routine** (a scheduled automation). Routines run in Anthropic's cloud on a schedule — no machine of yours needs to be on. You create it once in the Claude Code web or desktop app.

> **All files live on `main`**, so the routine reads them directly.

---

## ⚠️ One-time setup: enable GitHub Pages (so the email link works)

The email links to the full briefing at `https://lazybreadzero.github.io/DailyBrief/briefings/<date>.html`. That URL only resolves once **GitHub Pages is enabled**:

**GitHub → repo Settings → Pages → Build and deployment → Source: "Deploy from a branch" → Branch: `main` / `/(root)` → Save.**

The repo must also be **public** (it is). Give it ~1 minute to build. To verify, open `https://lazybreadzero.github.io/DailyBrief/briefings/2026-06-02.html`.

**Don't want to enable Pages?** The template's button also works with this zero-setup fallback URL (renders the same file straight from the public repo):
`https://htmlpreview.github.io/?https://raw.githubusercontent.com/LazyBreadZero/DailyBrief/main/briefings/<date>.html`

---

## Create the routine

**Where:** Claude Code on the web (https://claude.com/code) or the desktop app → **Automations / Routines** → **New routine**.

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
Gmail (with SEND permission)
```

### Schedule
```
Daily at 08:00, timezone Europe/Vienna
```

### Network access
```
Full (required for web searches)
```

### Prompt  (paste this exactly — it is deliberately strict about the email)
```
You generate today's "Frontier Intelligence" briefing. Work from the repository LazyBreadZero/DailyBrief on branch main.

1. Read briefing_system_prompt.md fully — it is your house style and instructions.
2. Read briefing_archive.md fully — the memory of all prior editions. Build continuity; do not repeat covered stories.
3. Run 5–8 web searches (follow-up threads from the archive first, then fresh news in NeuroTech / XR / BCI / spatial computing). Use today's real date.
4. Write the full self-contained HTML briefing per briefing_system_prompt.md and save it as briefings/YYYY-MM-DD.html (today's actual date).
5. Append today's edition block to briefing_archive.md before the summary table, update the table, and commit both files.

6. SEND THE EMAIL — follow this exactly; do NOT improvise the email:
   a. Read email_template.html from the repo and copy it VERBATIM.
   b. Replace ONLY the {{TOKENS}}: {{DATE_ISO}} (e.g. 2026-06-03), {{DATE_LONG}} (e.g. Tuesday, 3 June 2026), {{EDITION}}, {{CATEGORIES}}, {{LEAD_KICKER}}, {{HEADLINE}}, {{DECK}}, {{BULLET_1}}..{{BULLET_4}} (form: <b>Topic</b> — one line), {{DEEP_READ}} (or delete that <tr> if none).
   c. The button link must be exactly https://lazybreadzero.github.io/DailyBrief/briefings/{{DATE_ISO}}.html
   d. Send the FILLED TEMPLATE as the HTML body via Gmail to angelo.gunther@gmail.com, subject "Frontier Intelligence — {{DATE_LONG}}".
   e. NEVER paste the full briefing into the email. NEVER attach it. NEVER redesign the template. The email is only the preview + the link.
```

---

## Gmail send permission

When adding the **Gmail connector**, grant **send** scope during OAuth. If it only has draft scope, the routine will create a draft each morning instead of sending.

---

## After creating it

1. **Run it once manually** ("Run now") and confirm: a new `briefings/YYYY-MM-DD.html` is committed, the archive is updated, and the email that arrives is the **short template preview with a working "Read the full briefing" button** (not the full HTML).
2. Click the button in the email to confirm the link resolves (enable Pages first, or use the htmlpreview fallback).
3. Leave it on the daily 08:00 Europe/Vienna schedule.
