---
name: labs-project-health
description: Quick health check for a planday-labs project. Surfaces stale branches, open PRs, failing workflows, exposed secrets, unused resources, and data classification drift. Load when you want a status snapshot of the project.
---

# planday-labs Project Health Check

Run a health snapshot of this planday-labs repository.

## What to check

### Repository hygiene
- List open pull requests — are any stale or blocked?
- List open issues — any that are security or data-related and unresolved?
- Are there stale branches that have not been touched in over 30 days?
- Is the default branch protected?

### Workflow status
- What is the current status of each workflow? Any failing?
- Are deploy workflows still pointing to a placeholder (`echo "not yet configured"`)? If so, is that intentional?
- Are action versions pinned (e.g. `actions/checkout@v4` not `@main`)?

### Secret and credential hygiene
- Run a quick scan: are there any obvious secrets in recent commits or open PRs?
- Are repository secrets in use — do they still appear to be needed?

### Data classification
- Based on the code and recent changes, what data does this project appear to handle?
- Has the classification been documented (e.g. in README or a CLASSIFICATION.md)?
- Has anything changed recently that would increase the sensitivity level?
- If the project handles personal data, is that acknowledged and controlled?

### Dependency health
- Are there open Dependabot PRs? How old?
- Any known vulnerabilities in current dependencies?

### Resource hygiene
- Are there any environments, deployments, or integrations that appear unused?
- Are there credentials or tokens that should be rotated or revoked?

## Output format

```
## Project Health — <repo name>
**Date:** <today>

### Status summary
🟢 / 🟡 / 🔴 — one sentence overall

### Open items
| Area | Finding | Severity |
|---|---|---|
| <area> | <finding> | 🟢 OK / 🟡 Attention / 🔴 Action required |

### Recommendations
- <action item>
```

If the repository appears healthy with no open items, say so clearly.
