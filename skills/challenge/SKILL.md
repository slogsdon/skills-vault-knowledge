---
name: challenge
description: Use when Shane wants to pressure-test a belief, steelman an opposing view, or invoke /challenge. Do NOT use for confirming or validating a position.
---

# Skill: /challenge [argument]

Steelman the strongest opposition to a belief using vault evidence — the value is in the rigour of the challenge, not in protecting the position.

**Don't:** soften the opposition to protect Shane's self-image. Don't look for confirming evidence — look for what challenges the position.

## Steps

1. Parse the argument/topic from Shane's request.
2. Follow [Qwen Protocol](../_lib/qwen-protocol.md) with:
   - `task`: "Vault access (bash only, no MCP tools): `obsidian search query='TERM' limit=10`, `obsidian read file='Note Name'` (no .md). Steelman the strongest opposition to '[argument]'. Identify the most vulnerable assumptions, surface counterevidence from the vault, and pressure-test the position rigorously."
   - `skill`: "challenge"
3. Review Qwen's result, synthesize if needed, and present to Shane.

## Fallback

If Qwen is unavailable:

1. Run `obsidian search query='[argument]' limit=10` via bash to find notes related to the topic
2. Read the relevant notes by running `obsidian read file='[note name]'` via bash for each — look especially for where Shane states the position most confidently
3. Steelman the opposition:
   - Build the strongest possible case against `[argument]` — not a strawman, the actual best version
   - Find the most vulnerable assumptions underlying `[argument]`; name them explicitly
   - Search the vault for any counterevidence — places where Shane's own notes undermine the position
4. Pressure-test the position:
   - What would have to be true for `[argument]` to be wrong?
   - What's the most common smart objection to this position?
   - What would a rigorous critic say?
5. Don't soften it — the value is in the discomfort
6. Present the challenge to Shane as: the strongest opposition case, the most vulnerable assumptions, and the counterevidence found in his own vault
