# Install on a host

Canonical files live next to this skill (`sdd-mode/`, plus sibling `principle-*` and `sdd-tdd`). Do not fork the Markdown.

`SDD/` is always the **target repo root**.

## This checkout

Skill files: `.agent/skills/`. Cursor does not load that folder by itself.

**Cursor (this repo):** `.cursor/rules/sdd-under-pstack.mdc` is always-on and points at `.agent/skills/sdd-mode/`. That is enough for composition. Optional: junction so `/sdd-mode` also appears in the skills picker:

```powershell
# from repo root, Windows (Developer Mode or admin for symlinks)
cmd /c mklink /J .cursor\skills .agent\skills
```

```bash
# macOS / Linux
mkdir -p .cursor && ln -s ../.agent/skills .cursor/skills
```

## Copy into a product repo

Copy `sdd-mode/`, `sdd-tdd/`, and every `principle-*` directory into the host skills folder:

| Host | Folder |
|---|---|
| Cursor | `<repo>/.cursor/skills/` |
| Grok | `<repo>/.grok/skills/` |
| Kiro | `<repo>/.kiro/skills/` |
| Antigravity | `<repo>/.agents/skills/` |
| This pack / generic | `<repo>/.agent/skills/` |
| User-level | `~/.cursor/skills`, `~/.grok/skills`, … |

Also copy `templates/cursor-rule.mdc` → `<repo>/.cursor/rules/sdd-under-pstack.mdc` (adjust the skill path if not `.agent/skills`).

## Check

The running agent can resolve `sdd-mode/SKILL.md`. First reply line of a product change names **skill root** and **catalog row**.
