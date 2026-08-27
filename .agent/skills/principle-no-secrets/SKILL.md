---
name: principle-no-secrets
description: "API keys, tokens, passwords, connection strings go in env or a secret manager. Never commit .env. Use when wiring credentials."
---

# No hardcoded credentials

**Why:** A secret in git is a published secret. Rotation is the only fix. OWASP secrets management: store secrets in a dedicated system; inject at runtime.

**Pattern:** `.env` gitignored. Commit `.env.example` with empty names. Production: secret manager. Tests: fakes, not real keys.

**Boundaries:** Public client IDs and non-secret config may live in repo if the vendor documents them as public.

**Source:** https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html
