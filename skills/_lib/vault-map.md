# Vault Map

> Where things live, so a retrieval doesn't have to be told. Regenerate with
> `obsidian folders` + `obsidian files | awk -F/ '{print $1}' | sort | uniq -c`.
> Last verified 2026-08-04.

## Top level (note counts)

| Path | Notes | What's in it |
|---|---:|---|
| `Knowledge/` | 555 | Everything durable. Search here first. |
| `Archive/` | 91 | Superseded. Search only when explicitly asked about history. |
| `Inbox/` | 63 | Unprocessed capture, plus `vault-index.md` and `vault-log.md`. |
| `Daily/` | 60 | One note per day, append-only session log. Episodic, not semantic. |
| `Files/` | 56 | Images, templates, attachments. Rarely a search target. |
| `GP/` | 27 | Global Payments work material. |
| `Reflections/` | 17 | Weekly reviews and self-assessments. |
| `Profiles/` | 12 | `voice.md`, `taste.md` — read before drafting prose or judging design. |
| `MEMORY.md` | 1 | Agent working memory index. |

## Inside `Knowledge/`

- `Concepts/` — the wiki. ~52 pages on the four-section Vault Schema. The main semantic target.
- `Context/` — operating context: `accountability.md`, `patterns.md`, `Vault Schema.md`, `Clippings/`, and `Memory/<project>/` per-project memory (archive only, not read live).
- `Projects/` — per-project folders. Active: `LeadSurface/`, `Loop & Gate/`, `Blog - DevRel Series/`, `Blog - Agentic Workflow Series/`, `Adyt/`, `Paperclip/`, `Local Business Web Presence/`, `Ideas/`.
- `Reference/` — external material: `AI Prompts/` (the prompt library + its two MOCs), `Agent Harnesses/`, `Clippings/`, `Claude Code Academy from Anfloy/`.
- `Meetings/`, `People/`, `Publishing/` — as named.

## Query heuristics

- **Vocabulary drifts.** A project is often filed under an old name — LeadSurface material sits under both `LeadSurface` and `signalbloom`/`Lede`. Search the aliases, not just the current name.
- **Fuzzy matcher.** `obsidian search` is full-text and loose; the same broad query returns near-identical result sets. Two or three *narrow, differently-worded* queries beat one broad one repeated.
- **Read before concluding.** A search hit is a filename, not evidence. Read the note before asserting what it says.
- **Absence is a finding.** "No note covers this" is a legitimate result — report it rather than stretching a weak hit.
