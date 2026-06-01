# Julinka's Brief — *"Appetite"*

A daily personal intelligence briefing for **Julinka Naomi Waesche**, on the four worlds she lives in — **Venture Capital, Food science, Art, and Nature** — written in *Economist*/*FT* broadsheet style and delivered by email every morning at **08:00 Europe/Vienna**.

The publication masthead is **"Appetite"** (from her own tagline — *"a healthy appetite for projects with range"*). It is a sibling of the *Frontier Intelligence* system in this repository: same engine, different reader. It lives entirely in this `julinka/` folder and does not touch the original setup.

## How it works

1. The routine reads [`briefing_system_prompt.md`](./briefing_system_prompt.md) — the generator instructions and house style.
2. It reads [`briefing_archive.md`](./briefing_archive.md) fully — the memory of every prior edition (stories, sources, entities, concepts, open follow-up threads).
3. It runs 5–8 targeted web searches, prioritising follow-up threads from recent editions, then fresh news across the four pillars.
4. It writes a complete self-contained HTML briefing into [`briefings/`](./briefings) as `YYYY-MM-DD.html`.
5. It appends a new edition block to `briefing_archive.md` and updates the summary table.
6. It emails a short HTML snapshot to the recipient.

## Design

The same broadsheet bones as *Frontier Intelligence*, re-skinned with an **enSoie-inspired** palette and her own site's warmth: ivory ground, **goldenrod** accent (replacing red), a thin **Vichy/gingham** rule, a line-art **sun** motif, **Fraunces** headlines + **Source Serif 4** body + **DM Sans** labels, rounded cards and pill buttons.

## Files

| File | Purpose |
|------|---------|
| `briefing_system_prompt.md` | Generator instructions + house style + the "Appetite" design spec. Read first on every run. |
| `briefing_archive.md` | Persistent memory. Read at the start of every run, appended at the end. Seeded with Edition 1. |
| `briefings/` | Output directory — one HTML file per edition. |
| `ROUTINE_SETUP.md` | Copy-paste configuration for creating the daily Claude Code Routine. |

## Setting up the daily automation

See **[`ROUTINE_SETUP.md`](./ROUTINE_SETUP.md)** for the exact prompt, schedule, connectors, and step-by-step instructions. Edition 1 (1 June 2026) is the seed; the first scheduled run will produce Edition 2 and build on Edition 1's open threads.
