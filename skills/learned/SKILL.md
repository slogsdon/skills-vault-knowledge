---
name: learned
description: Turn a vault insight or pattern into polished written content — blog draft, LinkedIn post, newsletter section. Use when /learned is invoked, when the user says "write this up", "turn this into a post", "I want to publish about X", or when a /weekly-learnings session surfaces a publishable thread. Do NOT use for raw note-taking (use /log) or for ghost-writing in someone else's voice (use /ghost).
---

# Skill: /learned [argument]

Transform vault insights into a polished written piece — blog post, essay, or reflection — in Shane's voice, grounded in specific vault material, not a bullet dump.

**Don't:** produce a bullet list of insights — write narrative prose. Don't start with the most recent note — lead with the most surprising or hard-won insight.

## Steps

1. Parse the argument/topic from Shane's request.
2. Follow [Qwen Protocol](../_lib/qwen-protocol.md) with:
   - `task`: "Vault access (bash only, no MCP tools): `obsidian search query='TERM' limit=10`, `obsidian read file='Note Name'` (no .md). Transform Shane's vault insights about '[argument]' into a polished written piece — a blog post, essay, or reflection. Use his authentic voice."
   - `skill`: "learned"
3. Review Qwen's result, synthesize if needed, and present to Shane.

## Fallback

If Qwen is unavailable:

1. Run `obsidian search query='[argument]' limit=10` via bash to find notes related to the topic
2. Read the top 5–10 most relevant notes by running `obsidian read file='[note name]'` via bash for each
3. Extract key insights, observations, and recurring ideas from those notes
4. Transform them into a polished written piece in Shane's voice:
   - Use first-person, direct prose (not listicles unless the content demands it)
   - Lead with the most surprising or hard-won insight
   - Build a narrative arc: what changed, what was learned, why it matters
   - End with an open question or implication
5. Present the piece to Shane
