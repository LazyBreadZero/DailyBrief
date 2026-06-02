# Appetite (Julinka's Brief) — Routine Setup

The daily briefing is produced by a **Claude Code Routine** (a scheduled automation) running in Anthropic's cloud. You create it once in the Claude Code web or desktop app. This system lives entirely in the `julinka/` folder of `LazyBreadZero/DailyBrief` and is independent of the original *Frontier Intelligence* briefing.

---

## ⚠️ One-time setup: enable GitHub Pages (so the email link works)

The email links to `https://lazybreadzero.github.io/DailyBrief/julinka/briefings/<date>.html`. That URL only resolves once **GitHub Pages is enabled**:

**GitHub → repo Settings → Pages → Source: "Deploy from a branch" → Branch: `main` / `/(root)` → Save.** (The repo is public.) Verify after ~1 min by opening `https://lazybreadzero.github.io/DailyBrief/julinka/briefings/2026-06-01.html`.

**Zero-setup fallback** (works right now, no Pages needed):
`https://htmlpreview.github.io/?https://raw.githubusercontent.com/LazyBreadZero/DailyBrief/main/julinka/briefings/<date>.html`

---

## Create the routine

**Where:** Claude Code on the web (https://claude.com/code) or the desktop app → **Automations / Routines** → **New routine**.

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
You generate today's "Appetite" briefing for Julinka. Work from the repository LazyBreadZero/DailyBrief on branch main, inside the julinka/ folder.

1. Read julinka/briefing_system_prompt.md fully — your house style and instructions.
2. Read julinka/briefing_archive.md fully — the memory of all prior editions. Build continuity; do not repeat covered stories.
3. Run 5–8 web searches across the four pillars (Venture Capital, Food, Art, Nature) — follow-up threads from the archive first, then fresh news. Use today's real date.
4. Write the full self-contained HTML briefing per julinka/briefing_system_prompt.md and save it as julinka/briefings/YYYY-MM-DD.html (today's actual date).
5. Append today's edition block to julinka/briefing_archive.md before the summary table, update the table, and commit both files.

6. SEND THE EMAIL — follow this exactly; do NOT improvise the email:
   a. Read julinka/email_template.html from the repo and copy it VERBATIM.
   b. Replace ONLY the {{TOKENS}}: {{DATE_ISO}} (e.g. 2026-06-03), {{DATE_LONG}} (e.g. Tuesday, 3 June 2026), {{EDITION}}, {{LEAD_KICKER}}, {{HEADLINE}}, {{DECK}}, {{BULLET_1}}..{{BULLET_4}} (form: <b>Pillar</b> — one line), {{DEEP_READ}} (or delete that <tr> if none).
   c. The button link must be exactly https://lazybreadzero.github.io/DailyBrief/julinka/briefings/{{DATE_ISO}}.html
   d. Send the FILLED TEMPLATE as the HTML body via Gmail to julinkacannes@gmail.com, subject "Appetite — {{DATE_LONG}}".
   e. NEVER paste the full briefing into the email. NEVER attach it. NEVER redesign the template. The email is only the preview + the link.
```

---

## Gmail send permission

When adding the **Gmail connector**, grant **send** scope during OAuth. If it only has draft scope, the routine will create a draft each morning instead of sending.

---

## After creating it

1. **Run it once manually** ("Run now") and confirm: a new `julinka/briefings/YYYY-MM-DD.html` is committed, the archive is updated, and the email that arrives is the **short template preview with a working "Read the full brief" button** (not the full HTML).
2. Seed memory is **Edition 1 (1 June 2026)**, so the first run produces **Edition 2** and builds on Edition 1's open threads.
3. Leave it on the daily 08:00 Europe/Vienna schedule.
