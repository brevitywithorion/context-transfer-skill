# Context Transfer Skill

A skill for Grok and Grokbot that combats **context rot** by forcing a fresh, accurate Context Snapshot from your persistent memory on every relevant turn.

## What it does

- Reads your durable memory file at the start of conversations or on request.
- Builds a short, prioritized internal **Context Snapshot** (identity, goals, active projects, preferences, recent status).
- Uses that snapshot as the authoritative source of truth for the rest of the response.
- Prevents long threads from diluting or overwriting important facts.

## Installation

### For Grok (this environment)
1. Copy the skill directory into your skills path (e.g. `~/.grok/skills/context-transfer/` or the platform's bundled skills location).
2. Ensure `SKILL.md`, `CHANGELOG.md`, and `evals/` are present.
3. The skill triggers automatically based on its description when context refresh is relevant.

### For Grokbot
1. Place the skill folder where Grokbot loads skills (or paste the contents of `SKILL.md` into a custom agent/skill prompt).
2. Adjust the memory file path in the workflow if your Grokbot memory location differs from `/root/.grok/user_info/memory.md`.
3. Instruct the bot to consult the skill at the start of turns or when you say "refresh context".

## Usage

- Just talk normally — the skill is designed to activate when personal context matters.
- Explicit triggers: "refresh my context", "what do you know about me", "update my info".
- The snapshot stays internal unless you ask for a summary.

## Files

- `SKILL.md` — Core instructions
- `CHANGELOG.md` — Version history
- `evals/` — Test cases and trigger phrases

## License

MIT — use freely.
