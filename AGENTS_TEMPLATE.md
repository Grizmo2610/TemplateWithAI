# AGENTS.md — Project Agent Instructions

> Always-loaded project context for AI coding agents.
>
> This file contains project-independent rules. Project-specific information belongs in separate documentation such as `docs/`, `README.md`, or project configuration files.

## Agent Tooling

The repository may be used with multiple AI coding agents.

- `AGENTS.md` is the shared baseline instruction file.
- Agent-specific instruction files may extend or override these rules where supported.
- Shared skills should live in a repository-level skills directory when supported by the selected agents.
- Prefer a single shared skill implementation rather than maintaining duplicated copies for different agents.
- When multiple agents are available, verify important workflows on the primary development agent first, then verify compatibility with other supported agents.
- Do not assume that a tool-specific feature is available to every agent. Check the repository configuration and the agent's documented conventions.

## Project Context

Project-specific architecture, technology stack, environments, domains, schemas, services, and business terminology must not be hardcoded into this template.

Read the following project documentation when it exists:

- `README.md` — project overview and setup.
- `docs/` — architecture, technical documentation, and domain knowledge.
- `.agents/` or equivalent — shared agent skills and supporting instructions.
- `CLAUDE.md`, `GEMINI.md`, or other agent-specific files — tool-specific instructions.
- `PROJECT_STATUS.md` / `ROADMAP.md` — current project status and planned work.

When project-specific information is required and is not documented, inspect the repository before making assumptions.

## General Operating Rules

- Do not invent project requirements, architecture, business rules, or interfaces.
- Inspect existing code and documentation before modifying behavior.
- Prefer existing project patterns over introducing new patterns.
- Make the smallest change that correctly solves the requested task.
- Do not perform unrelated refactoring.
- Do not modify generated files unless the task explicitly requires it.
- Do not overwrite user changes without explicit authorization.
- Do not expose credentials, secrets, tokens, private keys, or other sensitive configuration.
- Do not commit local credentials or environment-specific configuration.
- When requirements are ambiguous and the ambiguity can materially change the implementation, stop and ask for clarification.
- Record important assumptions when they cannot be avoided.

## Session Protocol

### Start of Session

Before starting a non-trivial task:

1. Check the current repository state.
2. Identify the current branch.
3. Read the relevant project documentation.
4. Check for an active task, specification, or work item.
5. Inspect existing implementation and tests related to the task.
6. Determine the required verification before making changes.

Example:

```bash
git status
git branch --show-current
```

### During the Task

- Keep the active scope limited to the current task.
- Do not start unrelated work because it is nearby or convenient.
- Preserve existing behavior unless the requested change requires otherwise.
- Prefer incremental changes that can be verified independently.
- If an unrelated defect is discovered, record it rather than silently expanding scope.

### End of Session

Before declaring a task complete:

1. Run the required verification.
2. Review the final diff.
3. Confirm that only intended files changed.
4. Update the relevant task/spec/status documentation if required.
5. Report verification evidence.

## WIP Control

Use WIP = 1 for implementation work.

- Work on one task at a time.
- Do not begin another feature before the current task passes verification.
- Do not mix opportunistic refactoring with feature work.
- Keep unrelated bugs out of the current change unless explicitly requested.

## Git & Version Control

### Protected Branches

- Do not commit directly to protected branches.
- Do not push directly to protected branches when the project requires pull/merge requests.
- Follow the repository's branch protection and review rules.

### Safe Staging

Do not blindly stage the entire repository.

Prefer:

```bash
git add <specific-file>
```

before committing.

Check:

```bash
git status
git diff
git diff --cached
```

before creating a commit.

### Dangerous Commands

Do not use destructive Git commands without explicit authorization when they may remove user work.

Examples requiring caution:

```bash
git reset --hard
git clean -fd
git checkout -- <file>
git restore <file>
git push --force
```

Never use `git commit --no-verify` merely to bypass a failing hook.

### Branch Workflow

Use the repository's documented branching strategy when one exists.

A generic convention may be:

```text
<type>/<issue-or-feature>-<short-description>
```

Examples:

```text
feat/feature-name
fix/issue-name
refactor/component-name
docs/update-guide
chore/update-tooling
```

Do not hardcode project-specific ticket formats, domains, schema names, or team names into this template.

### Commit Messages

Use the project's established commit convention.

If none exists, Conventional Commits is a suitable default:

