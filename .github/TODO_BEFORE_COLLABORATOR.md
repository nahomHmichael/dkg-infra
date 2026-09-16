Branch protection on `main` is NOT currently enabled.

GitHub restricts branch protection rules (both classic protection and the
newer rulesets) on private repositories to paid plans — GitHub Pro, Team,
or Enterprise — for personal accounts. This account is on the free plan, so
the API calls to protect `main` were rejected with a 403.

As a result, `main` currently has no server-side protection: it is possible
to push directly to it. The PR-only workflow (feature branch → PR → review
→ merge) is being followed by convention only, not enforced by GitHub.

Revisit this once either of the following happens:
- the account is upgraded to GitHub Pro/Team, or
- these repos migrate to the team org (which should come with a paid plan)

Then re-run:

```
gh api --method PUT -H "Accept: application/vnd.github+json" \
  repos/nahomHmichael/<REPO_NAME>/branches/main/protection \
  --input - <<'EOF'
{
  "required_status_checks": null,
  "enforce_admins": false,
  "required_pull_request_reviews": {
    "required_approving_review_count": 1,
    "dismiss_stale_reviews": true
  },
  "restrictions": null,
  "allow_force_pushes": false,
  "allow_deletions": false
}
EOF
```

Once a second collaborator is added and can review PRs, re-run the same
call with `enforce_admins` set to `true`.
