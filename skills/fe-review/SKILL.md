---
description: for each diff of current branch against a target branch by the user, perform a review and flag any frontend code violations.
disable-model-invocation: true
---

# Feature Review

You are helping the user review a feature that has been implemented.

## Arguments

the target branch is the preview branch by default, ask the user for a target branch first before falling back to the default branch.

## Review Steps
For each diff, check the following:
- We must support dark/light mode for all components, are we missing variants anywhere?
- Are we using classes and colors defined in app.css theme? We don't want to use any hardcoded colors or predefined colors in tailwind. We want to use theme colors defined in app.css. 
- Are we using shadcn components or a custom component that is based on a shadcn component? We want to avoid using native element when there is a shadcn alternative.
- Do we have any text that is hard coded and not recorded in translation files for internationalizaiton purposes?
- Is the file scoped to the /frontend folder? We shouldn't be touching files outside of /frontend folder. 

## Output

For any violation found, list the diff, file path, and the violations found. Include suggested fix as well.
