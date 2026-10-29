---
name: delegate
description: Orchestration pattern for AI coding agents — keep the judgment on the strongest model, delegate everything else by default to cheaper models through self-contained briefs. Works on Claude Code, Antigravity and ChatGPT/Codex; the model for each tier is set in one editable block at the top. Use on any task that involves reading, researching, or writing more than a couple of lines, or when asked to delegate, use subagents, work in parallel, save tokens, manage context, or save the expensive model for judgment. Includes model tiers per AI system, decomposition into units, a named-worktree convention (one per writer), audit tiers by risk, and the context rules — what to keep out, what to write to disk, when to compact. The brief is the deliverable; it must carry what a weaker model would not think of on its own.
---

## Configuration — edit only this block

```
SYSTEM:    auto    # auto | claude | antigravity | codex
                   # auto = use the system whose subagent tools you actually have
AUTO_LAND: false   # true  = after every check passes, commit and push without asking
                   # false = stop after verification and ask the user first
```

| Tier | What runs on it | Claude Code | Antigravity | ChatGPT / Codex |
|---|---|---|---|---|
| `TIER_JUDGMENT` | The main session: judgment, architecture, writing briefs, final verification. Never delegated. | `fable` (`opus` if Fable is not available to you) | `pro` | `gpt-6-astra` |
| `TIER_WORKER` | Subagents: writing code against a brief, tests, multi-file refactors, research, summaries, audits | `sonnet` | `flash` | `gpt-6.1-sol` |
| `TIER_LOOKUP` | Subagents: yes/no, a path, a count, a symbol's location, any mechanical check | `haiku` | `flash_lite` | `gpt-6-luna` |

**How to read the rest of this file.** Everywhere below, `TIER_JUDGMENT`, `TIER_WORKER` and `TIER_LOOKUP` mean *the model in this table for the active system*. Raw model names appear only here and in "Calling a subagent on each system".

