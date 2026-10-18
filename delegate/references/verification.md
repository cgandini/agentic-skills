# Verification — never accept a report

Subagents report confidently and are sometimes wrong. Their report is a claim, not a result.

**Research results:**
- Demand `file:line` citations in the brief's Return section, then spot-check two of them yourself
- "I could not find X" is also a claim — grep for it once before believing it
- Cross-check anything that will drive a decision

**Code results:**
- Read the diff. Not the summary of the diff — the diff.
- Run the acceptance commands yourself. "Tests pass" in a report is a sentence, not a test run.
- Check the invariants you listed: did the export keep its name, did the untouchable file stay untouched (`git diff --stat`)
- Look specifically for what you put in Traps — if you warned about it, check it

**The claim that costs nothing to make and everything to believe: "this was already handled."**

When a subagent reports that the work was unnecessary — *already fixed in commit `abc1234`*, *that
helper already exists*, *the bug isn't reproducible* — it has done no work. So there is no diff to
read and no acceptance command that fails. **Every check above silently passes, because there is
nothing to check.** This is the one report your verification routine cannot catch by running.

It is also the report most worth doubting, because "nothing to do here" is the cheapest possible
answer and nothing in the process pushes back on it.

**One command is enough. Spend it.**

| The claim | The check |
|---|---|
| "already fixed in commit X" | `git log --oneline -S '<the symbol>' -- <file>` — does that commit exist, and did it touch that file? |
| "that already exists" | one `grep` for it |
| "not reproducible" | reproduce it yourself once, or say out loud that you could not |

If the check contradicts the claim, you have just found a bug that would otherwise have shipped
twice: once when it was not fixed, and again when it was reported as fixed.

And when you relay a "no work needed" to the user, **say whether you verified it or are repeating
it**. Those are different sentences and the user cannot tell them apart from your summary.

**Anything flagged in the Return as "I had to decide":** that is the subagent telling you where your brief had a hole. Read those first. They are either fine, or they are the bug.

**Anything flagged as "I saw this and did not touch it":** read those second, and do not file them away unexamined. Two kinds arrive. An *adjacent finding* is free intelligence — decide whether it becomes its own unit, and say so out loud, because the alternative is that it is never mentioned again. A *blast-radius* report is not free: it means the work you are about to merge breaks something outside the diff you reviewed, and no amount of reading that diff would have shown it. Resolve it before the merge, not after.

---


## Integration and Reporting

You are the only one who saw everything. When results come back:

1. Verify each one (above)
2. Resolve conflicts between units — naming drift, duplicated helpers, incompatible assumptions
3. Merge worktrees if used; run the full test suite once on the merged result
4. Tell the user what was done, what was decided along the way, and what was flagged — in your words, not by pasting reports

Relay findings; never forward a subagent's output verbatim as if it were yours. You are accountable for it.

