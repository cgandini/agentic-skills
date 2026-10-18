# Worktrees — one per writer, named for the work

Readers do not get worktrees. Read-only search and research agents read the orchestrator's tree. Only agents that **write** get their own — and every one of them does, because two writers in one tree overwrite each other.

### The shape

Git worktrees are siblings, not nested. The *branches* nest, and the names carry the hierarchy:

```
main
└─ plan/rate-limit                    the orchestrator's integration branch
   ├─ unit/rate-limit/redis-client    writer A   ─┐ wave 1
   ├─ unit/rate-limit/middleware      writer B   ─┘
   └─ unit/rate-limit/route           writer C     wave 2, after A and B merge
```

```
.worktrees/
├─ rate-limit/                  plan/rate-limit               the orchestrator, if not on main
├─ rate-limit--redis-client/    unit/rate-limit/redis-client
├─ rate-limit--middleware/      unit/rate-limit/middleware
└─ rate-limit--route/           unit/rate-limit/route
```

`ls .worktrees/` sorts every unit under its plan. `git branch --list 'unit/rate-limit/*'` lists a plan's units. `git worktree list` shows path and branch side by side. Nothing needs a legend.

- **Integration branch:** `plan/<slug>` for anything with more than one wave or that outlives the session; `main` directly for a small task. Units branch *from* it and merge *back into* it.
- **Slugs:** kebab-case, from the task and the unit's purpose. `rate-limit--redis-client`, never `task-1--part-a`. The name is documentation.
- **Why the `plan/` and `unit/` prefixes:** git refuses `rate-limit` and `rate-limit/x` in the same repo — a ref cannot be both a file and a directory. The prefixes keep the two namespaces apart.

### Lifecycle — the orchestrator owns all of it

**The orchestrator creates the worktree, before spawning.** Not the writer. The orchestrator knows the base branch, the name, and has to track it for the merge. Some systems can create a worktree for you automatically (Claude Code: `isolation: "worktree"`; Antigravity: `Workspace: "branch"` or `"share"`), but the name is random — use that only when the name does not matter.

> **[CRITICAL] BASE RULE:** Always run `git fetch origin` first and branch from `origin/main` — **never** from local `main` (which may be behind if a previous session did not pull in the root checkout).

```bash
# once per repo
mkdir -p .worktrees
git check-ignore -q .worktrees || { echo ".worktrees/" >> .gitignore; git add .gitignore; git commit -m "chore: ignore .worktrees"; }

# ALWAYS fetch and branch from origin/main, never stale local main
git fetch origin

# the integration branch, if using one (multi-wave plans)
git branch plan/rate-limit origin/main

# one per writer, from the integration branch (or directly from origin/main for single-wave tasks)
git worktree add .worktrees/rate-limit--redis-client -b unit/rate-limit/redis-client plan/rate-limit
```

**Bootstrap is step 0 of the writer's brief**, with exact commands — a fresh worktree has no `node_modules` and none of the gitignored env files:

```
Step 0 — bootstrap:
  cd .worktrees/rate-limit--redis-client && cp ../../.env* . && npm ci
  If it fails, STOP and report the output. Do not debug the install.
```

`pnpm` shares its store across worktrees and makes this nearly free. `npm ci` copies — with many parallel writers on a large install, that is the cost to watch.

**The brief confines the writer:**

```
You work in .worktrees/rate-limit--redis-client on branch unit/rate-limit/redis-client.
Do not checkout, switch, rebase, or create worktrees. Commit on your branch when done.
```

**On return — the orchestrator, in this exact atomic order:**

1. Verify per the Verification section, **inside the unit worktree**, before merging anything
2. Merge or rebase onto the latest target (`plan/<slug>` for multi-wave, or `origin/main` after `git fetch origin` for single-wave)
3. A conflict is judgment: resolve it yourself — and if two units touched one file, the cut was wrong; re-cut next time
4. **Push once verified — only if `AUTO_LAND: true`** (`git push origin HEAD:main`), or push the integration branch while multi-wave work is in flight and merge `plan/<slug>` into `origin/main` (`--no-ff`) as soon as the plan completes. With `AUTO_LAND: false`, stop here and ask the user (see Landing).
5. **Fast-forward the root checkout (`main`) right after the push** (`git -C <repo-root> fetch origin && git -C <repo-root> merge --ff-only origin/main`) so the root working directory is never left behind `origin/main`
6. **Mandatory cleanup in the same turn — never leave a finished worktree on disk:**
   ```bash
   git worktree remove .worktrees/rate-limit--redis-client --force && git branch -d unit/rate-limit/redis-client && git worktree prune
   ```

`--force` because a built worktree always has untracked artifacts. `prune` because a worktree directory removed any other way leaves stale metadata that blocks the next `add` with the same name. **A task is NOT complete until its worktree and merged local branch are removed (`git worktree list` must show zero leftover worktrees from finished tasks).**

