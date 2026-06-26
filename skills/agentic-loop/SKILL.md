---
description: work on a github issue from start to finish.
---

# Workflow
1. Start by checking the github project named 'Kelvin's Retirement Plan' and see if there are any issues with 'Todo' status. If there are none, that's good and you are done. If there are, pick one and change the status to 'In Progress'. Send a message to the private slack channel 'agent-notification' notifiying that work has started if an issue is picked up.


2. Before starting anywork, make sure you are on the latest commit on the main branch.

3. Create a git worktree off of the newest main branch with a new branch in ../loop/<issue-number>-<sensible-branch-name>/ for each issue. <issue-number>-<sensible-branch-name> should be the branch name to work on. Create the folder named 'loop' if it doesn't exist. Do all work in the worktree folder. 

4. When you are done, create a PR on github. Watch the CI to make sure all checks have passed. Fix CI errors until all green. If there are merge conflicts or branch is outdated, rebase on top of the newest main and force push with lease.

5. Link the issue to the PR. Mark the issue status to 'Ready For Review'. Remove the worktree locally once the PR is created. Send a message to the 'agent-notification' channel including a link to the issue and a link to the PR. Provide a brief description of what was done and how the reviewer can verify the fix.

# Acceptance Criteria
1. A PR is created
2. PR is linked to issue
3. Issue status set to 'Ready For Review'
4. Worktree cleaned locally
5. PR ready for merging and all CI have passed
