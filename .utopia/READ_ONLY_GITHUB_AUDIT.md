# UTOPIA-AUDIT-001 — GitHub and GPT↔Claude Code access audit (READ ONLY)

**Owner:** Muradym
**Requested:** 2026-11-14 (Asia/Almaty)
**Status:** READY FOR CLAUDE TO RUN — NOT EXECUTED
**Language:** Russian reports
**Mode:** STRICT READ ONLY, evidence-based
**Purpose:** Diagnose why cloud Claude Code cannot independently reach the GitHub repositories visible to GPT, and audit the available project structure, CI, integrations and known bottlenecks.

## Absolute safety boundaries
- DO NOT change any file, branch, PR, issue, secret, repository settings, permissions or GitHub App installation.
- DO NOT install plugins, MCP servers or dependencies, run workflows, start trading, send orders, create commits, push or deploy.
- DO NOT connect to the laptop, VPS or desktop bridge. No local/cloud infrastructure changes.
- Never use `--ignore-rules`, `--dangerously-skip-permissions`, `gh auth login` (interactive mutation) or any credential bypass.
- NEVER print, copy, transmit, store or expose tokens, secrets or private repository contents in a public PR/comment/artifact/log.
- Keep KOKON OMEGA, KOKON MINI LOCAL, Arb Monitor, AI_CINEMA_STUDIO/ARLAN, and Utopia fully separated. Audit available GitHub repos individually; do not import code or configurations across projects.
- The ChatGPT GitHub App grant DOES NOT transfer to Claude Code. Never claim Claude has GitHub access until tested from its own environment.

## Phase 0 — Identity and GitHub access proof (execute first)
In the CURRENT CLAUDE CLOUD environment, execute read-only checks:
```sh
claude --version
gh --version
gh auth status
gh api user --jq .login
gh repo view Muradym/claude-engineer --json nameWithOwner,isPrivate,defaultBranchRef
gh repo view Muradym/KOKON-OMEGA --json nameWithOwner,isPrivate,defaultBranchRef
gh repo view Muradym/CLAUDE-CODE-SKILLS --json nameWithOwner,isPrivate,defaultBranchRef
```
- Do not print env vars or inspect raw tokens. If the CLI is unavailable, use authorized GitHub MCP read-only tools, and record their names and exact non-sensitive errors.
- Check the exact effective identity and authorization separately for each repository, and classify `READABLE`, `403 FORBIDDEN`, `404 NOT FOUND`, `PROXY BLOCKED`, `AUTH INVALID`, or `NOT TESTED`.
- `gh auth status` success alone is NOT proof of repository access; verify an actual read on each repo.
- No escalation to write credentials. Request only the minimum missing permission if needed.

## Phase 1 — Read-only repository audit (only readable repos)
Audit each repository separately:
1. Default branch, exact HEAD SHA, clone/access status, branch topology, README/CLAUDE.md, project layout and active configuration.
2. GitHub Actions/workflow definitions, recent run status, failed checks, PRs and issues if enabled; compare configuration vs actual runtime evidence.
3. Secret handling risks from code/config metadata only (do NOT display secret values); dependency integrity, risky shell commands, privilege escalation flags, especially `--ignore-rules`, insecure MCP settings and overly broad write tokens.
4. Claude Code workflows, plugin/MCP/skills definitions and launch commands. Determine what is truly installed and proven vs merely mentioned in docs.
5. KOKON-OMEGA: static audit only. No tests that hit exchanges, orders, billing or external systems. If unavailable, record BLOCKED and continue with other repositories.
6. CLAUDE-CODE-SKILLS: inventory skill names and verify definitions/configuration; no installation.
7. Utopia (claude-engineer): inspect CLAUDE.md, .github/workflows, .utopia, event triggers, permissions, availability of Actions and issue status without enabling anything.

## Phase 2 — GPT ↔ Claude integration diagnosis
Differentiate the following (separately):
- ChatGPT's GitHub App installation and selected repository scope.
- Claude Code cloud GitHub authorization (its own token/OAuth/app).
- GitHub Actions `GITHUB_TOKEN` (scoped to the workflow repository, NOT automatically to KOKON private repo).
- Anthropic/Claude API or OAuth credential for running the model (NOT a GitHub credential).
- Cloud proxy and network allowlists.

Question: Can this running Claude session read all three repos? Give commands actually executed, exact status codes and actionable authorization path where blocked. Do not request secret values in chat.

## Evidence rules
- Report exact repo URL + branch + commit SHA for inspected code, line/file anchors, check/run links when available.
- Classify findings P0/P1/P2/P3, risk, reproduction, suggested correction, verification method, and whether owner approval is required.
- Distinguish CONFIRMED, INFERRED, and NOT VERIFIED. No invented percentages.
- Do not claim access to OpenAI's private source code or ChatGPT internal projects through GitHub.

## Final response, in Russian
1. ACCESS MATRIX: per repo: Claude actual READ access + evidence + error.
2. DONE: which read-only checks were performed.
3. FINDINGS: prioritized P0–P3 with evidence and impact.
4. BLOCKERS: exact missing scopes, secrets, Apps, network policies, or disabled features; identify only the specific owner action that cannot be performed automatically.
5. NEXT: minimal non-destructive steps to make GPT→GitHub→Claude read-only access operational; no execution of changes without new authorization.
6. State explicitly: 'No files or settings were changed; no installations or trading actions were performed' ONLY if accurate.

## Delivery
Send detailed results privately to the owner in the Claude chat (not to any public repository), so the owner can forward the report to GPT. Do not modify files to publish your report.
