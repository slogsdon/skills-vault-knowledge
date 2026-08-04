# Changelog

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
