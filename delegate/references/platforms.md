# Calling a subagent on each system

Use the subsection for the active `SYSTEM` (set in SKILL.md). In every example the model is a tier from the Configuration table.


Use the subsection for the active `SYSTEM`. In every example the model is a tier from the Configuration table.

### Claude Code

- **Per call:** the subagent tool (`Agent`) takes a `model` parameter: `sonnet`, `opus`, `haiku`, `fable`, a full model ID, or `inherit`.
- **Persistent definitions:** a Markdown file in `.claude/agents/` (project) or `~/.claude/agents/` (personal), with `name`, `description` and `model` in the frontmatter.
- **Which model wins** (v2.1.251 and later): the per-call `model`, then the definition's `model`, then the `CLAUDE_CODE_SUBAGENT_MODEL` environment variable, then the main conversation's model. An alias that names the same family as your main model runs on your main model's exact version.
- **Read-only search:** the built-in `Explore` subagent. A subagent you define yourself with the name `Explore` and `model: haiku` replaces it, which keeps exploration cheap.
- **Background and worktrees:** subagents can run in the background; `isolation: "worktree"` gives a writer its own worktree (random name — see Worktrees for the named form).
- **Check what actually ran:** `/tasks` shows the model of each subagent.

```
Agent(
  model: "sonnet"                 # TIER_WORKER
  prompt: <the brief>
  description: "<3-5 words>"
  run_in_background: true
)
```

### Antigravity

- **Per call:** `invoke_subagent` takes a list of subagents; each has a `TypeName`, a `Role`, a `Prompt` (the brief) and a `Model`: `pro`, `flash`, `flash_lite` or `inherit` (`inherit` = the same model as your main session).
- **Parallel by default:** several subagents in one call run at the same time in the background, and you are notified when each one reports. Do not poll.
- **Read-only search:** use the `research` type. Writers use `self`.
- **Workspace:** `inherit` (shared with you), `share` (shared repository, independent branch) or `branch` (isolated copy). Writers should never use `inherit` when another writer is active.
- **Reusable roles:** `define_subagent` creates a named role once; `send_message` talks to a subagent that is still alive.
- **You choose a tier, not a version.** Antigravity decides which concrete model `flash` or `pro` is today.

```
invoke_subagent(
  Subagents: [{
    TypeName: "self",
    Role: "<2-5 word job title>",
    Model: "flash",               # TIER_WORKER
    Workspace: "branch",
    Prompt: "<the brief>"
  }]
)
```

### ChatGPT / Codex

- **Subagents only start when you ask.** Say it in the prompt: "spawn two agents", "delegate this in parallel". Multi-agent support must be enabled in your Codex configuration.
- **Model per call:** name the model (and optionally the reasoning effort) in the same prompt. An explicit spawn value overrides the defaults below.
- **Defaults:** in `config.toml`, `[agents]` accepts `default_subagent_model`, `default_subagent_reasoning_effort` and `max_concurrent_threads_per_session`. With nothing set, a subagent inherits its parent's model and effort.
- **Custom agents:** one TOML file each, in `.codex/agents/` (project) or `~/.codex/agents/` (personal). Required fields: `name`, `description`, `developer_instructions`. Optional: `model`, `model_reasoning_effort`. A value set in the file wins over everything else. Sandbox, approvals, provider and MCP servers are inherited from the parent and cannot be overridden there.
- **Built-in agents:** `default`, `worker` (implementation and fixes) and `explorer` (read-only search).
- **Reasoning effort:** start at `high` for `gpt-6-luna`; for `gpt-6.1-sol`, use an effort your client supports and raise it only for demanding work.

```
Spawn one agent on gpt-6.1-sol to implement the brief below,
and wait for it. <the brief>
```

A `TIER_LOOKUP` agent as a file, `.codex/agents/lookup.toml`:

```toml
name = "lookup"
description = "Fast, narrow lookups: where is X, does Y exist, how many Z."
model = "gpt-6-luna"
model_reasoning_effort = "high"
developer_instructions = """
Answer only the question asked. Cite file:line. Do not edit files.
If the answer is not in the code, say so and stop.
"""
```

---

## What to know about subagents (any system)

- **They start with nothing.** No conversation, no memory of what you discussed. Everything they need is in the prompt or on disk.
- **Their report comes back to you, not to the user.** You relay what matters.
- **Read-only search agents locate; they do not audit.** Use them for "where is X", "how does Y work", "list every Z".
- **Background by default.** Fire it, keep orchestrating, get notified. Wait for a result only when your very next action needs it and nothing else could happen meanwhile.
- **Parallel writers collide.** Two agents editing the same tree at once will overwrite each other. Every writer gets its own worktree, created and named by you — see the Worktrees section.
- **Pick the tier by what the work is** — see Model economy and the table under Latency.

---

