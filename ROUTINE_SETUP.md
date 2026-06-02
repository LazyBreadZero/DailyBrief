# Routine Setup — ONE routine, BOTH briefings

A single **Claude Code Routine** produces *both* daily briefings in one run and sends *two* emails:
- **Frontier Intelligence** (Angelo) — files at the repo root → emails `angelo.gunther@gmail.com`
- **Appetite** (Julinka) — files in `julinka/` → emails `julinkacannes@gmail.com`

Their content, memory, and outputs stay completely separate (root vs `julinka/` folders). See `HOW_IT_WORKS.md` for the architecture.

---

## One-time setup
1. **GitHub Pages** — ✅ enabled (Source: `main` / `(root)`). The emails link to `https://lazybreadzero.github.io/DailyBrief/...`.
2. **Gmail connector** — must have **send** scope (not just draft). Only Gmail is required; other connectors (Canva, Calendar, Drive, Notion) are unused and can be removed.
3. **Repo** — the routine must be connected to `LazyBreadZero/DailyBrief` (branch `main`).

---

## Configure the routine
Claude Code → **Routines** → open *Frontier Intelligence Daily Briefing* → ✏️ **Edit**.
- **Name:** `Daily Briefings — Frontier Intelligence + Appetite`
- **Repository:** `LazyBreadZero/DailyBrief` (branch `main`)
- **Connectors:** Gmail (send)
- **Schedule:** Daily at 08:00, Europe/Vienna
- **Network:** Full
- **Instructions:** replace everything with the block below, then **Save**.

### Instructions (paste verbatim)
```
You produce TWO separate daily briefings in ONE run, each with its own data and its own email. Keep them fully separate — never mix their content or memory. Work from LazyBreadZero/DailyBrief, branch main. Use today's real date for everything.

═══ BRIEF 1 — FRONTIER INTELLIGENCE (Angelo) · files at repo ROOT ═══
1. Read briefing_goal.md (the mission) and briefing_system_prompt.md (house style + rules).
2. Read briefing_archive.md fully — your memory of every prior edition. Build continuity; never repeat a covered story.
3. Run 5–8 web searches ONLY on the beats in briefing_system_prompt.md (NeuroTech, XR, AR/VR, BCI, spatial computing). Do NOT drift into general AI-industry news. Follow-up threads from the archive first, then fresh news.
4. Write the full self-contained HTML briefing per briefing_system_prompt.md and save it as briefings/YYYY-MM-DD.html.
5. Append today's edition block to briefing_archive.md before the summary table, update the table, and commit.
6. EMAIL (do exactly; never improvise):
   - Read email_template.html and copy it VERBATIM.
   - Replace ONLY the {{TOKENS}}: {{DATE_ISO}}, {{DATE_LONG}}, {{EDITION}}, {{CATEGORIES}}, {{LEAD_KICKER}}, {{HEADLINE}}, {{DECK}}, {{BULLET_1}}..{{BULLET_4}} (each "<b>Topic</b> — one line"), {{DEEP_READ}} (or delete that <tr> if none).
   - Button link MUST be exactly https://lazybreadzero.github.io/DailyBrief/briefings/{{DATE_ISO}}.html
   - Send the FILLED TEMPLATE as the Gmail HTML body to angelo.gunther@gmail.com, subject "Frontier Intelligence — {{DATE_LONG}}".
   - NEVER paste the full briefing into the email. NEVER attach it. Preview + button only.

═══ BRIEF 2 — APPETITE (Julinka) · files in julinka/ ═══
7. Read julinka/briefing_goal.md and julinka/briefing_system_prompt.md.
8. Read julinka/briefing_archive.md fully. Build continuity; never repeat a covered story.
9. Run 5–8 web searches across the four pillars (Venture Capital, Food, Art, Nature). Follow-up threads first, then fresh news.
10. Write the full self-contained HTML briefing per julinka/briefing_system_prompt.md and save it as julinka/briefings/YYYY-MM-DD.html.
11. Append today's edition block to julinka/briefing_archive.md before the summary table, update the table, and commit.
12. EMAIL (do exactly; never improvise):
   - Read julinka/email_template.html and copy it VERBATIM.
   - Replace ONLY the {{TOKENS}}: {{DATE_ISO}}, {{DATE_LONG}}, {{EDITION}}, {{LEAD_KICKER}}, {{HEADLINE}}, {{DECK}}, {{BULLET_1}}..{{BULLET_4}} (each "<b>Pillar</b> — one line"), {{DEEP_READ}} (or delete that <tr> if none).
   - Button link MUST be exactly https://lazybreadzero.github.io/DailyBrief/julinka/briefings/{{DATE_ISO}}.html
   - Send the FILLED TEMPLATE as the Gmail HTML body to julinkacannes@gmail.com, subject "Appetite — {{DATE_LONG}}".
   - NEVER paste the full briefing into the email. NEVER attach it. Preview + button only.

Do BRIEF 1 completely, then BRIEF 2 completely. End state: two new HTML files committed (one at root briefings/, one in julinka/briefings/), both archives updated, and two preview emails sent.
```

---

## After saving
1. Hit **Run now** once. Confirm: a new `briefings/YYYY-MM-DD.html` **and** a new `julinka/briefings/YYYY-MM-DD.html` are committed, both archives updated, and **two** emails arrive — each a short preview with a working "Read the full…" button (not the full HTML).
2. Click both buttons to confirm the Pages links resolve.
3. Leave it on the daily 08:00 Europe/Vienna schedule.
