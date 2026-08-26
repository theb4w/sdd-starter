---
name: principle-privacy-logging
description: "Never log sensitive content. Log metadata needed to debug. Use when adding logs, traces, error reports, or analytics."
---

# Privacy and logging

Do not log secrets, tokens, passwords, or the project's defined sensitive content (PII, PHI, payment data, message bodies — listed in `AGENTS.md`). Log identifiers, timing, and error class.

User content in a database is an architecture decision (ADR), not a logging convenience.

**Source:** `AGENTS.md` regra 3.
