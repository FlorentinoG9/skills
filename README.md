# Agent Skills

A collection of skills for AI coding agents by [FlorentinoG9](https://github.com/FlorentinoG9). Skills are packaged instructions that extend agent capabilities.

Skills follow the [Agent Skills](https://agentskills.io/) format.

[![skills.sh](https://skills.sh/b/FlorentinoG9/skills)](https://skills.sh/FlorentinoG9/skills)

## Available Skills

### abac-system

Plan, implement, verify, and battle-test production-grade, agnostic Attribute-Based Access Control (ABAC) systems. Centralizes policy decisions, field-level permissions, and query/query-adapter translation from a single source of truth.

**Use when:**

- Designing or implementing ABAC/permissions/policy engines
- Adding typed `can`/`authorize` decisions with auditable reasons
- Enforcing field-level read/edit permissions from the same policies
- Translating authorization rules to database/query filters via an agnostic AST/adapter
- Reviewing or battle-testing authorization for deny-by-default/fail-closed behavior

**Categories covered:**

- Centralized policy model (single source of truth)
- Typed `can`/`authorize` API with structured auditable decisions
- Subject/resource/environment/data attributes and deterministic conflict handling
- Field-level read/edit permissions derived from the same policies
- Agnostic query/filter AST + `QueryAdapter<T>` contract (no hard ORM dependency)
- Service-layer enforcement, parity testing, and adversarial battle testing

## Installation

```bash
npx skills add FlorentinoG9/skills
```

Install a specific skill:

```bash
npx skills add FlorentinoG9/skills --skill abac-system
```

## Usage

Skills are automatically available once installed. The agent will use them when relevant tasks are detected.

**Examples:**

```
Design an ABAC policy engine for my app with ownership, department, and environment rules
```

```
Add field-level read/edit permissions and query filtering from the same ABAC policies
```

```
Battle-test this authorization implementation for fail-closed behavior and query parity
```

## Skill Structure

Each skill contains:

- `SKILL.md` - Instructions for the agent
- `references/` - Supporting documentation (optional)
- `scripts/` - Helper scripts for automation (optional)

## License

Apache-2.0
