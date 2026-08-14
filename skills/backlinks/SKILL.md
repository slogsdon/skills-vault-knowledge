---
name: backlinks
description: Use when asked to audit backlinks or repair the knowledge graph structure, or when /backlinks is invoked. Do NOT use for finding conceptual bridges between ideas — use /connect for that.
---

# Skill: /backlinks [argument]

Audit the vault's backlink structure to surface orphaned notes, dead links, and one-way connections — the value is in finding what the knowledge graph has lost or never built.

**Don't:** use this to find conceptual bridges — that's /connect. Don't auto-fix findings — surface for Shane to act on.

## Steps

1. Parse the argument/topic from Shane's request.
2. Follow [Qwen Protocol](../_lib/qwen-protocol.md) with:
   - `task`: "Vault access (bash only, no MCP tools): `obsidian search query='TERM' limit=10`, `obsidian read file='Note Name'` (no .md), `obsidian backlinks file='Note Name'`. Audit the vault's backlink structure around '[argument]' (or broadly). Find orphaned notes, broken connections, and opportunities to strengthen the knowledge graph."
   - `skill`: "backlinks"
3. Review Qwen's result, synthesize if needed, and present to Shane.

## Fallback

If Qwen is unavailable:

1. If `[argument]` is provided, run `obsidian search query='[argument]' limit=10` via bash; otherwise run broad searches (e.g. `obsidian search query='MOC OR index OR hub' limit=20`) via bash to sample the vault
2. Read a set of notes by running `obsidian read file='[note name]'` via bash for each — look for `[[wikilinks]]` and `[[note references]]` embedded in them
3. Identify backlink health:
   - **Orphaned notes:** notes that exist but appear nowhere as a `[[link]]` in other notes
   - **Dead links:** `[[links]]` that reference notes that don't exist yet
   - **One-way links:** A links to B, but B never links back to A despite being clearly related
   - **Hub notes:** notes that are referenced frequently — check they're actually well-developed
4. If scoped to `[argument]`, analyze the local backlink cluster; if broad, sample across the vault
5. Present findings as:
   - Orphaned notes (list with brief description of what's isolated)
   - Dead links / missing notes worth creating
   - Recommended reciprocal links to add
   - Hub notes that need more development
6. Prioritize the top 3–5 highest-value repairs
