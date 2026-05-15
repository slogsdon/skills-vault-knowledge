---
name: stranger
description: Build an outside-observer portrait of Shane from vault evidence — what someone reading only the public artifacts would conclude about who he is, what he cares about, what he's avoiding. Use when /stranger is invoked, when the user says "what would someone think of me from this", "how do I come across", "audit my public self", "stranger view", or before refining a personal-brand bio. Do NOT use for self-described identity work — this is deliberately external.
---

# Skill: /stranger [argument]

Build an outside-observer portrait from vault evidence alone — a stranger's perspective with no insider charity, surfacing what a perceptive outsider would conclude.

**Don't:** protect Shane's self-image in the analysis. Don't draw on self-described identity — only what the vault evidence reveals.

## Steps

1. Parse the argument/topic from Shane's request.
2. Follow [Qwen Protocol](_lib/qwen-protocol.md) with:
   - `task`: "Vault access (bash only, no MCP tools): `obsidian search query='TERM' limit=10`, `obsidian read file='Note Name'` (no .md). Build an outside-observer portrait of Shane based on the vault, focusing on '[argument]' or broadly. What would a perceptive stranger conclude about how he thinks?"
   - `skill`: "stranger"
3. Review Qwen's result, synthesize if needed, and present to Shane.

## Fallback

If Qwen is unavailable:

1. If `[argument]` is provided, run `obsidian search query='[argument]' limit=15` via bash; otherwise run broad topic searches via bash (e.g. `obsidian search query='work' limit=10`, `obsidian search query='ideas' limit=10`, `obsidian search query='journal' limit=10`)
2. Read 10–15 notes by running `obsidian read file='[note name]'` via bash for each, sampling across different topics, time periods, and note types
3. Adopt the perspective of a perceptive stranger reading these notes cold — no insider context, no charity
4. Build a portrait based purely on what the notes reveal:
   - What does this person clearly care about most?
   - What patterns of thinking are immediately visible?
   - What does this person seem to be afraid of or avoiding?
   - What would a stranger guess about their core beliefs, even unstated ones?
   - What would seem strange, inconsistent, or surprising from the outside?
5. Be unflinching — a stranger has no reason to protect Shane's self-image
6. Present the portrait to Shane, with specific evidence from notes for each observation
