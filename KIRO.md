# Kiro

How to install and use the `i-have-adhd` skill in [Kiro](https://kiro.dev).

Kiro has no plugin marketplace for this repo. It reads [Agent Skills](https://kiro.dev/docs/skills.md) natively from a `.kiro/skills/` directory: the same `SKILL.md`, no conversion. This repo already ships the Kiro copy at `.kiro/skills/i-have-adhd/SKILL.md`, kept in sync with the canonical `skills/i-have-adhd/SKILL.md`.

## Install

Pick a scope:

- Workspace (this project only): the skill is already at `.kiro/skills/i-have-adhd/` — nothing to do beyond opening the project in Kiro.
- Global (every project): copy the skill into your home Kiro directory.

```bash
git clone https://github.com/ayghri/i-have-adhd
mkdir -p ~/.kiro/skills
cp -R i-have-adhd/skills/i-have-adhd ~/.kiro/skills/
```

On a name collision, the workspace copy wins over the global one.

## Use

1. Start a new Kiro chat session (skills are indexed at session start).
2. Type `/i-have-adhd` to turn the mode on for the session.
3. Say `stop adhd mode` or `normal mode` to turn it off.

Trailing text after the command is passed as extra context, e.g. `/i-have-adhd summarize this file`.

## Verify

Type `/` in the chat input and confirm `i-have-adhd` appears in the command list. Or check the folder:

```bash
ls .kiro/skills/i-have-adhd      # workspace scope
ls ~/.kiro/skills/i-have-adhd    # global scope
```

## Update

Re-copy the folder after pulling the latest canonical skill:

```bash
git -C i-have-adhd pull
cp -R i-have-adhd/skills/i-have-adhd ~/.kiro/skills/    # global scope
```

For the workspace copy, sync `.kiro/skills/i-have-adhd/SKILL.md` from `skills/i-have-adhd/SKILL.md` (the rule body is identical; only the frontmatter `description` is adjusted for Kiro).

## Uninstall

Delete the skill folder:

```bash
rm -rf .kiro/skills/i-have-adhd      # workspace scope
rm -rf ~/.kiro/skills/i-have-adhd    # global scope
```

## Activation notes

- Installed, not always on. The `description` is written for explicit invocation, so the mode stays off until you type `/i-have-adhd`.
- Kiro does not honor the `disable-model-invocation` frontmatter flag used by Claude Code and Qwen Code. Kiro decides auto-activation by matching your request against the skill `description`; the Kiro copy's description is scoped to manual invocation to keep it invoke-only in practice.
- Want a hard guarantee against auto-activation? Attach the skill to a custom agent via its `resources` field (`skill://.kiro/skills/i-have-adhd/SKILL.md`); custom agents do not auto-load skills.

## Troubleshooting

- `/i-have-adhd` not in autocomplete: start a new session. Skills are indexed at session start.
- Installed but replies still preamble: open a new session; confirm the folder name matches the frontmatter `name` (`i-have-adhd`).
- Want different rules: edit `skills/i-have-adhd/SKILL.md` (canonical), then re-copy to `.kiro/skills/i-have-adhd/`.
