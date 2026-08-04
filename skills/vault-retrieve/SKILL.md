---
name: vault-retrieve
description: Answer a question from the vault — generate the query fan-out, read every match, and return the relevant content verbatim with its paths. Use when Shane says "what do my notes say about X", "search the vault for X", "pull everything on X", "check my notes before we start", or when any task needs vault context before it can proceed. Do NOT use to write or update notes (use /obsidian or /ingest), to find links between two known concepts (use /connect), or to trace how an idea changed over time (use /trace).
---

# Skill: /vault-retrieve [topic]

Return what the vault actually says about a topic — pick the queries yourself, read the hits, and quote them, so the asker never has to hand over a list of search commands.

**Don't:** run one broad query and stop; the matcher is fuzzy and returns a near-identical set for any broad phrasing, so one query means one blind spot. **Don't** report a filename as an answer — a hit is a candidate, and the note has to be read before you can say what it holds. **Don't** paraphrase when the asker needs the source; return the text.

## Steps

1. **Read [vault-map.md](../_lib/vault-map.md)** for folder layout and query heuristics. It is why this skill exists — hand-written retrieval prompts kept re-supplying the map.
2. **Generate 3–5 narrow queries**, differently worded, covering:
   - the topic's own vocabulary
   - its **aliases and former names** (projects get renamed — LeadSurface material is also filed under `signalbloom` and `Lede`)
   - an adjacent framing likely used in a title
   ```bash
   obsidian search query='<term>' limit=10
   ```
3. **Read every plausible hit** — `obsidian read path='<exact path>'` (or `file='<name>'` without `.md`). Read in full. A range read is how a note gets misreported.
4. **Return the content**, grouped by note, each with its path. Verbatim for anything the asker will quote, act on, or check. Summarize only the clearly peripheral.
5. **State the gaps.** Name what you searched that returned nothing. "Nothing in the vault covers X" is a real answer and more useful than a stretched match.

## Output

```
## <topic> — N notes

### <path/to/Note.md>
<relevant content, verbatim>

### <path/to/Other.md>
<relevant content, verbatim>

## Not found
Searched: <queries that returned nothing useful>
```

## Scope guards

- Default to `Knowledge/`. Include `Archive/` only when asked about history — it holds superseded material that reads as current.
- `Daily/` is episodic. Search it for "when did I do X", not for what Shane thinks about X.
- Never reach vault files through `Read`/`Grep`/`Glob` or a direct bash path. The `obsidian` CLI is the only supported access path.
