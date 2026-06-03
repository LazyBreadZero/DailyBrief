# Routine Setup — ONE routine, BOTH briefings (bulletproof persistence)

A single **Claude Code Routine** produces *both* daily briefings each morning and sends *two* emails:
- **Frontier Intelligence** (Angelo) — files at repo root → `angelo.gunther@gmail.com`
- **Appetite** (Julinka) — files in `julinka/` → `julinkacannes@gmail.com`

> **Why the old run failed (and this fixes it):** in a scheduled routine, `git push` does **not** work (the sandbox has no SSH/token; GitHub auth goes through a scoped proxy), and `WebFetch`/raw URLs **paraphrase** file contents instead of returning them exactly. The reliable path is the **GitHub MCP tools** — `get_file_contents` to read, `push_files` to commit — and the routine must be **allowed to push to `main`**.

---

## ⚠️ Prerequisites — set these on the routine (most are one-time)
1. **Allow unrestricted branch pushes → ON.** By default a routine may only push to `claude/*` branches; this brief writes to `main`, so this toggle is **required** (Routine settings, when creating/editing).
2. **Connectors:** **GitHub** (so the `mcp__github__*` tools are available) **and Gmail (send)**. You can remove Calendar/Drive/Canva/Notion — they're unused.
3. **GitHub Pages:** ✅ already enabled (Source `main` / root). Links are `https://lazybreadzero.github.io/DailyBrief/...`.
4. **Repository:** `LazyBreadZero/DailyBrief`, branch `main`.
5. **Schedule:** Daily 08:00, Europe/Vienna. **Network:** Full.

---

## Instructions (paste verbatim into the routine's Instructions box)
```
You produce TWO separate daily briefings in ONE run, each with its own data and its own email. Keep them fully separate. Use today's real date everywhere. Repo: LazyBreadZero/DailyBrief, branch main.

PERSISTENCE RULES (critical — the sandbox cannot git push):
- READ every repo file with the GitHub tool get_file_contents (owner LazyBreadZero, repo DailyBrief, ref main). NEVER read repo files via WebFetch or raw URLs — they paraphrase and corrupt the content.
- WRITE/commit every repo file with the GitHub tool push_files (branch main, multiple files in one commit). NEVER use git, gh, ssh, or Composio for git — they have no push credential here and will fail.
- If get_file_contents / push_files aren't loaded, find them first via ToolSearch ("github get_file_contents", "github push_files").

═══ BRIEF 1 — FRONTIER INTELLIGENCE (Angelo) · files at repo ROOT ═══
1. get_file_contents for: briefing_goal.md, briefing_system_prompt.md, briefing_archive.md, email_template.html.
2. Use briefing_archive.md as memory — build continuity, never repeat a covered story.
3. Run 5–8 web searches ONLY on the beats in briefing_system_prompt.md (NeuroTech, XR, AR/VR, BCI, spatial computing). Do NOT drift into general AI-industry news.
4. Compose the full self-contained HTML briefing per briefing_system_prompt.md.
5. Compose the updated briefing_archive.md (append today's edition block before the summary table; update the table).
6. COMMIT with ONE push_files call to branch main, message "Frontier Intelligence — <DATE_LONG>", files:
     [ {path:"briefings/<DATE_ISO>.html", content: <the full HTML>},
       {path:"briefing_archive.md", content: <the full updated archive>} ]
7. EMAIL: take email_template.html, replace ONLY the {{TOKENS}} ({{DATE_ISO}},{{DATE_LONG}},{{EDITION}},{{CATEGORIES}},{{LEAD_KICKER}},{{HEADLINE}},{{DECK}},{{BULLET_1..4}} as "<b>Topic</b> — one line",{{DEEP_READ}} or delete that <tr>). Button link MUST be https://lazybreadzero.github.io/DailyBrief/briefings/<DATE_ISO>.html . Send the filled template as the Gmail HTML body to angelo.gunther@gmail.com, subject "Frontier Intelligence — <DATE_LONG>". NEVER paste the full briefing or attach it — preview + button only.

═══ BRIEF 2 — APPETITE (Julinka) · files in julinka/ ═══
8. get_file_contents for: julinka/briefing_goal.md, julinka/briefing_system_prompt.md, julinka/briefing_archive.md, julinka/email_template.html.
9. Memory + continuity as above.
10. Run 5–8 web searches across the four pillars (Venture Capital, Food, Art, Nature).
11. Compose the full HTML briefing per julinka/briefing_system_prompt.md.
12. Compose the updated julinka/briefing_archive.md.
13. COMMIT with ONE push_files call to branch main, message "Appetite — <DATE_LONG>", files:
     [ {path:"julinka/briefings/<DATE_ISO>.html", content: <the full HTML>},
       {path:"julinka/briefing_archive.md", content: <the full updated archive>} ]
14. EMAIL: fill julinka/email_template.html (tokens {{DATE_ISO}},{{DATE_LONG}},{{EDITION}},{{LEAD_KICKER}},{{HEADLINE}},{{DECK}},{{BULLET_1..4}} as "<b>Pillar</b> — one line",{{DEEP_READ}}). Button link MUST be https://lazybreadzero.github.io/DailyBrief/julinka/briefings/<DATE_ISO>.html . Send to julinkacannes@gmail.com, subject "Appetite — <DATE_LONG>". Preview + button only.

Do BRIEF 1 completely, then BRIEF 2. End state: two push_files commits on main (a new HTML + updated archive each) and two preview emails sent.
```

---

## After saving — verify once with **Run now**
You should see, on `main`: a new `briefings/YYYY-MM-DD.html` **and** `julinka/briefings/YYYY-MM-DD.html`, both archives updated (via `push_files` commits, **not** git), and **two** preview emails with working buttons. If a commit step is skipped, re-check **"Allow unrestricted branch pushes"** and that **GitHub** is in the connectors list.
