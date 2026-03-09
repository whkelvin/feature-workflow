---
description: Review implemented feature - run tests, lint, code review, and generate a verification checklist
disable-model-invocation: true
---

# Feature Review

You are helping the user review a feature that has been implemented.

## Arguments

`$ARGUMENTS` is the feature name (kebab-case). If empty, ask the user for the feature name.

## Prerequisites

Read `./feature/<feature-name>/exploration.md` and all files under `./feature/<feature-name>/design/` to understand what was supposed to be built.

## Review Steps — Execute in order

### Step 1: Run Tests
- Identify the test commands for this project (look for package.json scripts, Makefile targets, pytest config, etc.).
- Run all relevant tests.
- Report results: total passed, failed, skipped.
- If any tests fail, list each failure with the test name, file, and error message. put them in a file under failed-tests.md and list all tests that failed. For each test failure, investigate why the tests fail and suggest a fix in failed tests.md. If there are multiple failures, do this in a loop where each failure goes through a test -> fail -> fix -> test until pass cycle, tell the user what you are doing as you go.

### Step 2: Run Linting
- Identify the lint commands for this project.
- Run all linters.
- Report results: total warnings, errors.
- If any lint errors exist, list each with file, line, and message. fix all linting errors.

### Step 3: Code Review
Perform a comprehensive code review using subagents for key areas, only do this on the changed code

- code-quality-reviewer
- performance-reviewer
- test-coverage-reviewer
- security-code-reviewer

Instruct each to only provide noteworthy feedback. Once they finish, review the feedback and post only the feedback that you also deem noteworthy.

Provide feedback using inline comments for specific issues.
Use top-level comments for general observations or praise.
Keep feedback concise.
### Step 4: Verification Checklist
Based on the user stories from exploration.md and the design docs, generate a manual testing checklist:

```markdown
## Verification Checklist

### User Story: <story description>
- [ ] <Step to verify>
- [ ] <Expected outcome>
- [ ] <Edge case to test>

### User Story: <next story>
...

### General Checks
- [ ] All API endpoints return correct status codes
- [ ] Error states are handled in the UI
- [ ] Loading states are shown during async operations
- [ ] Notifications appear after actions complete (if applicable)
- [ ] No console errors in browser dev tools
- [ ] Responsive on mobile/tablet (if applicable)
```

## Output

Save the review report to `./feature/<feature-name>/review.md` with all findings from steps 1-4.

## Working Rules

1. Run tests and linting first before doing the code review — failing tests may highlight areas to focus on.
2. Be specific in code review findings — always include file paths and line numbers.
3. Prioritize critical issues over style suggestions.
4. The verification checklist should be practical — each item should be something the user can manually verify in under a minute.
