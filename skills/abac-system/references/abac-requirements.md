# ABAC Workspace Requirements

## Source requirements
- ABAC as default for ~95% of apps: flexible, centralized policies.
- Single source of truth for permission logic. One place to change who can do what.
- Policy model based on actions/tasks with context: subject/user, resource/target, and other attributes (including environment/external like "is today Friday?").
- API like `can(user, action, resource/context)` returning allow/deny (boolean or structured result) usable everywhere (UI, backend/service layer).
- Attributes can come from user (role, department, ownership), resource (createdBy, department, locked), and environment.
- Advanced: field/column-level permissions per action/resource from same source of truth.
- Database integration: convert same permission rules into a database query/filter (e.g. Drizzle `where`) so queries only fetch permitted data and permission logic is not duplicated. Library must be AGNOSTIC: query/filter AST or adapter interface/translator contract (no hard Drizzle dependency), with example adapter/contract.
- Service layer as single enforcement point; deny by default; easy to audit/review.
- Production-ready: typed API, predictable behavior, testable, documented usage, handles edge cases.

## Eval scenarios (must satisfy)
- Centralized policies, no duplicated rule logic.
- `can` API usable from UI/backend with structured result.
- Environment attributes (e.g. day/time/flag) affect decisions.
- Ownership/department/role rules.
- Field-level read/edit restrictions per action/resource.
- DB query translation without duplication via agnostic filter/adapter.
- Deny-by-default, missing/unknown attributes, policy conflicts/auditability, edge cases.