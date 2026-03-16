# Git workflows

### Dependent feature branch rebase workflow

> **Scenario:** You're implementing a feature in a monorepo with interdependent backend and frontend changes. You create separate branches for each (frontend branched off backend) to enable independent PRs. This workflow keeps the frontend branch automatically synced with backend changes through rebasing, ensuring clean commit history and avoiding merge conflicts when both PRs are merged.

1. Branch `feature/backend` off of main.
2. Branch `feature/frontend` off of `feature/backend`.
3. Make changes to `feature/frontend`. Commit and push as normal.
4. Make changes to `feature/backend`, then rebase `feature/frontend` on top:

```bash
git checkout feature/frontend
git rebase feature/backend
git push --force-with-lease
```

Use `force-with-lease` to only force push if nobody else has pushed commits since we last checked.

When ready to merge into main, merge backend MR first, then frontend MR. The frontend MR will only show your frontend-specific commits since it's cleanly rebased on top of backend.

