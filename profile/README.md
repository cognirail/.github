<div align="center">

<img src="../assets/cognirail-icon.png" alt="Cognirail" width="96" />

# Cognirail

**Engineering rails for agentic software.**

Cognirail explores the engineering layer around AI-assisted software:
guardrails, lint presets, ability packages, context contracts, and small tools
that make agent work explicit, reviewable, and maintainable.

[![npm scope](https://img.shields.io/badge/npm-%40cognirail-cb3837?style=flat-square&logo=npm&logoColor=white)](https://www.npmjs.com/org/cognirail)
[![GitHub organization](https://img.shields.io/badge/GitHub-cognirail-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/cognirail)

</div>

## Why This Exists

AI agents can now write, edit, search, call tools, and run tests. The hard part
is no longer only capability. The hard part is making the work stay legible:

- what judgment was applied
- which source was trusted
- where the boundary is
- what evidence proves the result
- how the system should fail when context is missing

Cognirail is about that layer: the rails between raw model capability and
software teams that need stable, inspectable behavior.

## Current Work

| Project | Focus |
| --- | --- |
| [`from-skills-to-abilities`](https://github.com/cognirail/from-skills-to-abilities) | A working model for packaging expert judgment as loadable, routed, validated, and degradable agent abilities. |
| [`@cognirail/eslint-config`](https://github.com/cognirail/eslint-config) | Opinionated ESLint flat config and Prettier preset for TypeScript and agent-shaped codebases. |
| [`python-lint-config`](https://github.com/cognirail/python-lint-config) | Opinionated ruff + ty baseline for Python — AI coding guardrails with no inline escape hatches. |
| [`bash-lint-config`](https://github.com/cognirail/bash-lint-config) | Opinionated shellcheck + shfmt baseline for Bash — the shell sister of the TypeScript and Python presets. |
| [`swift-lint-config`](https://github.com/cognirail/swift-lint-config) | SwiftLint + SwiftFormat guardrails for AI-generated Swift code. |

## Core Model

```text
Tool -> Skill -> Ability -> Cognitive Architecture
```

- **Tools** give agents external capabilities.
- **Skills** give agents procedures.
- **Abilities** give agents judgment contracts.
- **Cognitive architecture** connects abilities, memory, rules, tools, and validation.

The current research direction is **Ability packaging**: a way to move beyond
larger prompt files or more agent personas, and instead package judgment with
source routing, validation, and degradation behavior.

## Engineering Principles

- **Explicit over implicit**: boundaries, roles, exceptions, and trusted sources should be visible.
- **Reviewable by default**: generated code should not be able to hide from guardrails.
- **Small public surfaces**: internals stay behind stable barrels and package exports.
- **Evidence before confidence**: every rule, preset, or ability should have a way to be checked.
- **Human-owned decisions**: automation should reduce toil without hiding tradeoffs.

## Lint Guardrails

One shared stance across languages: **strict baselines, pinned tool versions, and no inline escape hatches**.
Exceptions live in reviewed project config — never as `# noqa`, `# shellcheck disable`, or `eslint-disable` comments.

| Language | Package | Engine |
| --- | --- | --- |
| TypeScript | [`@cognirail/eslint-config`](https://github.com/cognirail/eslint-config) | ESLint flat config + Prettier |
| Python | [`python-lint-config`](https://github.com/cognirail/python-lint-config) | ruff + ty |
| Bash | [`bash-lint-config`](https://github.com/cognirail/bash-lint-config) | shellcheck + shfmt |
| Swift | [`swift-lint-config`](https://github.com/cognirail/swift-lint-config) | SwiftLint + SwiftFormat |

## Agent Project Shape

The TypeScript package focuses on making agent-shaped projects easier to keep consistent:

```text
src/
  agent/
    runtime/     execution loop and public runtime API
    tools/       tool definitions and schemas
    prompts/     prompt text and factories
    evals/       evaluation cases and harnesses
```

```js
import { defineAgentConfig } from '@cognirail/eslint-config/agent';

export default defineAgentConfig({
  tsconfigRootDir: import.meta.dirname,
  boundaries: [
    {
      publicAlias: '@agent/runtime',
      internalGlobs: ['src/agent/runtime/**'],
      consumers: ['src/agent/**', 'src/tools/**', 'test/**'],
    },
  ],
});
```

## Install

**TypeScript**

```bash
pnpm add -D @cognirail/eslint-config eslint typescript prettier
```

```js
import { defineConfig } from '@cognirail/eslint-config';

export default defineConfig();
```

**Python**

```bash
uv add --dev cognirail-python-lint-config
uv run cognirail-python-lint-config check
```

**Bash**

```bash
uv add --dev cognirail-bash-lint-config
uv run cognirail-bash-lint-config check
```

## Start Here

- Read the essay: [`From Skills to Abilities`](https://github.com/cognirail/from-skills-to-abilities)
- Try the TypeScript lint preset: [`@cognirail/eslint-config`](https://github.com/cognirail/eslint-config)
- Try the Python lint preset: [`python-lint-config`](https://github.com/cognirail/python-lint-config)
- Try the Bash lint preset: [`bash-lint-config`](https://github.com/cognirail/bash-lint-config)
- Follow the package scope: [`@cognirail` on npm](https://www.npmjs.com/org/cognirail)
