---
name: principle-privacy-logging
description: "Log metadata needed to debug, never secrets or the project's defined sensitive content. Use when adding logs, traces, or error reports."
---

# Privacy and logging

**Why:** Logs leak. OWASP’s logging cheat sheet: do not log credentials, session tokens, or unnecessary personal data. Once in a log sink, data is copied, retained, and often over-privileged.

**Pattern:** Log identifiers, timing, error class. Define “sensitive” in `SDD/AGENTS.md` (PII, PHI, payment, message bodies). User content in a database is an ADR, not a `console.log`.

**Boundaries:** Local debug of a failing test may print fixtures; strip before commit.

**Source:** https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html
