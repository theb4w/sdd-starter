---
name: principle-no-secrets
description: "API keys, tokens, passwords, connection strings go in env or a secret manager. Never commit .env. Use when wiring credentials or writing .env.example."
---

# No hardcoded credentials

Put secrets in environment variables or a secret manager. Keep `.env` gitignored. Commit only `.env.example` with empty or fake values.

If a sample in a skill or test needs a key, use a placeholder name, never a real value.

**Source:** `AGENTS.md` regra 4.
