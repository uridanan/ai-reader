---
description: Stage, commit, and push changes to the repository
---

When the user invokes the `/push` command, automate the process of staging, committing, and pushing the current workspace changes to the remote repository in the current branch.

// turbo-all

1. **Check Status**: Use the `run_command` tool to run `git status` to see if there are any uncommitted changes. If the working tree is clean, inform the user and stop.
2. **Stage Changes**: Use `run_command` to execute `git add .` to stage all modifications.
3. **Commit Changes**: 
   - If the user provided a specific message (e.g., `/push fixed the issue`), use it.
   - If the user just typed `/push`, optionally run `git diff --cached` to see what changed, and generate a concise, conventional commit message automatically (e.g., `chore: update files`, `feat: implement new ui`).
   - Execute `git commit -m "<message>"` using the `run_command` tool.
4. **Push**: Execute `git push origin HEAD` (or just `git push`) using the `run_command` tool to push the changes to the current branch.
5. **Confirmation**: Let the user know the changes have been successfully pushed.
