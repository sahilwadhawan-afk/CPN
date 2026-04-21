---
name: pr-description
description: Generate and update pull request descriptions. Use when the user wants to create or improve a PR description based on the changes in the current branch, commit history, or diff.
---

# PR Description Skill

Generate clear, structured pull request descriptions based on branch changes, commit history, and diffs.

## Workflow

Make a todo list for all the tasks in this workflow and work on them one after another.

### 1. Gather Context

Collect information about the changes:

```bash
# Get current branch name
git rev-parse --abbrev-ref HEAD

# Get commits since branching from base (usually main or master)
git log main..HEAD --oneline

# Get full diff
git diff main..HEAD

# Get list of changed files
git diff main..HEAD --name-status
```

Also read any existing PR description or issue references mentioned by the user.

### 2. Analyze Changes

Identify:
- **What** changed (files, components, features)
- **Why** it changed (bug fix, feature, refactor, docs, etc.)
- **How** it works at a high level
- Any breaking changes or migration steps required
- Related issues or tickets

### 3. Draft the PR Description

Use the following template:

```markdown
## Summary
<1-3 bullet points describing what this PR does and why>

## Changes
<Bulleted list of notable changes grouped by area if applicable>

## Test Plan
<Bulleted markdown checklist of steps to verify the changes work correctly>

## Notes
<Optional: breaking changes, follow-up tasks, known limitations, or context for reviewers>
```

**Guidelines:**
- Keep the summary focused on the "why", not just the "what"
- Be concise — reviewers skim descriptions
- If there are breaking changes, call them out clearly under Notes
- Include reproduction steps for bug fixes
- Skip sections that don't apply

### 4. Apply or Output the Description

- If the user has an open PR, update it using the GitHub MCP tool `mcp__github__update_pull_request`
- If no PR exists yet, output the description so the user can copy it or create the PR
- If the user asks to create the PR, use `mcp__github__create_pull_request`

## Wrap Up

Summarize what was done:
- What information was used to generate the description (commits, diff, issue refs)
- Whether the PR was updated or the description was just output
- Any suggestions for follow-up (e.g. linking related issues, adding reviewers)
