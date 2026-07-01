# _labs-base

This is the base repository for all [planday-labs](https://github.com/planday-labs) projects.

Every new repository in the planday-labs org is forked from this one. That means you can pull workflow and skill updates from upstream into your project at any time using GitHub's **Sync fork** button or a `git fetch upstream` / `git merge upstream/main`.

## What's included

| Path | Purpose |
|---|---|
| `.github/dependabot.yml` | Weekly automated dependency update PRs |
| `.github/workflows/secret-scan.yml` | Gitleaks secret scanning on every push and PR |
| `.github/workflows/stale.yml` | Labels stale issues and PRs, closes after inactivity |
| `.github/workflows/deploy-staging.yml` | Deploy to staging on PR — **not yet configured** |
| `.github/workflows/deploy-production.yml` | Deploy to production on merge to main — **not yet configured** |
| `.claude/skills/labs-pr-review/SKILL.md` | Claude Code skill for PR review in the labs context |
| `.claude/skills/labs-project-health/SKILL.md` | Claude Code skill for checking project health |

## Pulling upstream updates into your fork

```bash
git remote add upstream https://github.com/planday-labs/_labs-base.git
git fetch upstream
git merge upstream/main
```

Or use the **Sync fork** button on your repository's GitHub page.

## Data classification

All planday-labs repositories must comply with Xero's Data Classification Standard. If you are unsure about the classification of data your project handles, ask in **#hello-responsible-data-use**.
