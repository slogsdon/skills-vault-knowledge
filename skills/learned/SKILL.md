---
name: learned
description: Turn a vault insight or pattern into polished written content — blog draft, LinkedIn post, newsletter section. Use when /learned is invoked, when the user says "write this up", "turn this into a post", "I want to publish about X", or when a /weekly-learnings session surfaces a publishable thread. Do NOT use for raw note-taking (use /log) or for ghost-writing in someone else's voice (use /ghost).
---

# Skill: /learned [argument]

Delegate to Qwen via the stepped execution protocol. Claude orchestrates; Qwen executes.

## Steps

1. Parse Shane's request and extract the argument/topic (if provided)
2. Call `mcp__lmstudio-agent__qwen_start` (standalone) or `mcp__plugin_shane-config_lmstudio-agent__qwen_start` (plugin — use whichever is available) with:
   - `task`: "Vault access (bash only, no MCP tools): `obsidian search query='TERM' limit=10`, `obsidian read file='Note Name'` (no .md). Transform Shane's vault insights about '[argument]' into a polished written piece — a blog post, essay, or reflection. Use his authentic voice."
   - `skill`: "learned"
   - `context`: any relevant context from the current conversation
3. Loop: if `status` is `"running"`, call `mcp__lmstudio-agent__qwen_continue` (or `mcp__plugin_shane-config_lmstudio-agent__qwen_continue` in plugin) with `session_id`; repeat until `status` is `"done"` or `"error"`
4. Review Qwen's `result`, synthesize if needed, and present to Shane

## Task description for Qwen

Vault access (bash only, no MCP tools): `obsidian search query='TERM' limit=10`, `obsidian read file='Note Name'` (no .md).

Transform Shane's vault insights about '[argument]' into a polished written piece — a blog post, essay, or reflection. Use his authentic voice.

## Fallback (if qwen_start/qwen_continue unavailable)

Execute the skill directly:

1. Run `obsidian search query='[argument]' limit=10` via bash to find notes related to the topic
2. Read the top 5–10 most relevant notes by running `obsidian read file='[note name]'` via bash for each
3. Extract key insights, observations, and recurring ideas from those notes
4. Transform them into a polished written piece in Shane's voice:
   - Use first-person, direct prose (not listicles unless the content demands it)
   - Lead with the most surprising or hard-won insight
   - Build a narrative arc: what changed, what was learned, why it matters
   - End with an open question or implication
5. Present the piece to Shane
