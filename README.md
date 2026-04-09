# Skill Forge

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude_Code-skill-orange?style=for-the-badge)](https://claude.ai/claude-code)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=for-the-badge)](https://github.com/apovalov/skill-forge/pulls)

**Build Claude Code skills through collaborative design, not mechanical generation.**

Most AI-generated skills are shallow - they skip gap analysis, ignore existing building blocks, and produce generic instructions. Skill Forge is a 7-phase interactive process that treats skill creation as a design problem, not a text generation task.

## When to use

Use Skill Forge when you want to create a new Claude Code skill or redesign an existing one. It replaces the "just write a SKILL.md" approach with a structured collaborative process.

**Triggers:** `create skill`, `new skill`, `skill forge`, `/skill-forge`

## The 7 Phases

| # | Phase | What happens | Gate |
|---|-------|-------------|------|
| 1 | **Problem Interview** | Deep-dive into the recurring problem (not just "I want a skill that...") | User confirms problem statement |
| 2 | **Gap Analysis** | Scan all installed skills for overlap | User decides: new skill vs extend existing |
| 3 | **Composition Discovery** | Find existing skills to use as building blocks inside the new skill | User reviews composition map |
| 4 | **Design** | Identity, pipeline, output spec, scope guard | User approves design |
| 5 | **Write** | Generate SKILL.md following best practices | File saved |
| 6 | **Pressure Test** | RED/GREEN test - without skill vs with skill | User confirms it works |
| 7 | **Deploy** | Save locally + optional push to GitHub | User confirms |

Each phase produces a deliverable. No phase is skipped. The user reviews before moving forward.

## Why not just ask Claude to write a skill?

Without Skill Forge, you miss:

- **Gap Analysis** - You might build something that already exists in your 50+ installed skills
- **Composition** - Instead of invoking existing skills as building blocks, you rebuild from scratch
- **Scope Guard** - Without explicit "this skill does NOT do X", skills creep in scope until they trigger on everything
- **Pressure Testing** - No way to verify the skill actually adds value vs Claude's default behavior

## Installation

### Claude Code (recommended)

```bash
claude plugin add apovalov/skill-forge
```

### Manual installation

```bash
# Clone the repo
git clone https://github.com/apovalov/skill-forge.git ~/.claude/plugins/skill-forge

# Or just copy the skill file
mkdir -p ~/.claude/skills/skill-forge
curl -o ~/.claude/skills/skill-forge/SKILL.md \
  https://raw.githubusercontent.com/apovalov/skill-forge/main/skills/skill-forge/SKILL.md
```

### Verify installation

In Claude Code, type `/skill-forge` or say "create skill" - you should see the Problem Interview phase start.

## Example session

```
You: I want to create a skill for writing changelog entries

Skill Forge Phase 1: "What problem do you solve again and again?"
You: Every time I finish a feature, I forget to write a good changelog...

Skill Forge Phase 2: "Found 3 related skills. Here's the overlap..."
[gap analysis table]

Skill Forge Phase 3: "Your changelog skill can compose these building blocks..."
[composition map: git-log reading + commit-message patterns]

Skill Forge Phase 4: "Here's the design. Approve?"
[skill identity + pipeline + output spec + scope guard]

You: Looks good, go.

Skill Forge Phase 5: [writes SKILL.md]
Skill Forge Phase 6: "Want me to pressure test it?"
Skill Forge Phase 7: "Saved. Push to GitHub?"
```

## Philosophy

- **A skill is a solution to a recurring problem**, not a file
- **Design before writing** - the design is the product, SKILL.md is just the encoding
- **Compose, don't rebuild** - find existing skills to use as building blocks
- **One question at a time** - never overwhelm with multiple questions
- **Scope guard everything** - explicit antigoals prevent skill creep

## Skill format reference

Skills follow the [Agent Skills specification](https://agentskills.io/specification):

```markdown
---
name: kebab-case-name
description: "Use when [trigger conditions only]. Triggers on 'phrase', 'phrase'."
---

# Skill Title

[Overview]

## Pipeline

[Numbered steps]

## [Sections per phase]

## Common Mistakes
```

Key rules:
- `description` = trigger conditions only, never workflow summary (Claude reads this to decide whether to load the skill)
- Keep description under 500 characters
- Start with "Use when..."

## Contributing

Found a way to improve the process? PRs welcome.

- Bug reports and feature requests: [Issues](https://github.com/apovalov/skill-forge/issues)
- Want to share a skill you built with Skill Forge? Open a PR to add it to the examples

## License

[MIT](LICENSE)
