# Concept Page Save Protocol

1. Ask Shane: "Save this as a Concept page? (yes/no)"
2. If no: done.
3. If yes: ask "What's your take on this?" and wait for Shane's verbatim response.
4. Create the page:
   ```
   obsidian create name='Concepts/[topic]' content='## Shane'\''s Take\n\n[Shane'\''s words]\n\n## Summary / Key Points / Cross-references\n\n[synthesis output]' silent
   ```
5. Commit:
   ```bash
   VAULT="$HOME/Library/Mobile Documents/iCloud~md~obsidian/Documents/Personal"
   git -C "$VAULT" add '<the note paths you wrote>' && git -C "$VAULT" commit -m "docs: add Concept page for [topic]"
   ```
