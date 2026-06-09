# Routine Setup — ONE routine, BOTH briefings

A single **Claude Code Routine** produces *both* briefings each morning and sends *two* emails:
- **Frontier Intelligence** (Angelo) — files at repo root → `angelo.gunther@gmail.com`
- **Appetite** (Julinka) — files in `julinka/` → `julinkacannes@gmail.com`

---

## ⚠️ Read this first: how a routine writes to GitHub (the thing that was broken)

A routine does **not** push via SSH, via an MCP "GitHub connector", or via Composio. It pushes with **plain `git`**, and the platform's **auth proxy** signs the push for you. There is exactly **one gate**:

> **"Allow unrestricted branch pushes"** must be enabled for this repo on the routine. By default a routine may only push to `claude/*` branches — never `main`. With this off, the daily push to `main` fails (the run reports "No SSH available" and gives up).

**The "GitHub Integration" connector at claude.ai/customize/connectors is unrelated** — it's a read-only GitHub *API* tool for chats. It does not grant push access and you do **not** need it here (which is why it doesn't appear in the routine's connector list).

So the routine needs, in its settings:
1. The repo **`LazyBreadZero/DailyBrief`** selected as a **Repository** (this is what provides authenticated clone + push — separate from "Connectors").
2. **"Allow unrestricted branch pushes" = ON** for it.
3. **Gmail** connector with **send** scope (for the emails).
4. Pages: ✅ already enabled.

---

## Instructions (paste verbatim into the routine's Instructions box)
```
You produce TWO separate daily briefings in ONE run, each with its own data and its own email. Keep them fully separate. Use today's real date everywhere. Repo: LazyBreadZero/DailyBrief.

PERSISTENCE — read from the clone, commit with plain git (NOT WebFetch, NOT SSH, NOT MCP/Composio):
- The repo is checked out for you with an authenticated remote. Read every file from that local working copy — it is exact. NEVER read repo files via WebFetch or raw URLs; they paraphrase and corrupt the content.
- This run starts on an auto-created claude/* working branch, NOT on main. After writing/editing files, push the new commit straight to the default branch with an explicit refspec, so it is not stranded on the claude/* branch:
    git add -A && git commit -m "<message>" && git push origin HEAD:main
- Use HEAD:main, never the bare "git push origin main": the bare form pushes your unchanged local main ref and strands the new commit on the claude/* branch (exactly what caused the Pages 404). The platform proxy signs the push automatically. (Requires "Allow unrestricted branch pushes" enabled for this repo in the routine settings — otherwise the push to main is rejected.)
- Do NOT clone a fresh copy from a public URL, and do NOT try SSH, gh, or Composio for the push.

═══ BRIEF 1 — FRONTIER INTELLIGENCE (Angelo) · files at repo ROOT ═══
1. Read (from the working copy): briefing_goal.md, briefing_system_prompt.md, briefing_archive.md, email_template.html.
2. Use briefing_archive.md as memory — continuity, never repeat a covered story.
3. 5–8 web searches ONLY on the beats in briefing_system_prompt.md (NeuroTech, XR, AR/VR, BCI, spatial computing). No general AI-industry drift.
4. Write the full self-contained HTML briefing to briefings/<DATE_ISO>.html.
5. Append today's edition block to briefing_archive.md (immediately after the previous edition block, BEFORE the Thinking Ledger); then UPDATE the living Thinking Ledger (open questions, positions-the-evidence-implies, blind spots) and the summary table, following the ARCHIVE UPDATE FORMAT in briefing_system_prompt.md exactly.
6. Commit + push both files to main with "git push origin HEAD:main" (one commit), message "Frontier Intelligence — <DATE_LONG>".
7. EMAIL: take email_template.html, replace ONLY the {{TOKENS}} ({{DATE_ISO}},{{DATE_LONG}},{{EDITION}},{{CATEGORIES}},{{LEAD_KICKER}},{{HEADLINE}},{{DECK}},{{BULLET_1..4}} as "<b>Topic</b> — one line",{{DEEP_READ}} or delete that <tr>). Button link MUST be https://lazybreadzero.github.io/DailyBrief/briefings/<DATE_ISO>.html . Send the filled template as the Gmail HTML body to angelo.gunther@gmail.com, subject "Frontier Intelligence — <DATE_LONG>". NEVER paste the full briefing or attach it — preview + button only.

═══ BRIEF 2 — APPETITE (Julinka) · files in julinka/ ═══
8. Read (from the working copy): julinka/briefing_goal.md, julinka/briefing_system_prompt.md, julinka/briefing_archive.md, julinka/email_template.html.
9. Memory + continuity as above.
10. 5–8 web searches across the four pillars (Venture Capital, Food, Art, Nature).
11. Write the full HTML briefing to julinka/briefings/<DATE_ISO>.html.
12. Append today's edition block to julinka/briefing_archive.md; update the table.
13. Commit + push both files to main with "git push origin HEAD:main" (one commit), message "Appetite — <DATE_LONG>".
14. EMAIL: fill julinka/email_template.html (tokens {{DATE_ISO}},{{DATE_LONG}},{{EDITION}},{{LEAD_KICKER}},{{HEADLINE}},{{DECK}},{{BULLET_1..4}} as "<b>Pillar</b> — one line",{{DEEP_READ}}). Button link MUST be https://lazybreadzero.github.io/DailyBrief/julinka/briefings/<DATE_ISO>.html . Send to julinkacannes@gmail.com, subject "Appetite — <DATE_LONG>". Preview + button only.

Do BRIEF 1 completely, then BRIEF 2. End state: both new HTML files + both updated archives pushed to main, and two preview emails sent.
```

---

## Verify with **Run now**
On `main` you should see new `briefings/<date>.html` + `julinka/briefings/<date>.html` and both updated archives, plus two preview emails with working buttons. If the push step is skipped or errors, the cause is almost always **"Allow unrestricted branch pushes"** still being off, or the repo not selected as a **Repository** on the routine.

### If native `git push` still fails (fallback)
Authorise **Composio → GitHub** once (the routine offers a "Connect GitHub to Composio" link), then the commit step can use Composio's *create-or-update-file* tool instead of `git push`. Slower and adds a dependency, but works without the proxy. Ask and I'll swap the persistence block to the Composio version.
