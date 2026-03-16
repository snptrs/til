# Git workflows

### Dependent feature branch rebase workflow

> **Scenario:** You’re working on a feature that needs backend and frontend changes in a monorepo. You want to keep both parts separate so you can do separate PRs. You branch backend off of main and implement the changes. You need the backend features to implement the frontend features, so you branch frontend off of backend. If you make any other changes to backend, you need to keep frontend in sync.

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

