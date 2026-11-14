# Utopia cloud task queue

The repository has **GitHub Issues disabled** (GitHub returned HTTP 410 on creating an Issue), so the ChatGPT → Claude Code bridge uses one owner-controlled task file:

`.utopia/ACTIVE_TASK.md`

## How it works
1. The owner asks GPT for a specific Utopia task in ChatGPT.
2. GPT writes or updates `.utopia/ACTIVE_TASK.md` on `main` through the authorized GitHub integration. **No laptop work is needed.**
3. `.github/workflows/utopia-task-dispatch.yml` notices this file change and sends a `repository_dispatch` event.
4. `.github/workflows/claude-autopilot.yml` starts `anthropics/claude-code-action@v1` in cloud GitHub Actions, subject to the runner, authentication and budget limits.
5. Claude reads `CLAUDE.md` and the active task, runs bounded verification, creates a branch and proposes a PR when supported. It does not merge into `main`.

## Task file format
Create the file only when execution is intended, not for drafting:

```markdown
status: approved
task_id: UTOPIA-001
title: Verify project build and tests

# Scope
Only Muradym/claude-engineer. Do not touch laptop or other repositories.

# Acceptance criteria
- Inspect build and test configuration
- Make the smallest necessary change
- Run and report actual tests
- Create a branch and PR; never merge automatically
```

## Preflight requirements
- GitHub Actions must be enabled in this fork.
- Provide exactly one authorized cloud credential as a GitHub Actions secret: `ANTHROPIC_API_KEY` or `CLAUDE_CODE_OAUTH_TOKEN`.
- Repository Actions settings must allow creating PRs if automatic PR creation is desired.
- GitHub Actions quotas, Anthropic limits and network policies still apply.
- Do not commit tokens, API keys, secrets, or local-machine credentials.

## Status as of 2026-11-14
Configuration committed. GitHub Issues are disabled. No Claude runtime test has been completed. An Actions run or successful PR is required before reporting an operational autopilot.
