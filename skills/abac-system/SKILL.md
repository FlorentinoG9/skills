---
name: abac-system
description: "Trigger: ABAC, attribute-based access control, permissions, policy engine, field-level permissions, database query permissions. Plan, implement, verify, and battle-test production-grade agnostic ABAC systems."
license: Apache-2.0
metadata:
  author: "FlorentinoG9"
  version: "1.2"
---

## Activation Contract

Load for planning, implementing, reviewing, or testing ABAC/permissions/policy-engine systems, including field-level and database query permissions.

## Hard Rules

- Centralize all authorization logic in one policy registry/source of truth; no duplicated allow/deny/field/query rules in UI, handlers, or DB code.
- Deny by default and fail closed on condition/filter errors, missing/unknown attributes, or invalid requests; never guess-allow.
- Provide typed `can`/`authorize` API with structured auditable decisions (`allow`, `reason`, `policyId?`, `matchedPolicies`, plus fields/filter as applicable) usable in UI and service layer.
- Support attributes from `subject`, `resource`, `environment`, and extra context; deterministic conflict handling (e.g. highest priority wins, deny beats allow at same priority) documented and tested.
- Field-level read/edit permissions and query filters must derive from the same policies.
- Keep core framework/DB agnostic: compile to portable filter/AST and translate via `QueryAdapter<T>` contract (no hard ORM dependency). Include memory adapter and a SQL/Drizzle-like translator example with parity to decisions.
- Production-ready only with evidence: `npm run build`, `npm run typecheck` (or equivalent), and `npm test` must pass; report exact commands/results and never claim success without running them.

## Decision Gates

| Need | Action |
|------|--------|
| Access check | `can`/`authorize` returns structured decision; default deny |
| Field control | Derive per-field `read/edit/none` from same policy source; apply least-privilege for known fields when rules constrain |
| DB enforcement | `compileQuery`/`toQuery` -> agnostic AST + adapter; prove parity with `can` and deny-all/unrestricted cases |
| Conflicts/errors | Apply deterministic precedence; condition/filter errors fail closed |
| Integration | Enforce in service layer; UI consumes decisions/projections/query results |

## Execution Steps

1. Read requirements/scenarios/rubric (see references); inventory actions, resources, attributes (incl. environment), field/query needs.
2. Design typed centralized policy model/API (`PolicyEngine`/registry, `can`, `authorize`, field perms, `compileQuery`, `toQuery`, adapters, service helper).
3. Implement agnostic core, adapters/examples, and service-enforcement pattern; change rules in one place only.
4. Verify with automated evidence: build, typecheck, tests covering allow/deny matrix, env/ownership/department/role/locked, field-level read/edit, adapter translation + query parity/no duplication, deny-all/unrestricted, conflicts, and fail-closed edge cases.
5. Battle-test adversarially (bypass attempts, missing attrs, condition/filter throws, mismatches, field leakage, stale env/query misuse) and fix issues found.

## Output Contract

Return:
- Plan/design choices, policy model, precedence, and tradeoffs.
- Files created/modified with key APIs/paths.
- Verification: exact commands + pass/fail evidence and scenario coverage.
- Battle testing: cases tried, findings, fixes.
- Requirements coverage mapping and honest gaps/risks.

## References

- `references/abac-requirements.md` — source requirements and eval scenarios for this workspace.
