# Utopia task queue — current safe mode

**Current state (2026-11-14): the only supported GitHub Actions task is a PUBLIC, strictly READ-ONLY audit of this repository.** Full autonomous code editing is **not yet enabled**; it requires a separate reviewed workflow and successful smoke test. No Claude workflow run has been observed.

## Task trigger
1. GPT writes `.utopia/ACTIVE_TASK.md` to `main` using its authorized GitHub connector.
2. The single workflow `.github/workflows/claude-autopilot.yml` triggers directly on a push changing that file. There is no intermediary dispatcher or Issue dependency.
3. Before any Anthropic API credentials are available to the job, an ordinary Python preflight verifies **exactly one** `status: approved` and **exactly one** `mode: read_only_audit` field.
4. Only a valid task can launch the Claude GitHub Action with read-only repository permissions, no Bash execution, a 10-turn ceiling, and a 15-minute timeout.

### Example (do not create until actually ready to run)
```markdown
status: approved
mode: read_only_audit
task_id: UTOPIA-AUDIT-002

# Scope
Audit public Utopia project files only; do not access private repos.

# Evidence
Report file paths, SHA, warnings and unverified points without secrets.
```

## Prerequisites
- Actions must be enabled and allowed to run pinned `actions/checkout` and `anthropics/claude-code-action` in this fork.
- One GitHub repository secret must be configured: `ANTHROPIC_API_KEY` or `CLAUDE_CODE_OAUTH_TOKEN`; availability and billing have **not** been verified.
- This repository is PUBLIC. Do not put private code, private audit details, tokens or confidential reports in task files, workflows, PRs or Actions logs.
- Claude Code's own cloud GitHub authentication is **separate** from ChatGPT's connector. The GitHub Actions token is scoped to Utopia; it does not grant access to private `KOKON-OMEGA` or `CLAUDE-CODE-SKILLS`.
- Private cross-repository audits must happen through Claude's separately authorized cloud session and be delivered privately, outside public GitHub artifacts.
- GitHub Issues are disabled in this repository (GitHub API returned 410). No Issue triggers are present.

## Evidence and status
- The repo's `CLAUDE.md` specifies safe project boundaries.
- `.utopia/READ_ONLY_GITHUB_AUDIT.md` is the separate instruction for Claude's **private cloud chat** to audit access to all three repositories, with no changes.
- The audit workflow file is committed, but **no successful GitHub Actions execution is proven**.
