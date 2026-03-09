---
description: Start or continue feature exploration - define the problem, users, use cases, and UI mockups
disable-model-invocation: true
---

# Feature Exploration

You are helping the user explore and define a new feature. The goal is to produce a comprehensive exploration document.

## Arguments

`$ARGUMENTS` is the feature name (kebab-case). If empty, ask the user for the feature name before proceeding.

## Output

Save the exploration document to `./feature/<feature-name>/exploration.md` with the following structure:

```markdown
# Feature: <Feature Name>

## Problem Statement
What problem are we solving and why does it matter?

## Target Users
Who are the primary users affected by this problem?

## User Stories
- As a <user>, I need to <action> so that <benefit>.

## Core Use Cases
Detailed breakdown of each use case.

## UI Mockups & Flow Descriptions
For each flow:
- image mock up for the ui, leave placeholer for user to fill in later. put TODO beside the placeholder
- Step-by-step description of the user interaction
- States: loading, empty, error, success
```

## Working Rules — YOU MUST FOLLOW THESE STRICTLY

1. **Ask strictly ONE question at a time.** Never ask multiple questions in the same turn. Never combine questions. One question per message, no exceptions.
Use the AskUserQuestion tool for discrete choices throughout this planning process. However, use natural text questions when:

The question is truly open-ended with unlimited valid answers
You need detailed explanations that don't fit 2-4 options
You can't anticipate reasonable options upfront
2. Each question must build directly on the user's previous answer, refining the specification incrementally.
3. Follow this structured exploration path in order:
   - **Problem**: What is the problem? Why does it need solving?
   - **Target users**: Who experiences this problem?
   - **Core use cases**: What are the key scenarios?
   - **UI Mockups**: For each flow, propose a mockup with a description. Ask the user to confirm or revise before moving to the next flow.
4. Document frontend needs with mockups — describe each screen/component, layout, and interaction.
5. After all flows are covered, compile the full exploration document and save it.

## Conversation Flow

1. Start by asking: "What problem are you trying to solve with this feature?"
2. After each answer, ask ONE follow-up that drills deeper into the current phase.
3. When a phase is complete, explicitly say you're moving to the next phase.
4. After the final mockup is confirmed, write the exploration document to disk and present a summary.

## If Resuming

If `./feature/<feature-name>/exploration.md` already exists, read it first and ask the user where they'd like to pick up or revise.
