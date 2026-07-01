---
name: labs-pr-review
description: PR review skill for planday-labs repositories. Checks correctness, secret hygiene, data classification compliance, and dependency risk. Load when reviewing a PR or before merging.
---

# planday-labs PR Review

This skill is the standard review gate for pull requests in planday-labs repositories.

## When to use

Load before:
- Merging any pull request
- Reviewing a teammate's PR
- Assessing whether a branch is ready to merge

## Review checklist

### Secrets and credentials
- No secrets, tokens, API keys, passwords, client secrets, or private keys in code, comments, or test fixtures
- No credentials in workflow files (use repository secrets via `${{ secrets.NAME }}`)
- No `.env` files committed with real values

### Data handling
- Review what data the change introduces or touches
- Apply Xero's Data Classification Standard — if the change introduces personal data, it is likely **Sensitive (p)** at minimum
- No production datasets copied into the repo, fixtures, or local files
- No data sent to unapproved third-party tools or AI services
- If the change increases the sensitivity of data the project handles, flag it for re-assessment before merging

### Correctness
- Logic is correct and handles edge cases
- No obvious bugs or unintended side effects
- Existing functionality is not broken

### Dependencies
- New dependencies are from known, maintained sources
- No obviously abandoned or suspicious packages
- Dependency versions are pinned or reasonably bounded

### Workflows
- Changes to `.github/workflows/` do not introduce supply chain risk (pinned action versions, no untrusted third-party actions)
- No workflow change grants excessive permissions

### Housekeeping
- Unused code, files, or credentials from earlier experiments are removed
- If the project no longer needs a resource (environment, automation, dataset), it is shut down

## Severity

| Level | Meaning | Gate |
|---|---|---|
| P0 | Secret exposed, production data leak, broken workflow, security issue | Block |
| P1 | Data classification concern, unapproved data use, correctness bug | Block unless explicitly waived |
| P2 | Cleanup needed, missing comments, minor improvement | Note and proceed |
| P3 | Style, naming | Proceed |

## Output

```
## labs PR Review
**Verdict:** APPROVE | REQUEST_CHANGES

### Findings
- [P0/P1/P2/P3] <file>:<line> — <description>

### Summary
<one sentence on the overall change>
```

If there are no findings, state `No issues found` and approve.
