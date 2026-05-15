---
name: level-up
description: Assess current proficiency in a domain and recommend specific growth actions. Use when /level-up is invoked, when the user says "where am I weak in X", "what should I learn next", "level me up on Y", "give me a study plan for Z", or when reviewing a skill area before committing to a learning sprint. Reads vault notes for evidence of current level. Do NOT use for general curriculum advice — this is grounded in the user's existing vault.
---

# Skill: /level-up [argument]

Assess Shane's current proficiency in a domain from vault evidence and identify the specific growth edge — not generic advice, but what the vault shows is missing or underdeveloped.

**Don't:** give advice not grounded in vault evidence. Don't produce a generic curriculum — identify the one capability gap that the vault reveals would unlock the most.

## Steps

1. Parse the argument/topic from Shane's request.
2. Follow [Qwen Protocol](_lib/qwen-protocol.md) with:
   - `task`: "Vault access (bash only, no MCP tools): `obsidian search query='TERM' limit=10`, `obsidian read file='Note Name'` (no .md). Assess Shane's current proficiency with '[argument]' based on vault evidence. What's the next growth edge? What specific actions would level him up?"
   - `skill`: "level-up"
3. Review Qwen's result, synthesize if needed, and present to Shane.

## Fallback

If Qwen is unavailable:

1. Run `obsidian search query='[argument]' limit=10` via bash to find notes related to the topic
2. Read the relevant notes by running `obsidian read file='[note name]'` via bash for each
3. Assess current proficiency based on vault evidence:
   - What does Shane demonstrate understanding of? (concepts he explains, applies, or questions at depth)
   - What's still surface-level? (concepts mentioned but not interrogated)
   - What's conspicuously absent? (things an expert in this area would typically grapple with)
4. Identify the next growth edge — the specific capability gap that, if closed, would unlock the most
5. Propose 2–3 concrete actions to level up (not generic advice — specific to what the vault shows):
   - A thing to read/learn
   - A thing to practice or build
   - A thing to write or reflect on to solidify the knowledge
6. Present the assessment to Shane
