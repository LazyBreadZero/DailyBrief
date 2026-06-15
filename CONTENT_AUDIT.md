# Frontier Intelligence — Content Audit & Redesign (June 2026)

*An executive review of Editions 1–15, why the briefs read as "AI," and what changed in the instructions to fix it. This file is the rationale; the changes live in `briefing_system_prompt.md` and `briefing_goal.md`.*

## The verdict

Formatting, timing and delivery are good. **Content is the problem, and it has been getting worse, not better.** Edition 2 (1 June) was genuinely strong — real news, named actors, numbers in context, a concrete point of view. By Editions 14–15 the brief had begun **feeding on itself**: the lead story of Edition 15 was a disputed trade-show exhibitor count (250 vs 3,250); its Deep Read was the brief auditing its own past citation of that number. That is not intelligence about the frontier. It is the brief talking to itself.

The decline is measurable across the run:

| Signal of self-reference (per edition) | Ed 2 | Ed 9 | Ed 11 | Ed 13 | Ed 14 | Ed 15 |
|---|---|---|---|---|---|---|
| "Edition N" callbacks to its own past | 12 | 8 | 20 | 33 | 28 | **39** |
| "this briefing" self-references | 0 | 0 | 5 | 14 | 15 | **19** |
| Uses of the signature word "convergence" | 2 | 0 | 1 | 1 | 32 | **27** |
| Em-dashes (an AI-prose tell) | 49 | 65 | 81 | 83 | 76 | 76 |

## Why it reads as "AI" and low-signal

### Structural causes (why it feels like the same formula every day)

1. **A fixed-volume template against a variable-volume world.** The old prompt mandated ~3,300 words every day: a 4–6-paragraph lead, a pullquote, two secondary stories, 3–5 briefs, two provocations, a "Sit With This," Events Radar, Signal-vs-Noise, and up to two ~1,000-word Deep Reads. The BCI/XR/spatial niche does **not** produce 3,300 words of genuinely new signal daily. The model filled the gap with padding. **This is the root cause of "the same stuff every day."**
2. **The continuity feature metastasised.** "Read the archive fully," "follow-up threads first," "1–2 continuity references" combined into a brief that now references its own past editions constantly (39 times in Ed 15). Continuity stopped being scaffolding for the writer and became the *subject* for the reader.
3. **Running countdowns reported as news.** "Science Corp CE Mark — Fifteen Editions, No Decision." "Android XR Catalyst — 15 days, still no EU cohort." These ran every day, often with an explicit "no new statement this week." A countdown with no news is the definition of noise.
4. **Narrow, repetitive sourcing.** The search strategy was three stale buckets plus "follow-ups first," which re-found the same handful of trade-press stories (AWE, Apple/Samsung glasses, Meta Ray-Bans) day after day. The credibility scale capped "Tier-1 journalism" at *TechCrunch / Road to VR* and never named the *Financial Times*, *The Economist*, Bloomberg, Reuters, primary journals, regulatory databases, or funding data. **The brief was reading XR fan-blogs and rephrasing them.** Thin inputs → thin output.
5. **Forced coverage of every beat.** The structure wanted something from each theme daily. Not every sector yields news every day — and that is fine.
6. **The Deep Read was effectively daily**, so on quiet days it became 1,000 words of methodology navel-gazing.

### Prose-level tells (why it reads as AI even when the news is fine)

The old prompt already said "Economist/FT standard, declarative, no hedging" — and the output broke every one of those rules. A style label is not enough; the specific failure patterns have to be named and banned:

1. **The antithesis reflex** — "not X, but Y" / "It is not A. It is B." The single most recognisable LLM tic; it appeared 5–10× per edition.
2. **The reveal-twist headline** — every headline an ironic em-dash inversion ("Meta Gives 130,000 Blind Veterans the Camera It Just Deleted Code From"). Exhausting and instantly "AI-clever."
3. **The literal "Step back:" label** — broadsheets never label their own structure.
4. **Self-narration** — "Today's Deep Read develops…," "Story 2, below, develops this," "this briefing will use 250 going forward."
5. **Hedge-stacking dressed as rigour** — "consistent with — but does not confirm," "may simply reflect," "watch whether."
6. **Manufactured-profundity closers** — "That should concentrate the mind."
7. **Tic vocabulary on repeat** — "this briefing," "convergence," "the floor," "resource convergence."
8. **Em-dash overload and rule-of-three cadence** ("No new sensors. No implants. No surgical access.").

What FT/The Economist actually do that the brief stopped doing: **lead with the fact, not the frame; keep the writer invisible; state a view plainly then defend it; let wit be dry and rare; and let a short item be short.**

## What changed (summary; full text in the two instruction files)

- **Sourcing rebuilt into tiers.** Tier A = FT, Economist, Bloomberg, Reuters, WSJ, The Information + primary sources (filings, journals: Nature/Science/NEJM/Lancet/STAT, ClinicalTrials.gov, FDA/EMA/MHRA/NMPA, PitchBook/Crunchbase). Tier C trade-blogs may only *point* to a story; the story must be verified and cited from Tier A/B.
- **A rotating sweep guarantees breadth** (capital, clinical/regulatory, platforms, science, policy) so the brief stops tunnelling on the same three stories — but **selection, not rotation, decides what prints.**
- **A hard 80/20 selection bar.** Rank candidates by significance × magnitude × relevance × source quality. Print only what clears the bar. **If one thing clears it, the brief is one story long.** No quota per beat. A running thread is a story only when it *moved*; otherwise it is tracked silently in the archive, never printed as a countdown.
- **Flexible, signal-sized structure.** ~400 words on a quiet day, up to a Deep Read on a big one. Deep Reads are now rare (target 1–2 per *week*).
- **Named the AI tells and banned them**, with positive models and before/after examples.
- **Continuity inverted.** It is a tool for the writer, not a subject for the reader: ≤1 explicit callback per edition, only when a *new* fact advances a thread; no "Edition N" citations in the body; the Thinking Ledger stays private memory in the archive.
- **A leaner Angle.** One provocation most days, tied to a real development, in plain language.

The machinery (HTML design, email teaser, git persistence, archive format) is unchanged — it works.
