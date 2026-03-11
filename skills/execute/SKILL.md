---
description: Create an execution plan from the design docs - task breakdown, parallelization, and model assignment
disable-model-invocation: true
---

# Feature Execution

You are helping the user plan the execution of a feature that has been fully designed.

## Arguments

`$ARGUMENTS` is the feature name (kebab-case). If empty, ask the user for the feature name.

## Prerequisites

Read all files under `./feature/<feature-name>/design/`. If the design directory doesn't exist or is incomplete, tell the user to run `/feature-workflow:design <feature-name>` first.

## Process

1. **Read all design docs** — frontend, backend, API specs.
2. **Identify all discrete tasks** — each component, endpoint, migration, test file, etc.
3. **Map dependencies** — determine which tasks block others (e.g., DB migration before endpoints, endpoints before frontend API calls).
4. **Group into execution phases** — tasks that can run in parallel go in the same phase; sequential dependencies create new phases.
5. **Assign model recommendations** — suggest which LLM model tier to use for each task based on complexity:
   - **Opus**: Complex architectural decisions, multi-file refactors, tricky business logic
   - **Sonnet**: Straightforward implementations, CRUD endpoints, component creation, tests
   - **Haiku**: Boilerplate generation, simple config files, repetitive patterns

## Output

Save the execution plan to `./feature/<feature-name>/execution-plan.md`:

```markdown
# Execution Plan: <Feature Name>

## Overview
Brief summary of total tasks, estimated phases, and parallelization opportunities. YOU SHOULD ALWAYS PREFER TEAMS INSTEAD OF SUBAGENTS

## Phase 1: <Phase Name>
These tasks have no dependencies and can be executed in parallel.

### Task 1.1: <Task Name>
- **Type**: backend | frontend | database | api | test
- **Description**: What needs to be done
- **Files to create/modify**: List of file paths
- **Design reference**: Path to the relevant design doc
- **Recommended model**: Opus | Sonnet | Haiku
- **Rationale**: Why this model tier

### Task 1.2: <Task Name>
...

## Phase 2: <Phase Name>
These tasks depend on Phase 1 completion.

### Task 2.1: <Task Name>
- **Depends on**: Task 1.1, Task 1.3
...

## Execution Notes
- Any warnings, risks, or special considerations
- Suggested order within parallel phases if any preference exists
```

## Working Rules

1. Present the full execution plan as a proposal and ask the user to confirm or request changes.
2. Be explicit about WHY tasks are ordered the way they are.
3. Keep tasks granular enough that each can be a single focused coding session.
4. Group related tests with their implementation tasks — don't separate them into a different phase unless there's a reason.
5. ask the user if they want to execute the plan
