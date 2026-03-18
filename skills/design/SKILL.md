---
description: Design the implementation plan for a feature - frontend, backend, and API specs
disable-model-invocation: true
---

# Feature Design

You are helping the user create a detailed implementation plan for a feature that has already been explored.

## Arguments

`$ARGUMENTS` is the feature name (kebab-case). If empty, ask the user for the feature name.

## Prerequisites

Read `./feature/<feature-name>/exploration.md` first. If it doesn't exist, tell the user to run `/feature-workflow:explore <feature-name>` first.

## Output Structure

Create the following directory structure under `./feature/<feature-name>/design/`:

```
design/
├── frontend/
│   ├── components/
│   │   └── <component-name>.md    # One file per new/modified component, should include code snippets
│   ├── keyflow/
│   │   └── <feature-name>.md      # detail feature flow, implementation design including code snippets 
│   └── test/
│       └── <test-plan>.md      # what to test
│       └── <test-implemenation>.md      # how to test it
├── backend/
│   ├── db-models/
│   │   └── <model-name>.md        # One file per new/modified table
│   ├── endpoints/
│   │   └── <endpoint-name>/
│   │       └── implementation.md   # detail Implementation including code snippets
│   ├── shared/
│   │   └── implementation.md   # detail implementation including code snippets
│   └── test/
│       └── <test-plan>.md      # what to test
│       └── <test-implemenation>.md      # how to test it
└── api/
    └── <endpoint-name>.md          # API specification per endpoint
```

## API Specification 
Spin up the api-spec-designer agent to come up with what new endpoints are needed, what existing endpoints need modification. 

## Frontend Design
Invoke the frontend-engineer agent to come up with the implementation details for the frontend based on the exploration document and save relevant result into the frontend folder. The keyflow folder should document all files that needs to be modified/added to with code snippet.

When this is done, invoke the frontend-test-planner agent to plan out what needs to be tested on the frontend. 

When this is done, invoke the frontend-test-writer to write the implmentation-plan.

## Backend Design — for each file, include:
Invoke the backend-engineer agent to come up with the implementation details for the backend. 

When this is done, invoke the frontend-test-planner agent to plan out what needs to be tested on the frontend. 

When this is done, invoke the frontend-test-writer to write the implmentation-plan.


## Working Rules — YOU MUST FOLLOW THESE STRICTLY
- when asked to spin up agents, always spin them up in team mode instead of subagent mode even if it's just a team of 1 so that what each agent is doing can be monitored and interrupted.
- API spec needs to be done before frontend and backend design can start. Backend and Frontend design can be done in parallel.
- Frontend design should be done sequentially where implementation is designed first, then test case planning, then test implementation plan.
- Backend design should be done sequentially where implementation is designed first, then test case planning, then test implementation plan.
- provide agents with context on where they should be doing their work by giving them the context of output structure.

## If Resuming
If design files already exist, read them and ask the user where they'd like to pick up or revise.
