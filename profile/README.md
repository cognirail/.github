<div align="center">

# Cognirail

**Engineering rails for agentic software.**

Guardrails, lint presets, context systems, and runtime tools for building AI-assisted codebases that stay explicit, reviewable, and maintainable.

[![npm scope](https://img.shields.io/badge/npm-%40cognirail-cb3837?style=flat-square&logo=npm&logoColor=white)](https://www.npmjs.com/org/cognirail)
[![GitHub organization](https://img.shields.io/badge/GitHub-cognirail-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/cognirail)

</div>

## What We Build

| Area | Focus | Status |
| --- | --- | --- |
| Agent guardrails | ESLint presets, role naming, import boundaries, prompt/tool/eval conventions | Active |
| Context infrastructure | Retrieval, memory, topic routing, and context assembly patterns | Planned |
| Prompt systems | Prompt versioning, review workflows, and evaluation loops | Planned |
| Runtime tooling | Small composable tools for agent execution and project hygiene | Planned |

## Current Packages

| Package | Purpose |
| --- | --- |
| [`@cognirail/eslint-config`](https://github.com/cognirail/eslint-config) | Opinionated ESLint flat config and Prettier preset for TypeScript and agent projects |

## Principles

- **Explicit over implicit**: agent code should make boundaries, roles, and exceptions visible.
- **Reviewable by default**: generated code should not be able to silence guardrails inline.
- **Small public surfaces**: internals stay behind stable barrels and package exports.
- **Human-owned decisions**: automation should reduce toil without hiding tradeoffs.
- **Evidence before confidence**: rules, presets, and runtime behavior should be testable.

## Agent Project Shape

```text
src/
  agent/
    runtime/     execution loop and public runtime API
    tools/       tool definitions and schemas
    prompts/     prompt text and factories
    evals/       evaluation cases and harnesses
```

The first Cognirail package focuses on keeping this shape enforceable through lint rules:

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

```bash
pnpm add -D @cognirail/eslint-config eslint typescript prettier
```

```js
import { defineConfig } from '@cognirail/eslint-config';

export default defineConfig();
```
