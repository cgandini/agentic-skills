# `delegate` — Agentic Orchestration Skill (Judgment vs. Execution)

**By Carolina L. Gandini, PhD** — Co-Founder @ [Imagine AI](https://imagineai.space) & Founder @ Padeler  
[LinkedIn](https://www.linkedin.com/in/carolina-gandini/) · [Interactive Guide in Spanish (`imagineai.space/recursos/delegate/`)](https://imagineai.space/recursos/delegate/) · [Raw Specification (`SKILL.md`)](https://imagineai.space/recursos/delegate/SKILL.md)

---

## EN · Overview & Problem

Most teams adopt AI coding assistants without adapting their orchestration model. In long sessions, the lead agent reads dozens of files, logs, and docs, quickly filling its context window. The consequences are predictable: reasoning degradation, forgotten constraints, hallucinations, and high token churn.

**`delegate`** is a production-tested orchestration skill that enforces a strict separation:

> **Your context is for judgment; subagents' context is for material.**

The orchestrator (running on a frontier reasoning model) stays lean: it formulates architectural decisions, scopes tasks into self-contained 12-point engineering briefs, and fires fast execution subagents in parallel background waves. Subagents read the files, implement the changes, verify against acceptance commands, and report structured summaries back.

---

## ES · Resumen y Problema

La mayoría de los equipos incorpora asistentes de IA para programar sin cambiar su modelo de orquestación. En sesiones largas, el modelo principal lee docenas de archivos, terminales y logs, saturando su ventana de contexto. El resultado es conocido: degradación del razonamiento, olvido de restricciones, alucinaciones y un costo de tokens disparado en cada turno.

**`delegate`** es una skill probada en producción que impone una regla de oro innegociable:

> **Tu contexto es para el juicio; el de los subagentes es para el material.**

El modelo líder (nivel juicio) permanece liviano: diseña la arquitectura, redacta un Brief de 12 puntos y lanza subagentes de ejecución en paralelo. Los subagentes exploran el código, implementan la solución, ejecutan comandos de aceptación en worktrees aislados y devuelven un reporte estructurado.

> Podés explorar la guía interactiva completa en español con diagramas y tablas en **[imagineai.space/recursos/delegate/](https://imagineai.space/recursos/delegate/)**.

---

## 3-Tier × 3-System Architecture / Arquitectura Multi-Plataforma

The skill works seamlessly across **Claude Code**, **Antigravity**, and **ChatGPT / Codex**, with model mappings defined in a single configuration block:

| Tier | Role & Responsibility | Claude Code | Antigravity | ChatGPT / Codex |
|---|---|---|---|---|
| **Tier 1 — Judgment (Lead)** | Architecture, brief authoring, edge-case discovery, verification, landing | `fable` (or `opus`) | `pro` | `gpt-6-astra` |
| **Tier 2 — Execution (Worker)** | File edits, running builds, single-phase implementation | `sonnet` | `flash` | `gpt-6.1-sol` |
| **Tier 3 — Consultation (Research)** | Large read queries, codebase search, broad documentation lookup | `haiku` | `flash_lite` | `gpt-6-mini` |

---

## Key Mechanics / Mecánicas Principales

### 1. 12-Point Engineering Brief
Every delegated task receives an explicit contract to prevent assumptions:
- **Goal:** Single observable outcome.
- **Context & Decisions:** Architectural choices already finalized.
- **Scope & Out-of-Bounds:** Explicit boundaries of what to touch and what NOT to touch.
- **Mirror:** Subagent reproduces the core requirements in its own words before touching code.
- **Traps:** Known edge cases, pitfalls, or platform footguns.
- **Acceptance Commands:** Exact shell commands that must pass.
- **Invariants:** Business and technical rules that must remain true.
- **Return Deliverable:** Exact expected output format.

### 2. The 2 Anti-Blindness Questions
Every worker must answer two mandatory questions upon completion:
1. **Adjacent findings:** *What did you discover outside your scope that the lead architect should know?*
2. **Blast radius:** *What existing features, endpoints, or tests could be impacted by this change?*

### 3. Writer Isolation via Git Worktrees
Parallel subagents never write to the same branch. Each worker runs in an isolated worktree (`.worktrees/<plan>--<unit>`), keeping `main` pristine and avoiding concurrency collisions.

### 4. Risk-Based Audit Tiers
- **Tier 0 (Fast Self-Check):** Low risk (docs, copy, comments).
- **Tier 1 (Automated Acceptance):** Medium risk (isolated components, UI bugfixes).
- **Tier 2 (Adversarial Review):** High risk (auth, migrations, financial logic, public API contracts) audited by an independent reviewer agent.

---

## Installation / Instalación

### Claude Code
```bash
git clone https://github.com/cgandini/agentic-skills.git
mkdir -p ~/.claude/skills/delegate
cp -R agentic-skills/delegate/* ~/.claude/skills/delegate/
```

### Antigravity / Gemini CLI
```bash
git clone https://github.com/cgandini/agentic-skills.git
mkdir -p ~/.gemini/config/skills/delegate
cp -R agentic-skills/delegate/* ~/.gemini/config/skills/delegate/
```

### ChatGPT / Codex
```bash
git clone https://github.com/cgandini/agentic-skills.git
mkdir -p ~/.codex/skills/delegate
cp -R agentic-skills/delegate/* ~/.codex/skills/delegate/
```

### Direct Raw Fetch
You can also download the raw `SKILL.md` specification directly:
```bash
curl -sO https://imagineai.space/recursos/delegate/SKILL.md
```

---

## Repository Structure / Estructura del Repositorio

```
agentic-skills/
├── LICENSE                    # MIT License
├── README.md                  # This documentation
└── delegate/
    ├── SKILL.md               # Main skill specification & configuration block
    └── references/            # Deep-dive operational guides
        ├── audit.md           # Audit tier specifications & pass bars
        ├── context.md         # Context budgeting & compaction guidelines
        ├── dimensions.md      # The 6 evaluation dimensions
        ├── landing.md         # Verified-landing protocols
        ├── latency.md         # Parallel background execution patterns
        ├── plans.md           # Plan state persistence on disk
        ├── platforms.md       # Platform-specific tool mapping
        ├── subagent.md        # Worker prompt template & contract
        ├── verification.md    # Acceptance command criteria
        └── worktrees.md       # Git worktree lifecycle management
```

---

## License

Released under the [MIT License](./LICENSE).  
Copyright (c) 2026 Carolina L. Gandini — [Imagine AI](https://imagineai.space).
