# CLAUDE-GITHUB-ACCESS-002 — full development access check and future VPS preparation

**Owner:** Muradym
**Date:** 2026-11-14 (Asia/Almaty)
**Current phase:** VERIFY GITHUB ACCESS AND COMPLETE READ-ONLY AUDIT.
**Future phase:** Authorized feature-branch implementation, tests and VPS deployment preparation. NOT actual VPS deployment.
**Reporting language:** Russian.

## Account and repository boundaries
Account: `Muradym`.
Repositories:
- `Muradym/claude-engineer` (public; Utopia; self-contained project).
- `Muradym/KOKON-OMEGA` (private; independent KOKON project).
- `Muradym/CLAUDE-CODE-SKILLS` (private; independent skills repository).

Do not mix code, secrets, task queues, or artifacts across these repositories. Other projects (KOKON MINI LOCAL, Arb Monitor, AI_CINEMA_STUDIO/ARLAN) remain outside scope unless separately authorized.

## IMPORTANT: separate identities and permissions
- The ChatGPT/Codex GitHub App installation and permissions are **not** Claude Code's credentials.
- Claude Code on the web/cloud must be authorized with GitHub through its own connection.
- A cloud session can clone/push using the credentials connected to Claude. The **official Claude GitHub App** must be installed on the appropriate account/repositories for private repo access using browser-based setup.
- Account owner `Muradym` has Admin on the three repositories (confirmed by GPT), but this does **not** prove Claude has read or write access.
- Repo `claude-engineer` being publicly cloneable is **not** proof of authenticated GitHub write access.
- Do not invent elevated admin access or attempt credential extraction/bypass.

Official setup:
- https://claude.ai/code
- https://github.com/apps/claude
- https://github.com/settings/installations
- https://code.claude.com/docs/en/claude-code-on-the-web

For code editing, the official Claude app normally requires Contents: read/write and Pull requests: read/write. Workflow operations may require Workflows permission. Do not demand repository Administration permission merely for coding; changes to GitHub account/app authorization require the owner.

## Phase A — verify access now, READ ONLY
In Claude's **own cloud session**, using existing authenticated read-only CLI/MCP tools:
```sh
gh auth status
gh api user --jq .login
gh repo view Muradym/claude-engineer --json nameWithOwner,isPrivate
gh repo view Muradym/KOKON-OMEGA --json nameWithOwner,isPrivate
gh repo view Muradym/CLAUDE-CODE-SKILLS --json nameWithOwner,isPrivate
```
If `gh api` succeeds, additionally inspect current actor permissions without printing tokens:
```sh
gh api repos/Muradym/claude-engineer --jq .permissions
gh api repos/Muradym/KOKON-OMEGA --jq .permissions
gh api repos/Muradym/CLAUDE-CODE-SKILLS --jq .permissions
```
A missing `.permissions` field must be `NOT VERIFIED`, never assumed. Record 403/404/proxy failures exactly. If the cloud's GitHub proxy blocks API calls, attempt supported read-only repository-selector or MCP checks without bypassing policy.

Report for each repository:
`READ: CONFIRMED/BLOCKED`, `PUSH: CONFIRMED/BLOCKED/NOT VERIFIED`, `PR: CONFIRMED/BLOCKED/NOT VERIFIED`, evidence, permissions, errors.

## Phase B — finish separate static audit
Follow `.utopia/READ_ONLY_GITHUB_AUDIT.md`.
- Inspect available repositories' code, CI, PRs, branch rules and vulnerability risks.
- **DO NOT mutate any repository during the read-only audit**.
- Deliver confidential cross-project findings only in the owner's private Claude chat.
- Do not publish sensitive KOKON content to public Utopia repo or GitHub Actions logs.

## Phase C — after audit, future independent coding
The owner intends to permit Claude Code to develop and maintain authorized repositories *after the audit*:
1. In Claude Code cloud, choose the proper repository and `Accept edits` or `Auto` for the authorized implementation task. Plan mode is audit-only.
2. Work on a fresh **feature branch for that repository**, not on `main`. One bounded task -> review code -> tests -> commit -> push -> PR -> report.
3. Verify real push/PR access first by creating a small, non-sensitive, owner-approved test file on an isolated branch **after the read-only audit has finished**. Report branch name, commit SHA and PR URL. Never test write access by modifying `main`.
4. For KOKON-OMEGA, keep LIVE_TRADING and withdrawals OFF, SAFE MODE ON. No credentials in commits/logs. No financial orders.
5. Preparing for a new VPS may include deployment plans, scripts, environment templates without secrets, Docker/CI config, resource budget calculations, rollback and smoke-test checklists. **Do not SSH, install, restart, deploy, change firewall or spend money on VPS** until separately authorized.
6. Claude Code cloud sessions have bounded execution. Do not claim indefinite unattended autonomy without a configured runner and confirmed runtime evidence.
7. No destructive permission or account changes, no bypass flags `--ignore-rules`, `--dangerously-skip-permissions`, no force push and no auto-merge without explicit owner decision.

## Report format (Russian)
- ACCESS: per-repository actual read/write/PR permission (CONFIRMED/BLOCKED/NOT VERIFIED)
- AUDIT: P0-P3, exact file/line/commit evidence
- ROOT CAUSE: distinguish Github App installation vs Claude OAuth/token vs cloud proxy vs GitHub Actions
- FUTURE TASKS: ranked minimal safe changes with tests and readiness to prepare for VPS
- OWNER ACTION: only steps that cannot be done from Claude's present authorized environment
- Never claim any access or success without evidence.