```text
<type>(<scope>): <subject>
```

Common types:

```text
feat
fix
refactor
perf
docs
test
chore
build
ci
```

Keep commit messages concise and describe the actual change.

### Pull / Merge Requests

When the project uses pull/merge requests:

- Every production code change should go through the required review process.
- Include the relevant specification or issue reference.
- Include verification results.
- Mention material risks, migrations, compatibility concerns, or rollback considerations.
- Do not claim approval or completion that has not occurred.

## Coding Standards

Follow the project's existing language and framework standards.

If project-specific coding guidelines exist, they take precedence over generic conventions.

General rules:

- Use clear and descriptive names.
- Keep functions and modules focused.
- Avoid unnecessary abstraction.
- Avoid duplicated logic when a shared abstraction is clearly justified.
- Prefer explicit behavior over clever behavior.
- Handle errors at the appropriate boundary.
- Keep configuration separate from application logic.
- Do not hardcode environment-specific values.
- Avoid magic numbers and unexplained constants.
- Preserve backward compatibility unless a breaking change is intentional and documented.

## Naming

Use the naming convention already established by the project.

Do not impose technology-specific naming schemes globally.

When no convention exists:

- Use descriptive nouns for data structures and objects.
- Use verbs for actions and operations.
- Use consistent casing within each language.
- Use names that communicate units, scope, and lifecycle where relevant.

## Configuration & Secrets

- Keep secrets outside source code.
- Use environment variables or the project's approved secret-management mechanism.
- Do not commit `.env` files containing credentials.
- Provide safe example configuration such as `.env.example` when appropriate.
- Never print credentials or tokens in logs.
- Do not copy production credentials into development configuration.
- Treat connection strings, API keys, certificates, tokens, and private keys as sensitive.

## Data & Database Changes

When working with databases:

- Inspect the existing schema and migration strategy before making changes.
- Use migrations or the project's approved deployment mechanism.
- Avoid destructive schema changes unless explicitly requested and safely planned.
- Consider indexes, constraints, data volume, transaction boundaries, and rollback behavior.
- Do not hardcode environment-specific database endpoints.
- Verify database changes in an appropriate non-production environment before production deployment.
- Do not assume that similarly named fields have identical business meaning across systems or domains.

## API & Interface Changes

Before changing an API, CLI, event, file format, database interface, or other externally consumed contract:

- Find all known consumers.
- Check compatibility requirements.
- Update schemas or contracts when applicable.
- Update tests.
- Update documentation.
- Consider migration and rollback paths.

Do not silently change public behavior.

## Testing

Every behavior change should have appropriate verification.

Use the project's existing test commands first.

Typical verification layers:

### Static / Build Verification

Examples:

```bash
<lint-command>
<type-check-command>
<build-command>
```

### Unit / Component Verification

Examples:

```bash
<unit-test-command>
<component-test-command>
```

### Integration Verification

Examples:

```bash
<integration-test-command>
```

### End-to-End Verification

Examples:

```bash
<e2e-test-command>
```

Do not report a test as passed unless it was actually executed successfully.

If a required test cannot be executed, report the reason and what was verified instead.

## Verification Protocol

For a non-trivial change, verify at the appropriate levels:

1. Syntax / compilation / static checks.
2. Unit or component behavior.
3. Integration or runtime behavior when relevant.
4. End-to-end behavior when relevant.
5. Regression checks for affected existing functionality.

For data-processing changes, also verify where applicable:

- Row counts.
- Null behavior.
- Key integrity.
- Duplicate behavior.
- Boundary conditions.
- Idempotency.
- Source-to-target reconciliation.
- Historical/backfill behavior.
- Performance impact.

The exact verification commands belong to the project documentation, not this generic template.

## Database / Data Processing Safety

When executing scripts that can modify data or schema:

1. Confirm the target environment.
2. Confirm the target database/schema/project.
3. Read the script header and intended scope.
4. Verify that the connection matches the intended target.
5. Prefer dry-run or read-only validation when available.
6. Execute only the required script.
7. Verify the result after execution.

For scripts that perform DDL or destructive DML, require an explicit target declaration where practical.

Example:

```sql
-- TARGET ENVIRONMENT: <environment>
-- TARGET DATABASE: <database>
-- TARGET SCHEMA: <schema>
```

Never assume the current connection is safe merely because the command looks familiar.

## Logging & Error Handling