**Notes on the table**
- Model names change often. Edit the cells, nothing else.
- **Claude Code:** `opus`, `sonnet`, `haiku` and `fable` are aliases that always point to the newest version of that family. To pin a version, use a full ID such as `claude-sonnet-5`.
- **Antigravity:** you choose a *tier*; the platform decides which concrete model version it is today.
- **ChatGPT / Codex:** these are explicit model IDs. `gpt-6.1-sol` offers near-`gpt-6-astra` performance at lower cost, which is why it is the worker.
- Last verified: 2026-10-16 against the official docs — [Claude Code subagents](https://docs.claude.com/en/docs/claude-code/sub-agents), [Claude Code models](https://docs.claude.com/en/docs/claude-code/model-config), [Codex subagents](https://developers.openai.com/codex/subagents), [Codex models](https://developers.openai.com/codex/models).

---

# Delegate

You are the `TIER_JUDGMENT` model — the expensive one. Your value is not in typing the code or reading the files — a cheaper model does both fine *when told exactly what to do*. Your value is in knowing what "exactly" means: the edge case that will bite, the existing helper that must be reused instead of duplicated, the reason the obvious approach is wrong here, the one line that will fail silently. **The job is to write that knowledge into a brief and hand the brief off.** Every time you do the work yourself instead, you burn your context on file dumps and spend judgment on keystrokes.

## How this skill is laid out

This file is what you need **every turn**: the rule, the brief, the tiers. Everything consulted once — platform calls, worktree lifecycle, landing, plan storage, latency, context, verification detail — lives in `references/` and is loaded when that step comes up. Do not read a reference you do not need this turn; this skill is about context, and it practices what it says.

| Load | When |
|---|---|
| `references/subagent.md` | **Every brief** — paste it verbatim at the top of the prompt. It is the contract the subagent is held to, not a skill it might load. |
| `references/audit.md` | **Every tier-1 or tier-2 audit brief** — paste it after `subagent.md`. Self-contained: Check 0, severity scale, scoring, report format, conduct. |
| `references/dimensions.md` | The auditor's full 7-dimension checklist and grep patterns — attach to tier-2 audit briefs |
| `references/platforms.md` | Before the first subagent call of the session, to get the call shape for the active `SYSTEM` |
| `references/worktrees.md` | Before spawning any writer |
| `references/plans.md` | Before writing `plan.md` or any artifact to disk |
| `references/latency.md` | When planning a wave of more than two agents |
| `references/context.md` | When the session is long, or before compacting |
| `references/verification.md` | When a result comes back |
| `references/landing.md` | When verified work is ready to commit |

---

## Model economy

Models are not interchangeable, and you should not spend the most expensive one on work a cheaper one does equally well.

- **Judgment is bought once.** Understanding the problem, choosing the architecture, naming the helper to reuse, marking the traps and writing the brief all happen at `TIER_JUDGMENT`.
- **Execution is bought cheap.** Once the brief exists, the decisions are made. A `TIER_WORKER` model with a good brief writes the same code, the same tests and the same refactor as the top model, at a fraction of the cost and latency. Sending a `TIER_JUDGMENT` subagent to type code you already specified is paying twice for the same thinking.
- **Mechanical questions are bought cheapest.** Yes/no, a path, a version, a count: `TIER_LOOKUP`.
- **When a subagent does deserve `TIER_JUDGMENT`:** a tier-2 audit (see Audit tiers) or a question that is genuinely architectural. Nothing else.

If a `TIER_WORKER` result comes back wrong, the first suspect is the brief, not the model. Fix the brief before you reach for a bigger model.

## The Default Is to Delegate

**The burden of proof is on doing it yourself.** Before you read a file, run a search, or write a function, the question is not "should I delegate this?" — it is "why would I not?" If you have no answer in one sentence, delegate.

This includes the small things, which is where the rule is usually broken:

| You are about to… | Delegate it as… |
|---|---|
| Read three or more files to understand how something works | A lookup brief: "How does X work? Cite file:line." |
| Grep for callers, usages, definitions | A lookup brief with the exact symbols |
| Read a long doc, log, PR, or transcript to summarize it | A subagent brief: "Summarize for this purpose; return these fields." |
| Check whether something exists or is already implemented | A lookup brief with a yes/no answer contract |
| Look up how a library or API works | A research brief with the exact question and version |
| Compare two or three approaches or libraries | A research brief with the criteria and the decision you need to make |
| Write any function, component, migration, or test whose shape is clear | An implementation brief |
| Run the test suite, the build, the linter, and read the output | A verification brief: run these, report failures with file:line |
| Refactor across many files mechanically | A refactor brief with one worked example and the rule |

The reason is not only cost. Every file you read yourself sits in your context for the rest of the session. A subagent reads it, extracts the answer, and the file dump dies with it. **Your context is for judgment; theirs is for material.**

## The Narrow Exceptions

Do it yourself only when one of these is literally true:

- **The output needs no interpretation.** The test is not how many commands — it is what you do with the result. `ls` to see if a path exists, `cat package.json | grep version`, `git status`: the answer is consumed as-is. But if you would have to *read* the output and think about it — a file's contents, a test failure, a grep with twenty hits — that reading is the work, and it goes to a subagent.
- **The task needs the conversation** and it cannot be summarized in a paragraph. Rare — if you can explain it to the user, you can explain it to a subagent.
- **The task is the judgment itself.** Architecture, ambiguity resolution, tradeoffs, anything where the user might need to be asked. Subagents cannot talk to the user.
- **You could not verify the result.** If you cannot check it, you cannot delegate it.
- **Applying an auditor's TRIVIAL fix.** The code is already written and reviewed; a brief would only relay it. See § Trivial-fix closure.

"The brief would take as long as the work" is **not** on this list on its own. Writing the brief *is* the work — it is the part that needs you. If the brief is short because the task is simple, it costs nothing; if it is long because the task has traps, it was worth writing.

---

---

## The Split

| You keep | You delegate |
|---|---|
| Understanding the request and its unstated constraints | Reading the codebase to map what exists |
| Decomposing into units with clean boundaries | Web research against a precise question |
| Every decision that requires seeing the whole | Writing code against a precise spec |
| Writing the briefs | Running tests and builds, reporting results |
| Reading the results critically | Mechanical transformations across many files |
| Integration, tradeoffs, talking to the user | Producing the first draft of anything with a clear shape |

The line is **judgment vs execution**. If a step requires deciding, keep it. If it requires doing what was decided, hand it off.

---

---

## The Brief

This is the whole skill. A brief is not a task description; it is **a transcript of your thinking, written so someone with less of it can execute**. The test: if a competent contractor who has never seen this repo received only this document, would they produce what you would have produced?

### Template

```markdown
## Goal
<One paragraph. What, and — critically — WHY. The why is what lets the
subagent make the small decisions you did not anticipate the way you would have.>

## Context you do not have
<Everything from the conversation or your knowledge that the subagent
needs and cannot discover on its own. Stack, conventions, where things
live, what was already tried, what the user cares about.>

## Decisions already made — do not revisit
<The differentiators. Every choice you have already made, with the reason.
Which library. Which pattern. Which existing helper to reuse. Which
approach NOT to take and why. Specific names, specific paths, specific
values. This is where your judgment transfers.>

## Scope
IN:  <exactly what to produce>
OUT: <what looks adjacent but is not this task — name it so they do not wander>
DO NOT TOUCH: <files or areas that are off limits>

## Mirror this
<A path to existing code that does something structurally similar.
"Look at X, do it like that" transfers convention faster than describing it.>

## Traps
<The things you know will go wrong. The API whose default is wrong.
The test setup that must be extended, not replaced. The export that must
keep its name. Every gotcha you would catch and they would not.>

## Acceptance — I will check these
<Concrete, runnable, binary. Commands and expected output. Not "it works".>

## Return
<Exact shape of what to send back: files touched with one line each,
the diff of the critical file, decisions they had to make that you did
not cover, flagged clearly. And: STOP conditions — when to report back
instead of guessing.

Always ask for two more things, by name — see "What they saw and did
not touch" below:
  1. What they noticed and deliberately did NOT touch because the scope
     fence said so, with file:line. Real problems, not untidiness.
  2. Whether their change creates a new problem in code they were told
     not to touch. The blast radius of the fix, not just the fix.>
```

### The short form — for lookups, searches, and summaries

The full template is for implementation. A research or exploration brief needs four things, and can be five lines:

```markdown
QUESTION: <one precise question — not a topic, a question with an answer>
WHERE:    <paths, packages, URLs, or "the whole repo" — bound the search>
CONTEXT:  <the one or two facts that change what a good answer looks like>
RETURN:   <the shape: yes/no + evidence · list with file:line · table with these columns · <=200-word summary for this purpose>
ALSO:     <"anything broken you trip over on the way, even if I did not ask" — optional, but it is
           free: they are already reading that code, and the finding dies with their context otherwise>
STOP IF:  <the condition under which they should report instead of digging further>
```

Examples:

```markdown
QUESTION: Where is session userId read from, and does anything cache it?
WHERE:    src/server/**, src/app/api/**
CONTEXT:  I need to key a rate limiter on it; a cached stale id would be a bug.
RETURN:   Every read site as file:line, plus yes/no on caching with the evidence.
STOP IF:  There is more than one session implementation — tell me, do not pick one.
```

```markdown
QUESTION: What does this incident postmortem conclude, and what did it leave open?
WHERE:    docs/incidents/2026-08-12.md
CONTEXT:  I am about to add rate limiting and want to know if that was the recommended fix or something else was.
RETURN:   <=150 words: root cause, recommended fix, open questions. Quote the recommendation verbatim.
STOP IF:  The doc references another doc for the recommendation — give me the path, do not summarize a summary.
```

The **RETURN** line is the one people skip, and it is the one that makes the result usable without a second round trip. Say the shape.

### The differentiator checklist

Before sending, run down this list. Each item is a thing a strong model does by reflex and a weaker one does only when told:

- [ ] **Reuse over creation** — named every existing helper, client, type, or util that must be reused instead of reinvented
- [ ] **Convention** — pointed at a file to mirror, so naming, structure, and error handling match without a lecture
- [ ] **The wrong obvious path** — named the approach a reasonable person would take and why it is wrong here
- [ ] **Edge cases** — listed the ones that matter: empty, null, concurrent, offline, the 31st request
- [ ] **Failure policy** — said what happens when the dependency is down: fail open, fail closed, retry, degrade
- [ ] **Specific values** — actual names, actual paths, actual numbers. `Ratelimit.slidingWindow(30, "1 m")`, not "a reasonable limit"
- [ ] **Invariants** — what must not change: exported names, public signatures, storage paths, existing tests
- [ ] **The gotcha** — the library quirk, the config that is not picked up from env, the build step dev mode skips
- [ ] **Scope fence** — named the adjacent things that are NOT this task
- [ ] **Stop conditions** — told them when to come back instead of improvising: "if X does not exist, stop and report"
- [ ] **The other side of the fence** — asked, by name, what they noticed and did not touch, and whether their change breaks anything they were told to leave alone
- [ ] **The why** — explained the purpose well enough that unanticipated micro-decisions go the right way

If a brief has fewer than five of these, it is a task description, not a brief. Do it yourself or think harder.

### Example — the same task, twice

**Task description (what a weak delegation looks like):**

> Add rate limiting to the messages endpoint.

**Brief:**

```markdown
## Goal
Per-user rate limiting on POST /api/messages, 30 requests per minute.
Why: on 08-12 one client looped and took the endpoint down for everyone.
We need enforcement that protects other users, not punishment — which is
why the failure policy below is what it is.

## Context you do not have
- Next.js app router. API routes are src/app/api/**/route.ts.
- We already use Upstash Redis for sessions. The client is exported as
  `redis` from src/server/redis.ts. Reuse it. Do not add ioredis or a
  second client — one connection pool is a hard rule here.
- Handlers are wrapped in higher-order functions. See
  src/server/middleware/withAuth.ts — that is the pattern.

## Decisions already made — do not revisit
- Sliding window, not fixed. Use @upstash/ratelimit:
  Ratelimit.slidingWindow(30, "1 m").
- Key by userId from the session, NOT by IP. We are behind Cloudflare;
  IPs are shared and useless.
- On limit: 429, body { error: "rate_limited", retryAfter: <seconds> },
  plus a Retry-After header. Use the existing ApiError class in
  src/server/errors.ts so the shape matches every other error.
- Fail OPEN: if Redis is unreachable, log at warn and allow the request.
  Availability beats enforcement for this endpoint.

## Scope
IN:  withRateLimit HOF · apply it to POST /api/messages · unit test for
     the HOF · one integration test that hits the limit
OUT: other endpoints · admin bypass · config UI · dashboards
DO NOT TOUCH: withAuth.ts, the session code, vitest.config.ts

## Mirror this
src/server/middleware/withAuth.ts — same HOF shape, same export style,
same way of reading the session.

## Traps
- @upstash/ratelimit needs the client passed explicitly as `redis:`.
  It does not pick it up from env on its own.
- Redis is mocked in vitest.setup.ts. Extend that mock. Do not create a
  second mock and do not restructure the setup file.
- The route must keep exporting a named `POST`. Not default.

## Acceptance — I will run these
- npm run typecheck -> clean
- npx vitest run src/server/middleware -> green
- 31st request inside a minute -> 429 with Retry-After present

## Return
- Files created/modified, one line each
- Full diff of route.ts
- Anything you decided that is not covered above — flagged at the top,
  not buried
- Anything you noticed in withAuth.ts, the session code or vitest.config.ts
  that is actually broken — file:line, do not fix it
- Whether wrapping the route changes behaviour for any OTHER endpoint,
  or for anything in DO NOT TOUCH
- If the Redis mock cannot express what you need: STOP and tell me.
  Do not restructure test infrastructure to make it fit.
```

Everything in the second version is something you already knew. The first version made the subagent guess at all of it, and the guesses would have been: a second Redis client, IP-based keys, fail-closed, a new mock file, and a default export. Five things to undo.

---


### What the subagent must give back

The Return section of every brief ends with the five items in `references/subagent.md` — decisions beyond the brief, the requested shape, **adjacent findings**, **blast radius**, acceptance results. The third and fourth are the ones briefs forget, and they are where the next bug is: a scope fence keeps a subagent from wandering, and also keeps it silent about what it saw on the other side. Ask, or the finding dies with its context.

---

## Decomposition — cutting work into briefable units

A unit is briefable when one agent can finish it without asking anyone and without touching what another agent is touching. Cut for that.

**Cut by seam, not by layer.** "Backend / frontend / tests" shares files across units and forces a serial chain. "Redis client wrapper / rate-limit middleware / route integration" gives each unit its own files and lets two of the three run at once.

**The test of a good cut.** For each unit you can name: (a) the files it owns, (b) the contract it exposes or consumes — a signature, a type, a path — and (c) whether it needs anything another unit produces. If (a) overlaps between two units, merge them or re-cut. If (c) is yes, they are in different waves.

**Fix the contracts first.** When unit B consumes what unit A produces, write the signature into *both* briefs before either starts. A: "export `rateLimit(userId: string): Promise<Allowed | Limited>` from `src/server/ratelimit.ts`." B: "import it from there; it does not exist yet — code against the signature." That is what lets them run in parallel instead of B waiting on A.

**Size.** A unit is one brief and one review. If the brief needs more than one Goal, it is two units. If the diff will be more than you can read in one sitting, it is two units.

**When a wave is not enough — write a plan file.** Three or more waves, or any unit that depends on a decision not yet made, or work that will outlive this session: write `plan.md` with the units, their contracts, their wave, and their audit tier — in the plan folder per **Plans on disk** below. It becomes the thing that survives compaction. For a long sequence of phases, add a runtime check between phases (run the app, read the console) before each phase merges into the integration branch.

---

## Audit tiers — how much review a unit gets

You verify every unit yourself (above). Whether a *separate* auditor also runs depends on **risk, not size**.

**The auditor is always a fresh agent.** It has no memory of writing the code, no access to your reasoning, and it is told to be adversarial: find what the author missed, and re-verify every claim against the code — never against the brief, the plan or the author's summary. The point is the missing memory, not the model.

| Tier | What runs | When |
|---|---|---|
| **0** | Your verification only | Prototypes, mocks, throwaway · internal tooling with no dependents · purely additive with no shared surface · fully covered by existing tests that pass |
| **1** | + a fresh `TIER_WORKER` subagent reviews the diff adversarially | Changes existing behaviour in production code · touches a module with 3+ callers · schema or storage · a new dependency |
| **2** | + a fresh `TIER_JUDGMENT` subagent does a full adversarial audit · **cannot be waived** | Auth, sessions, permissions · money, billing · PII, data deletion, migrations · public API or contracts |

**Pass bar.** No unresolved critical or high finding. Lower findings are recorded as known debt; fix the ones inside files you are already touching.

### The pass bar — single source of truth

Defined here and nowhere else.

- Production Readiness Score **≥ 85**
- **Zero 🔴 CRITICAL** · **Zero 🟠 HIGH**
- 🟡 MEDIUM and 💡 LOW are **recorded, not blocking** — fix the ones in files you are already touching; log the rest as known debt in the delivery
- ⚪ INFO recorded for future audits
- **Tier 2 overrides:** ≥ 90 and zero MEDIUM, and the audit cannot be waived

**Why not "zero of everything":** LOW means "fix when touching the file anyway" — cosmetic residue that always exists. Requiring zero LOW guarantees the fix loop never terminates, and contradicts the scoring, where nine LOWs still score 91.

**Override per project**, stated in `plan.md`. Internal tooling can ship at 70; anything touching money, auth, or PII is tier 2 by definition.

**Fix loop:** when a report misses the bar, fix every 🔴 and 🟠, fix 🟡/💡 in files already touched, re-run Check 0, re-audit. **Maximum 3 loops** — after the third miss the design is wrong, not the patch. Re-plan, log it in the decisions file, reset the counter.

### Trivial-fix closure — when the score is low but the fix is one line

Severity measures **impact**; it says nothing about **effort**. A missing `await` on a write is 🔴 and a one-word fix. Re-auditing for that spends a full audit to review a diff the auditor already wrote. So, before entering the fix loop, sort every 🔴/🟠 by the auditor's `Fix size` field (see `references/audit.md`):

**A finding is TRIVIAL only if all of these are literally true:**
1. The auditor marked it `Fix size: TRIVIAL` **and** gave the exact before/after code.
2. You apply that code as written. Any deviation — a different variable, an extra line, "while I'm here" — and it is no longer the code the auditor reviewed: not trivial.
3. One file, one hunk, ≤ 5 changed lines, inside the lines the finding cites.
4. It adds no branch, state, dependency, or change to a signature, export, schema, storage path or public contract.
5. It is verifiable by a command: Check 0 plus the unit's acceptance, and — when it is cheap — a test that fails before the fix and passes after.

**Not eligible, ever:** a Check 0 failure (the auditor stopped before the dimensions; nothing else has been audited yet) · a finding repeated 3+ times (that is a pervasive pattern — a hole in the brief, not a typo).

**What you do with them:**
- **All blockers are TRIVIAL →** apply them yourself (this is a narrow exception: no interpretation, the code is given), run the verification commands, and **close without a re-audit**. Recompute the score as *reported score + the points those findings cost*. If that meets the pass bar, the unit passed.
- **Any blocker is NOT TRIVIAL →** normal fix loop. Apply the trivial ones first, so the re-audit sees them already fixed.
- **Tier 2 →** trivial fixes are applied the same way, but since tier 2 cannot be waived, closure needs a **delta check** instead of a full re-audit: a fresh `TIER_WORKER` gets only the finding and the hunk, and answers two questions — *does this close it, does it introduce anything?* Short brief, short answer.

A trivial closure **does not count** against the 3-loop limit. If a verification command fails after the fix, the finding was not trivial: revert to the normal fix loop.

**Record it** in the delivery: each finding closed this way, the line changed, and the command that proved it. That is the evidence a re-audit would have produced.

**Bump one tier** when the writer's Return flags decisions it made beyond the brief. Those are holes in *your* brief — and on your own brief you are the biased reviewer. A cold reader is the only one who catches a faithfully implemented wrong decision.

Assign the tier **in the brief**, so the writer knows what it is being held to, and record it in the plan file.


---

## The loop, end to end

1. **Understand** the request; decide the audit tier. *(you)*
2. **Decompose** into units with contracts; write `plan.md` if more than one wave. *(you — `plans.md`)*
3. **Brief** each unit: template above, `subagent.md` pasted on top. *(you)*
4. **Create a named worktree** per writer; fire the wave in the background. *(`worktrees.md`, `platforms.md`)*
5. **Keep working** while it runs — next brief, next wave. *(`latency.md`)*
6. **Verify** each result yourself; read the decisions and blast-radius items first. *(`verification.md`)*
7. **Audit** at the assigned tier, through a fresh subagent: `subagent.md` + `audit.md` + the handoff — never the brief's decisions. Blockers marked TRIVIAL close per § Trivial-fix closure, not by re-auditing. *(`audit.md`)*
8. **Integrate**, merge, clean up the worktree.
9. **Land** per `AUTO_LAND`. *(`landing.md`)*
10. **Report** in your words — never a pasted subagent report.
