# Landing — governed by `AUTO_LAND`

**Verified means all of these, checked by you and not reported to you:**

1. The acceptance commands from the brief ran under your hands and passed
2. The unit's audit tier ran and met the pass bar in `SKILL.md` § Audit tiers
3. Invariants held — `git diff --stat` shows no file from DO NOT TOUCH, exports kept their names
4. The full suite and build pass on the **merged** integration branch, not only in the unit's worktree
5. Nothing in the writer's Return is flagged as unresolved — including its *adjacent findings* and *blast radius* answers

## `AUTO_LAND: false` (the default)

Once verified, stop. Tell the user what is ready, on which branch, and ask before any commit or push. Do not push anything the user has not approved.

## `AUTO_LAND: true`

The user has authorized commit and push without asking — **for verified work only**. Once all five checks are literally true, land before ending the turn. Where it lands depends on the shape of the work:

**Single unit, no integration branch** (a one-wave task cut directly from `main`):

```bash
git fetch origin && git rebase origin/main && git push origin HEAD:main
git -C <repo-root> fetch origin && git -C <repo-root> merge --ff-only origin/main   # root checkout never lags origin/main
git worktree remove <worktree-path> --force && git branch -d <branch> && git worktree prune
```

**Multi-wave work on an integration branch** (`plan/<slug>` — see `worktrees.md`):

- **Each unit** merges into `plan/<slug>` and the plan branch is pushed. `main` does not move.
- **When the plan completes** and the full suite passes on the merged plan branch:

```bash
git checkout main && git pull
git merge --no-ff plan/<slug>        # one merge commit per plan — the whole plan reverts as a unit
git push
git branch -d plan/<slug> && git push origin --delete plan/<slug>
```

The `--no-ff` is the point: a plan that lands as one commit is one `git revert` away from undone. Landing each unit on `main` directly throws that away and leaves `main` half-done between waves.

If any of the five checks is not literally true, or anything is ambiguous, **stop and report** — the authorization covers verified work, not work that is probably fine.

## In both modes, always

Never `--force` to `main` · never push a failing suite · never land tier-2 work whose audit was skipped · never push to a branch the user did not name as the target.
