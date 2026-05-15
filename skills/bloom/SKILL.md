---
name: bloom
description: Map the branching question space from a topic — sub-questions, adjacent domains, meta-framings. Use when /bloom is invoked or Shane asks "what questions does X open up", "bloom on X". Do NOT use to trace how thinking evolved — that's /trace.
---

# Skill: /bloom [argument]

Expand a topic into its question space as a tree — questions that nest and relate, not a flat enumeration, with Level 3 meta-framings that challenge how the topic is posed.

**Don't:** flatten the bloom into a list. Don't surface only obvious sub-questions — Level 3 reframings that challenge the topic's framing are where the value is.

## Steps

1. Parse the argument/topic from Shane's request.
2. Follow [Qwen Protocol](_lib/qwen-protocol.md) with:
   - `task`: "Vault access (bash only, no MCP tools): `obsidian search query='TERM' limit=10`, `obsidian read file='Note Name'` (no .md). Map how '[argument]' branches into sub-questions across the vault. Level 1: immediate follow-on questions. Level 2: adjacent topics and domains with shared structure. Level 3: meta-questions that challenge how '[argument]' is framed. Note which branches are already explored in the vault vs. blank. Suggest 1–2 unexplored branches most worth pursuing. Output as a structured tree, not a flat list."
   - `skill`: "bloom"
3. Review Qwen's result, synthesize if needed, and present to Shane.

## Fallback

If Qwen is unavailable:

1. Run `obsidian search query='[argument]' limit=10` via bash; read relevant notes.
2. Map the bloom: Level 1 (direct sub-questions), Level 2 (adjacent questions and shared structures), Level 3 (meta-framings that challenge how the topic is posed).
3. Note vault coverage vs. blank branches. Suggest 1–2 most worth pursuing.
4. Present as a structured tree.