- Log enough information to diagnose failures.
- Do not log secrets or sensitive data.
- Include useful identifiers such as operation, request, job, or correlation IDs when available.
- Preserve the original error context.
- Fail explicitly when continuing would produce incorrect results.
- Avoid swallowing exceptions without a documented reason.

## Performance

Optimize based on evidence rather than assumptions.

Before optimizing:

- Identify the actual bottleneck.
- Measure current behavior where possible.
- Check data volume and access patterns.
- Consider memory, CPU, I/O, network, and concurrency.

After optimization:

- Re-run relevant tests.
- Compare performance against a known baseline.
- Confirm that correctness has not changed.

Do not introduce premature caching, parallelism, batching, or complexity without a measurable reason.

## Documentation

Keep documentation close to the code or workflow it describes.

Document:

- Architecture decisions.
- Public interfaces.
- Non-obvious business or technical rules.
- Operational procedures.
- Setup requirements.
- Migration steps.
- Known limitations.
- Important assumptions.

Do not duplicate the same source of truth across multiple documents.

When a rule is project-specific, document it in project-specific documentation rather than adding it to this template.

## Specifications & Task Management

For projects using specification-driven development:

```text
specs/
├── README.md
├── templates/
├── active/
└── archive/
```

A typical feature may contain:

```text
<feature>/
├── requirements.md
├── design.md
└── tasks.md
```

Adapt this structure to the actual repository.

When a task requires a specification:

- Understand requirements before implementation.
- Record important design decisions.
- Break implementation into verifiable tasks.
- Keep task status synchronized with actual progress.
- Attach verification evidence to completed tasks when the project requires it.

Do not create a project-specific workflow taxonomy in this generic template.

## Agent Skills

Shared skills may be organized as:

```text
.agents/
└── skills/
    └── <skill-name>/
        └── SKILL.md
```

A skill should contain:

- A clear purpose.
- Trigger conditions.
- Required inputs.
- Procedure.
- Verification criteria.
- Failure handling.

Keep skills focused on reusable workflows.

Project-specific skills should reference project documentation rather than embedding large amounts of project knowledge directly into the skill.

## MCP / External Tools

External tools may be configured through the repository's agent configuration.

Rules:

- Inspect the actual configuration before using an external tool.
- Follow the tool's authentication mechanism.
- Never expose credentials.
- Prefer read-only operations when write access is unnecessary.
- Verify the target resource before destructive operations.
- Do not assume a tool is installed or available merely because it is documented elsewhere.
- Keep environment-specific connection details out of this template.

## Communication

Default language should follow the project's existing documentation and team convention.

For technical work:

- State what changed.
- State what was verified.
- State any remaining limitation or blocker.
- Avoid claiming success without evidence.
- Keep explanations proportional to the task.

## When Requirements Are Unclear

Ask for clarification instead of guessing when ambiguity affects:

- Business logic.
- Data definitions.
- Security.
- External interfaces.
- Production behavior.
- Destructive operations.
- Backward compatibility.
- Architecture decisions.

Do not invent defaults merely to avoid asking.

## Definition of Done

A task is complete only when:

- The requested behavior is implemented.
- Relevant tests or verification have passed.
- The final diff contains only intended changes.
- Documentation is updated when required.
- No known blocking issue has been silently ignored.
- Verification evidence is available.
- The repository remains in a safe, consistent state.

## Out of Scope

This file must remain generic.

Do not add the following here unless they are genuinely universal across every project using this template:

- Specific programming languages or frameworks.
- Specific databases or cloud providers.
- Specific hosts, ports, URLs, schemas, or credentials.
- Specific business domains.
- Specific customer or product definitions.
- Organization-specific team names.
- Organization-specific roles or contacts.
- Organization-specific environments.
- Organization-specific workflow names.
- Specific data marts, tables, packages, or procedures.
- Specific ticket prefixes.
- Specific vendor products.
- Historical incidents that apply only to one repository.
- Project-specific source-of-truth paths.

Put those details in project-level documentation instead.

## Project-Specific Configuration

The following section is intentionally a template placeholder.

Populate it in the project's own documentation, not in this reusable `AGENTS.md`.

```text
Project:
Repository:
Primary language(s):
Framework(s):
Build command:
Test command:
Lint command:
Type-check command:
Deployment process:
Branch strategy:
Commit convention:
Architecture documentation:
Specification location:
Agent-specific instructions:
Shared skills:
External tools:
```
