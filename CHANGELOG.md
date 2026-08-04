# Changelog

## 0.4.0 — 2026-08-04

**Added `vault-retrieve`** — takes a topic, generates its own query fan-out,
reads every hit, and returns the content verbatim with paths.

Vault retrieval was the widest and longest-running pattern in a
prompt-and-skill audit over 539 sessions: **49 sessions**, active every month
from April to August, and the only family that never went quiet. It was always
hand-written — the prompt supplied the search commands, the folder paths, and
the note names, because no skill carried them. Meanwhile the transcripts show
**3,226 raw `obsidian` CLI calls**. The capability was never missing; the
queries were.

**Added `source-mine`** — mines one external source (GitHub, Google, chat
history, local filesystem, the vault itself) into attributed notes. Derived
from the 2026-04-08 → 04-18 runs that built the original knowledge graph, each
of which was written from scratch.

**Added two `_lib` references:**
- `vault-map.md` — folder layout, note counts, and query heuristics. This is
  the payload of `vault-retrieve`; hand-written prompts kept re-supplying it.
- `source-recipes.md` — per-source endpoints, extraction targets, and pitfalls.

## 0.3.0 — 2026-08-04

**Added `ingest`** — synthesizes one raw source (Clipping, article, transcript,
pasted text) into a Concept page conforming to `Context/Vault Schema.md`, then
registers it in `Inbox/vault-index.md` and `Inbox/vault-log.md`.

It was reviewed for removal alongside the 0.2.0 pruning and kept: the Vault
Schema contract is live, `Concepts/` holds 52 pages, and nothing else writes
that format. `learned` produces published content, `capture` is generic durable
knowledge, `meeting` targets `Meetings/`.

Fixed three stale references in the process — `/inbox-process` → `/inbox-triage`
(the former was retired with `skills-vault-rituals`), and the index/log paths,
which live in `Inbox/` rather than the vault root.

README resynced: it had still listed all seven removed lenses and omitted
`ingest`, `expand`, and `weekly-signals`.

## 0.2.0 — 2026-08-04

**Removed 7 analytical lens skills:** `bloom`, `compound`, `contradict`,
`drift`, `emerge`, `level-up`, `stranger`.

**Why:** a prompt-and-skill audit over 539 sessions (2026-04-03 → 2026-08-04)
recorded 0–1 invocations for each of these, while `obsidian` — the retrieval
skill they all sit on top of — was the most-used skill in the whole corpus.
Each was a single-shot framing over the same vault content: a prompt, not a
capability. Seven near-identical descriptions competing for the same trigger
diluted matching for the skills that do work.

**Where the content went:** consolidated into one Obsidian note,
`Knowledge/Reference/AI Prompts/Vault Lenses`, holding all seven framings.
Paste the framing you want on top of a `vault-retrieve` or `obsidian` call.
Full text also remains in this repo's git history at `c6699e7` and earlier.

**Kept:** `obsidian`, `backlinks`, `challenge`, `connect`, `expand`,
`fix-nested-code-fences`, `ghost`, `learned`, `map`, `meeting`, `trace`,
`vault-index`, `vault-lint`, `weekly-learnings`, `weekly-signals`.

## 0.1.0

Initial release — vault knowledge exploration and synthesis skills.
