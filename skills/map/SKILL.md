---
name: map
description: Use when asked to audit or map the structure of the knowledge graph, or when /map is invoked. Do NOT use for auditing backlinks on specific notes — use /backlinks for that.
---

# Skill: /map [argument]

Audit the structural health of the knowledge graph — what's well-connected, orphaned, and missing — to surface where the graph needs attention.

**Don't:** use this for targeted backlink audits — that's /backlinks. Don't auto-fix — surface findings for Shane to act on.

## Steps

1. Parse the argument/topic from Shane's request.
2. Follow [Qwen Protocol](_lib/qwen-protocol.md) with:
   - `task`: "Vault access (bash only, no MCP tools): `obsidian search query='TERM' limit=10`, `obsidian read file='Note Name'` (no .md), `obsidian backlinks file='Note Name'`. Audit the structure and health of the knowledge graph around '[argument]' (or the full vault). What's well-connected, what's orphaned, what's missing?"
   - `skill`: "map"
3. Review Qwen's result, synthesize if needed, and present to Shane.

## Fallback

If Qwen is unavailable:

1. If `[argument]` is provided, run `obsidian search query='[argument]' limit=15` via bash; otherwise run broad searches across topic clusters via bash (e.g. `obsidian search query='MOC' limit=10`, `obsidian search query='projects' limit=10`, `obsidian search query='ideas' limit=10`)
2. Read a sampling of notes by running `obsidian read file='[note name]'` via bash for each — aim for breadth across different sections of the vault
3. Assess knowledge graph health:
   - **Well-connected:** notes with rich cross-references and backlinks to other notes
   - **Orphaned:** notes that exist but aren't referenced from anywhere (no inbound links)
   - **Stub clusters:** areas with shallow coverage — a topic that should have depth but only has surface notes
   - **Missing nodes:** concepts that appear as `[[links]]` in notes but don't have their own notes yet
4. If scoped to `[argument]`, produce a local map of that cluster; if broad, produce a top-level structural overview
5. Present findings as: what's healthy, what's orphaned, what's missing, and 2–3 recommended connections to add
