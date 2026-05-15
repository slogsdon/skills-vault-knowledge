---
name: compound
description: Use when asked how knowledge has accumulated or compounded around a topic, or when /compound is invoked. Do NOT use for tracing evolution of thinking over time — use /trace for that.
---

# Skill: /compound [argument]

Show how knowledge about a topic has accumulated and compounded in the vault — from seed insight to current frontier — and whether it's still actively growing.

**Don't:** treat this as a summary of current knowledge — it's a map of how insights built on each other. Don't conflate with /trace; compounding is about accumulation, not evolution of position.

## Steps

1. Parse the argument/topic from Shane's request.
2. Follow [Qwen Protocol](_lib/qwen-protocol.md) with:
   - `task`: "Vault access (bash only, no MCP tools): `obsidian search query='TERM' limit=10`, `obsidian read file='Note Name'` (no .md). Show how knowledge about '[argument]' has accumulated and compounded in the vault. What insights build on earlier ones? What's the compounding trajectory?"
   - `skill`: "compound"
3. Review Qwen's result, synthesize if needed, and present to Shane.

## Fallback

If Qwen is unavailable:

1. Run `obsidian search query='[argument]' limit=10` via bash to find notes related to the topic
2. Read the relevant notes by running `obsidian read file='[note name]'` via bash for each, ordered chronologically where possible
3. Map the compounding structure:
   - What was the seed insight — the first or simplest version of the idea?
   - What was added on top? Which later notes build explicitly on earlier ones?
   - Where did combining two ideas produce a third that neither implied alone?
   - What's the current frontier — the most sophisticated form this knowledge has reached?
4. Identify the compounding trajectory: is the knowledge still actively compounding or has it plateaued?
5. Present as a narrative arc: seed → accumulations → synthesis → current frontier → next potential compound
6. Note any gaps where compounding stalled and why
