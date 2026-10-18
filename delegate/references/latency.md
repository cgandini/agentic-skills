# Parallelism

Decompose so that units are **independent** — no unit needs another's output. Then fire them all in one turn and background them.

```
turn 1:  subagent(research A)  subagent(research B)  subagent(search C)   <- all background
turn 2:  keep working: write the next brief, read the plan, answer the user
turn N:  results arrive -> verify -> integrate -> next wave
```

Research fans out well. Implementation fans out only when modules do not share files — and then each writer gets its own worktree, and you merge.

If unit B genuinely depends on unit A's result, that is two waves, not one. Do not fake independence.

---


## Latency — delegating everything without waiting for everything

The cost of delegation is not per subagent; it is per **round trip you wait on**. Ten lookups fired together cost about the same wall-clock as one. Ten lookups fired one after another, each awaited, cost ten cold starts. Every rule here is about collapsing round trips.

**1. Front-load the wave.** At the start of a task, before doing anything else, enumerate every lookup you will plausibly need — where does X live, who calls Y, how does Z work, what does the doc say — and fire them all in one turn, in the background. Then plan while they run. The first wave is the one that hurts if you serialize it, and it is the most predictable.

**2. Fire speculatively.** A background lookup you did not end up needing costs almost nothing. A lookup you needed and did not fire costs a full round trip. When in doubt, fire it. Bias toward wide.

**3. Keep an agent warm instead of spawning cold.** When the system lets you message a subagent that is still alive (Claude Code resumes a subagent and keeps its context; Antigravity has `send_message`), a subagent that has already read a module keeps it in context — follow-up questions to *that agent* are warm. Spawn one agent per domain ("the billing module", "the auth flow", "the design tokens") and keep talking to it rather than spawning fresh for each question. The first question pays the cold start; the rest ride on it. When you cannot message a live subagent, fold the follow-ups into the first brief's RETURN — ask for more than you need now.

**4. Tier by answer shape, not by importance.**

| Answer shape | Tier |
|---|---|
| Yes/no, a path, a version, a count, a single symbol's location | `TIER_LOOKUP` |
| A list with citations, a summary, a comparison, a codebase search, code or tests written against a brief, a refactor, a tier-1 review | `TIER_WORKER` |
| Architecture, an ambiguous tradeoff, a tier-2 audit | `TIER_JUDGMENT` — and usually that is you, not a subagent |

`TIER_LOOKUP` starts faster and answers faster for mechanical checks. For everything that has a brief, `TIER_WORKER` is the default: the thinking already happened when you wrote it.

**5. Do not idle.** While a wave runs: write the next brief, draft the plan, or ask the user the clarifying question you were going to ask anyway. The wait is only wasted if you wait.

**6. Verify by sampling, not by redoing.** If checking a result means re-reading everything the subagent read, you paid twice. Two citations spot-checked, the acceptance commands run, the invariants diffed — that is the verification. Reading it all again is not more rigorous; it is the delegation undone.

**7. Use the read-only search agent first.** Every system has a cheap read-only way to search (Claude Code: the built-in `Explore` subagent; Antigravity: a `research`-type subagent; Codex: the built-in `explorer` agent). It reads excerpts rather than whole files and returns conclusions. For "where is / how does / list every" it is faster than a general agent doing the same search. Reach for it first.

What this does not fix: a genuinely serial chain — B needs A's answer, C needs B's — is N round trips no matter what. Recognize those early, and for a short chain in a small codebase, that is the one case where doing the first hop yourself to unblock the wave can be the right call.

