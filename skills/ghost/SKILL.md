---
name: ghost
description: Use when you want to answer a question in Shane's voice, when asked to ghost-write as Shane, or when the /ghost command is invoked. Do NOT use for writing in Shane's voice when he is the author — this produces content as Shane, for external use.
---

# Skill: /ghost [argument]

Write content in Shane's authentic voice by grounding in his vault's vocabulary and reasoning style — a mirror, not a generic imitation.

**Don't:** invent voice patterns not present in the vault. Don't use generic writing conventions — mirror what the vault actually reveals about Shane's style.

## Steps

1. Parse the argument/topic from Shane's request.
2. Follow [Qwen Protocol](../_lib/qwen-protocol.md) with:
   - `task`: "Vault access (bash only, no MCP tools): `obsidian search query='TERM' limit=10`, `obsidian read file='Note Name'` (no .md). Answer the question or topic '[argument]' in Shane's authentic voice. Use the Ghost Writer Context file and vault notes to mirror his vocabulary, reasoning style, and tone. Produce content as Shane would write it."
   - `skill`: "ghost"
3. Review Qwen's result, synthesize if needed, and present to Shane.

## Fallback

If Qwen is unavailable:

1. Run `obsidian search query='[argument]' limit=10` via bash to find notes related to the topic
2. Run `obsidian search query='voice OR style OR writing' limit=10` via bash to find notes that reveal Shane's voice patterns
3. Run `obsidian search query='Ghost Writer' limit=5` via bash to find the Ghost Writer Context file if it exists
4. Read 5–8 relevant notes by running `obsidian read file='[note name]'` via bash for each, to absorb his vocabulary and reasoning style
5. Produce the content in Shane's voice:
   - Mirror his vocabulary (direct, specific, no hedging)
   - Use his reasoning style (builds from first principles, acknowledges tradeoffs)
   - Match his tone (intellectually engaged, occasionally dry, no fluff)
   - Cite specific vault material where relevant, as he would
6. Present the ghost-written content to Shane
