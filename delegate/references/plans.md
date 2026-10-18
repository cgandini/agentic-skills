# Plans on disk — where everything goes

One convention for every plan, so any agent can find and resume it. Defined here because this skill is always loaded.

```
<repo>/documents/plans/
└── 2026-08-21-rate-limit/                       YYYY-MM-DD-<topic>  · date the plan started
    ├── plan.md                                  always exactly this name — the plan itself
    ├── 2026-08-21-rate-limit-requirements.md    every other artifact: YYYY-MM-DD-<topic>-<kind>.md
    ├── 2026-08-21-rate-limit-design.md
    ├── 2026-08-22-rate-limit-research-redis.md  date = when THIS file was written, not the folder's
    ├── 2026-08-22-rate-limit-decisions.md       one decisions log per plan, appended live
    ├── 2026-08-22-rate-limit-brief-redis-client.md
    ├── 2026-08-23-rate-limit-phase-2-middleware.md
    └── 2026-08-23-rate-limit-audit-phase-2.md
```

- **`plan.md` is the only file without a date prefix.** Anything can find it by name: `documents/plans/*/plan.md`.
- **Every other file** is `YYYY-MM-DD-<topic>-<kind>.md`, and the date is **the file's own**, not the folder's. The folder dates when the plan started; each file dates when that step happened — a research note on day 2, a phase mini-plan on day 5, an audit on day 6. Read together, the filenames are the plan's timeline without opening anything. The topic is repeated so the file stays identifiable when it is shared or moved on its own.
- **Flat.** No `research/`, no `.briefs/`, no subfolders. The `<kind>` segment is the grouping: `research-<subject>`, `brief-<unit>`, `phase-<n>-<name>`, `audit-<what>`, `decisions`, `design`, `requirements`, `summary`.
- **`<topic>` is kebab-case** and is the same slug the plan branch uses: folder `2026-08-21-rate-limit`, branch `plan/rate-limit`, worktrees `rate-limit--*`. One slug, everywhere.
- **It lives on `main`.** Create the folder and commit `plan.md` on `main` *before* cutting the plan branch — the plan is the contract, and it exists on the main line from the first day. Progress (phase files, audits, decisions, updates to `plan.md`) accumulates on the plan branch and lands with the final merge.
- **Never overwrite an existing plan folder.** If `documents/plans/<date>-<topic>/` exists with contents, it is a different plan — pick a more specific topic.

