# Context — what enters, and what survives

Context is paid on **every turn**, not once. A file read at turn 3 is re-sent at turns 4, 5, 6 — until compaction. A 20k-token file dump read early costs 20k tokens times every remaining turn. That is why delegation is a context strategy before it is a cost strategy: the subagent pays for the file once, and it dies with them.

Three levers, in order of size.

### 1. Keep it out — the biggest lever

- **Never read a whole file to answer a question about part of it.** `Read` with `offset`/`limit`, or delegate the question.
- **Never let raw tool output land in context when a summary would do.** `grep -c` instead of `grep`. `| tail -20` on a build log. `--reporter=dot` on a test run, then the failures only. `--json | jq '.summary'` where a tool offers it.
- **Never paste a subagent's report verbatim.** Extract, relay. The report was written for you, not for the user.
- **The RETURN line of every brief is a context budget.** "<=200 words", "a table with these three columns", "file:line list, nothing else". A brief without a RETURN shape gets back an essay.
- **Do not re-read what you already read.** If you need it again, the part you needed should have been written down the first time.

### 2. Make it survive — what makes compaction safe

Compaction is lossy and it will happen. What survives is what is on disk.

- **Decisions, constraints, and the current plan go to a file the moment they are made** — `plan.md` and the `-decisions.md` log in the plan folder (see Plans on disk) — not only the conversation. A constraint that lives only in turn 12 does not exist after compaction.
- **Before a long implementation phase, write the state:** what is done, what is next, what was decided and why. After compaction, read that file instead of trusting the summary.
- **Briefs for big tasks go to disk** as `YYYY-MM-DD-<topic>-brief-<unit>.md` in the plan folder. Reviewable, reusable across compactions, and the next wave can reference them by path instead of restating them.

### 3. Compact on purpose — the smallest lever, but the one that keeps a long session usable

- **Automatic compaction triggers when context is nearly full** — the worst possible moment: mid-task, no chance to write state first, and the summary decides what your constraints were.
- **Compact at milestones instead:** after a phase merges, after research is integrated, before starting an independent unit. `/compact` in Claude Code, `/compress` in Gemini CLI.
- **Right before compacting, write state to disk. Right after, re-read the plan and decisions files.** Do not assume the summary kept your invariants.
- **Steer the summary.** `/compact` accepts focus instructions — "keep the decisions, the file list, and the acceptance criteria; drop the exploration." Say what matters, or the summarizer guesses.

The trap: treating compaction as the fix. It is cleanup after the damage. The lever is upstream — what you let in, and what you wrote down before it was lost.

