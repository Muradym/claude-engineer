# Utopia — Claude Code cloud engineering instructions

Repository: `Muradym/claude-engineer`. All user-facing comments/reports in Russian, code and commit messages in English. Time zone: `Asia/Almaty`.

## Scope and separation
- Work only in this authorized repository and the current cloud runner. Do not use or configure the owner's laptop.
- Never access or modify KOKON OMEGA, KOKON MINI LOCAL, Arb Monitor or AI_CINEMA_STUDIO/ARLAN without a separate explicit instruction.
- The phrase Utopia/ユートピア is the name of this project; do not assume it identifies a verified third-party plugin.

## Autonomy with gates
- For an owner-authorized Issue, inspect the repository, plan, implement, verify, commit to a feature branch, and create a Pull Request without routine confirmations.
- Work one task at a time: scope -> implementation -> tests -> diff/secret review -> commit -> PR -> report.
- Never force-push, bypass protection, merge to `main`, change billing, exfiltrate credentials, disable security gates or install unknown code without owner approval.
- A GitHub Actions run is time-bounded. Never pretend this document starts a background daemon.

## Plugins, skills, MCP, and agents
- Discover extensions only when needed for the active issue. Prefer official Anthropic sources and maintained official vendor repositories.
- Before any install, document source, license, package version, network needs, permissions and security risks; avoid remote shell scripts and unreviewed installation hooks.
- Persist project-specific skills under `.claude/skills/<name>/SKILL.md`, project agents under `.claude/agents/`, and nonsecret MCP definitions under `.mcp.json`. Environment-only installations are ephemeral in GitHub-hosted runners.
- Never commit tokens or API keys. Secrets are supplied by GitHub Secrets or another approved secret store. If outbound proxy blocks an endpoint, report the block; do not evade network policy.
- Verify each tool with a real invocation. Record installed, verified, unavailable and blocked separately.

## Engineering standards
- Keep all trading LIVE and withdrawal functionality disabled by default if encountered. No real-money actions.
- Never replace production logic with fake results or skip failing tests to claim green status. Legitimate tests may use mocks, labelled explicitly.
- Before a commit, run applicable syntax checks, linters and tests, `git diff --check`, `git status --short`, inspect changed files for secrets, then commit only relevant files.
- Create a new feature branch and PR; never directly commit to `main` from the agent. Report commit SHA and PR URL. Do not claim PASS without actual output.

## Reports (Russian; concise)
- DONE: 2–3 concrete changes.
- TOOLS: installed/verified/blocked tools.
- EVIDENCE: tests PASS/FAIL, commit SHA, PR URL, workflow link.
- BLOCKED: exact error and smallest required owner action (if any).
- NEXT: one specific next step.
