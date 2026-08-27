# Where this skill lives

Hosts do not agree on the skills directory. The **content** is `sdd-mode/` (this folder). The **parent** is whichever the running agent already loads.

Resolve **skill root** as the first directory that contains `sdd-mode/SKILL.md`:

1. `<repo>/.cursor/skills/`
2. `<repo>/.grok/skills/`
3. `<repo>/.kiro/skills/`
4. `<repo>/.agents/skills/` (Antigravity)
5. `<repo>/.agent/skills/` (this pack’s checkout)
6. User-level equivalents (`~/.cursor/skills`, `~/.grok/skills`, …)

`templates/` and `playbooks/` are always **next to** `SKILL.md`, never a hardcoded `.agent/` path.

Install: `references/install.md`. Copy or symlink `sdd-mode/` (and `principle-*`, `sdd-tdd`) into that host folder. Do not fork the Markdown.

This checkout is `.agent/skills/`. Cursor loads `.cursor/skills/` **or** an always-on rule that points here (`.cursor/rules/sdd-under-pstack.mdc`).

`SDD/` is always at the **target repo root**, independent of skill root.
