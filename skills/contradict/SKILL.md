---
name: contradict
description: Use when asked to find contradictions or inconsistencies in thinking, or when /contradict is invoked. Do NOT use for pressure-testing a single belief — use /challenge for that.
---

# Skill: /contradict [argument]

Find where Shane's vault contradicts itself — direct oppositions, contextual tensions, value conflicts — and distinguish healthy complexity from actual inconsistency.

**Don't:** flag nuanced position-holding as contradiction. Don't soften findings — name the tension directly.

## Steps

1. Parse the argument/topic from Shane's request.
2. Follow [Qwen Protocol](_lib/qwen-protocol.md) with:
   - `task`: "Vault access (bash only, no MCP tools): `obsidian search query='TERM' limit=10`, `obsidian read file='Note Name'` (no .md). Find logical tensions, contradictions, or inconsistencies in the vault related to '[argument]' (or across the full vault). Where does Shane contradict himself or hold competing beliefs?"
   - `skill`: "contradict"
3. Review Qwen's result, synthesize if needed, and present to Shane.

## Fallback

If Qwen is unavailable:

1. Run `obsidian search query='[argument]' limit=15` via bash; if no argument, run broad searches via bash: `obsidian search query='believe' limit=10`, `obsidian search query='value' limit=10`, `obsidian search query='decided' limit=10`
2. Read 10–15 notes by running `obsidian read file='[note name]'` via bash for each, prioritizing notes that state positions or make claims
3. Look for contradictions:
   - Direct contradictions: two notes asserting opposite things about the same topic
   - Contextual contradictions: a stated belief that conflicts with a stated decision or habit
   - Temporal contradictions: a position that changed without acknowledgment
   - Value contradictions: two stated values that pull in opposite directions
4. For each contradiction found, present it as: "In [note A], you say [X]. In [note B], you say [Y]. These are in tension because [reason]."
5. Distinguish between healthy tension (holding complexity) and actual inconsistency (one must be wrong)
6. Present 3–5 most significant contradictions to Shane, with note references
