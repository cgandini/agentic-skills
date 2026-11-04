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

### MiniMax Code

- **Per call:** the subagent tool is `task`. It takes `description`, `prompt`, `agent_name`, and optionally `model`, `effort` and `run_in_background`.
- **Always pass `model`.** Omitted, the subagent inherits `MiniMax-M3` and nothing runs on the cheaper tier. The tool's own description says to set `model` only when the user names one and never to choose one. The tier table in this skill is that choice, made by the user: treat it as naming the model on every call. The value is a source-qualified key, such as `minimax/MiniMax-M3.1-Flash`.
- **`MiniMax-M3.1-Flash` also needs `effort`.** With `model` and no `effort`, the call fails with "requires an explicit thinking effort". Accepted values: `default`, `low`, `medium`, `high`, `xhigh`, `max`. Pass `default` unless the brief says otherwise.
- **Check what actually ran** on the first subagent of the session: the `"model"` values in `messages.jsonl`, in that child's folder under `~/.minimax/v2/sessions/`. The `task` result gives its `session_id`. If they say `MiniMax-M3`, stop and tell the user: every tier is running on `MiniMax-M3`.
- **`model_verdict: missing` says nothing about the model.** That field holds a verdict parsed from the child's reply text, and `missing` is normal when there is none.
- **A file cannot pin the model.** In a plugin agent's frontmatter `model` is always ignored, and so are `isolation` and `background`. Only the `task` call sets the model.
- **Roles:** `agent_name` takes `worker` (implementation), `explore` (read-only search), `verifier` (validates, changes no project files: use it for audits) or `mavis` (mixed work).
- **Parallel means background.** `task` calls run one at a time in the foreground, so use `run_in_background: true` for a wave. There is a concurrency limit; its value is not documented.
- **Completion:** each call returns a `task_id`. A `<background-task-finished>` event wakes you; read the result with `task_output`. Do not poll. `task_append` sends follow-up work to a child that keeps its context, and `task_stop` ends one.
- **No worktree per subagent.** Create the named worktree yourself and put its path in the brief, as a hard rule: work only inside this path.
- **Reasoning:** `MiniMax-M3` starts with thinking off through the API, and its `effort` takes `on` or `off`. Use `on` for a tier-2 audit. `MiniMax-M3.1-Flash` always thinks.
- **Instructions:** MiniMax Code reads `AGENTS.md`, not `CLAUDE.md`. A rule that tells the session to load this skill must also live there.
- **Skills:** found in `.minimax/skills`, `.claude/skills` and `.agents/skills` (walking up from the workspace), and in `~/.claude/skills`, `~/.codex/skills` and `~/.agents/skills`.

```
task(
  description: "<3-5 words>",
  agent_name: "worker",
  model: "minimax/MiniMax-M3.1-Flash",   # TIER_WORKER
  effort: "default",
  prompt: "<the brief>",
  run_in_background: true
)
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

