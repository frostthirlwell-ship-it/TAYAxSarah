# Branch Protection — apply via GitHub UI after Sarah is added

After Sarah's GitHub user is invited as collaborator, configure these settings on `main`:

**Settings → Branches → Add branch protection rule → Branch name pattern: `main`**

Enable:
- [x] Require a pull request before merging
- [x] Require approvals: **1** (cross-AI review enforced)
- [x] Dismiss stale pull request approvals when new commits are pushed
- [x] Require review from Code Owners
- [x] Require conversation resolution before merging
- [x] Require linear history (no merge commits — squash or rebase only)
- [x] Do not allow bypassing the above settings (humans can still bypass via admin)

Do NOT enable:
- "Require deployments to succeed" — no CI yet
- "Lock branch" — would block both AIs entirely
- "Restrict pushes that create matching branches" — branches are how we work

Result: neither AI can land code without the other's approval, but Frost + Jet (org admins) can merge directly if needed.
