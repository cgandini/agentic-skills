# Agentic Skills & Protocols

**By Carolina L. Gandini, PhD** — Co-Founder @ [Imagine AI](https://imagineai.space) & Founder @ Padeler  
[LinkedIn](https://www.linkedin.com/in/carolina-gandini/) · [Skills & Recursos (`imagineai.space/recursos/`)](https://imagineai.space/recursos/)

A collection of production-tested, deterministic agentic skills, orchestration patterns, and workflows for **Claude Code**, **Antigravity**, **Cursor**, **VS Code**, and **ChatGPT / Codex**.

---

## EN · Skills Catalog

| Skill | Category | Description | Specification & Guides |
|---|---|---|---|
| **`delegate`** | Orchestration | Judgment vs. Execution pattern: frontier model keeps context lean; cost-effective models execute in parallel worktrees. | [Interactive Guide](https://imagineai.space/recursos/delegate/) · [`SKILL.md`](./delegate/SKILL.md) |
| **`personal-web`** | Personal Brand & Web | Step-by-step guidance to launch a personal brand web + mobile `/admin/` panel on Cloudflare Pages + D1 for USD 0/month. | [Interactive Guide](https://imagineai.space/recursos/personal-web/) · [Template Repo](https://github.com/cgandini/personal-web) · [`SKILL.md`](./personal-web/SKILL.md) |

---

## ES · Catálogo de Skills

| Skill | Categoría | Descripción | Especificación y Guías |
|---|---|---|---|
| **`delegate`** | Orquestación | Patrón Juicio vs. Ejecución: el modelo más potente mantiene el contexto limpio; modelos económicos ejecutan en worktrees paralelos. | [Guía Interactiva](https://imagineai.space/recursos/delegate/) · [`SKILL.md`](./delegate/SKILL.md) |
| **`personal-web`** | Marca Personal y Web | Guía paso a paso para lanzar tu web personal con tu identidad y panel móvil `/admin/` en Cloudflare Pages + D1 por USD 0/mes. | [Guía Interactiva](https://imagineai.space/recursos/personal-web/) · [Plantilla en GitHub](https://github.com/cgandini/personal-web) · [`SKILL.md`](./personal-web/SKILL.md) |

---

## 1. `delegate` — Agentic Orchestration Skill (Judgment vs. Execution)

### EN · Overview & Problem

Most teams adopt AI coding assistants without adapting their orchestration model. In long sessions, the lead agent reads dozens of files, logs, and docs, quickly filling its context window. The consequences are predictable: reasoning degradation, forgotten constraints, hallucinations, and high token churn.

**`delegate`** is a production-tested orchestration skill that enforces a strict separation:

> **Your context is for judgment; subagents' context is for material.**

The orchestrator (running on a frontier reasoning model) stays lean: it formulates architectural decisions, scopes tasks into self-contained 12-point engineering briefs, and fires fast execution subagents in parallel background waves. Subagents read the files, implement the changes, verify against acceptance commands, and report structured summaries back.

### ES · Resumen y Problema

La mayoría de los equipos incorpora asistentes de IA para programar sin cambiar su modelo de orquestación. En sesiones largas, el modelo principal lee docenas de archivos, terminales y logs, saturando su ventana de contexto. El resultado es conocido: degradación del razonamiento, olvido de restricciones, alucinaciones y un costo de tokens disparado en cada turno.

**`delegate`** es una skill probada en producción que impone una regla de oro innegociable:

> **Tu contexto es para el juicio; el de los subagentes es para el material.**

El modelo líder (nivel juicio) permanece liviano: diseña la arquitectura, redacta un Brief de 12 puntos y lanza subagentes de ejecución en paralelo. Los subagentes exploran el código, implementan la solución, ejecutan comandos de aceptación en worktrees aislados y devuelven un reporte estructurado.

> Podés explorar la guía interactiva completa en español con diagramas y tablas en **[imagineai.space/recursos/delegate/](https://imagineai.space/recursos/delegate/)**.

### 3-Tier × 3-System Architecture / Arquitectura Multi-Plataforma

The skill works seamlessly across **Claude Code**, **Antigravity**, and **ChatGPT / Codex**, with model mappings defined in a single configuration block:

| Tier | Role & Responsibility | Claude Code | Antigravity | ChatGPT / Codex |
|---|---|---|---|---|
| **Tier 1 — Judgment (Lead)** | Architecture, brief authoring, edge-case discovery, verification, landing | `fable` (or `opus`) | `pro` | `gpt-6-astra` |
| **Tier 2 — Execution (Worker)** | File edits, running builds, single-phase implementation | `sonnet` | `flash` | `gpt-6.1-sol` |
| **Tier 3 — Consultation (Research)** | Large read queries, codebase search, broad documentation lookup | `haiku` | `flash_lite` | `gpt-6-mini` |

### Key Mechanics / Mecánicas Principales

#### 1. 12-Point Engineering Brief
Every delegated task receives an explicit contract to prevent assumptions:
- **Goal:** Single observable outcome.
- **Context & Decisions:** Architectural choices already finalized.
- **Scope & Out-of-Bounds:** Explicit boundaries of what to touch and what NOT to touch.
- **Mirror:** Subagent reproduces the core requirements in its own words before touching code.
- **Traps:** Known edge cases, pitfalls, or platform footguns.
- **Acceptance Commands:** Exact shell commands that must pass.
- **Invariants:** Business and technical rules that must remain true.
- **Return Deliverable:** Exact expected output format.

#### 2. The 2 Anti-Blindness Questions
Every worker must answer two mandatory questions upon completion:
1. **Adjacent findings:** *What did you discover outside your scope that the lead architect should know?*
2. **Blast radius:** *What existing features, endpoints, or tests could be impacted by this change?*

#### 3. Writer Isolation via Git Worktrees
Parallel subagents never write to the same branch. Each worker runs in an isolated worktree (`.worktrees/<plan>--<unit>`), keeping `main` pristine and avoiding concurrency collisions.

#### 4. Risk-Based Audit Tiers
- **Tier 0 (Fast Self-Check):** Low risk (docs, copy, comments).
- **Tier 1 (Automated Acceptance):** Medium risk (isolated components, UI bugfixes).
- **Tier 2 (Adversarial Review):** High risk (auth, migrations, financial logic, public API contracts) audited by an independent reviewer agent.

### Installation / Instalación

```bash
git clone https://github.com/cgandini/agentic-skills.git

# Claude Code
mkdir -p ~/.claude/skills/delegate
cp -R agentic-skills/delegate/* ~/.claude/skills/delegate/

# Antigravity / Gemini CLI
mkdir -p ~/.gemini/config/skills/delegate
cp -R agentic-skills/delegate/* ~/.gemini/config/skills/delegate/

# ChatGPT / Codex
mkdir -p ~/.codex/skills/delegate
cp -R agentic-skills/delegate/* ~/.codex/skills/delegate/
```

Direct raw fetch:
```bash
curl -sO https://imagineai.space/recursos/delegate/SKILL.md
```

---

## 2. `personal-web` — Branded Personal Web & Mobile Admin Panel

### EN · Overview & Purpose

Most creators and independent professionals rely on generic link-in-bio services that look identical, charge monthly subscriptions for basic customizations, or require technical knowledge to update.

**`personal-web`** turns any AI assistant (in browser chat, agentic IDEs, or terminal) into a patient, step-by-step guide that helps anyone—regardless of technical background—build a custom personal brand website matching their identity, backed by a private mobile `/admin/` panel and click analytics on Cloudflare Pages + D1 for USD 0/month.

Key elements:
- **Zero code required:** Works in browser chats (claude.ai, ChatGPT, Gemini) with public link fetching or `FOR-CHAT.md`, in agentic IDEs (Antigravity, Cursor, VS Code), or in terminal CLIs (Claude Code, Antigravity, Codex) with `SKILL.md`.
- **5 Structured Phases:** Design System extraction from Instagram/web, Content & Block hierarchy, Brand JSON generation (`brand/{theme,seed,examples}.json`), Cloudflare Pages + D1 setup, and Daily mobile administration.
- **Cost USD 0/month:** Fully runs on Cloudflare's free tiers with edge HTML for instant loading (<100ms), D1 SQLite persistence, and zero tracking cookies.
- **Template Repository:** [github.com/cgandini/personal-web](https://github.com/cgandini/personal-web)
- **Interactive Guide & Downloads:** [imagineai.space/recursos/personal-web/](https://imagineai.space/recursos/personal-web/)

### ES · Resumen y Propósito

La mayoría de los creadores y profesionales usan servicios genéricos de enlaces que se ven todos iguales, cobran mensualidades por funciones básicas o requieren editar código a mano cada vez que se quiere actualizar una foto o un enlace.

**`personal-web`** transforma a cualquier asistente de IA en una guía que te acompaña paso a paso (sin conocimientos técnicos de terminal, GitHub ni Cloudflare) a tener tu propia web personal con tu identidad de marca, panel privado `/admin/` en el celular y analíticas de clics en Cloudflare Pages + D1 por USD 0/mes.

- **5 Fases Deterministas:** Sistema de diseño desde Instagram o tu web, contenido y jerarquía de bloques, archivos de marca (`brand/{theme,seed,examples}.json`), instalación en Cloudflare y uso diario desde el teléfono.
- **Tres caminos de ejecución:**
  1. **Camino A (Chat web sin instalar nada):** claude.ai, ChatGPT o Gemini con el prompt de inicio o adjuntando `FOR-CHAT.md`.
  2. **Camino B (IDE con agentes):** Google Antigravity, Cursor o VS Code con Claude Code o Codex trabajando directo en el repositorio.
  3. **Camino C (Agentes en terminal):** Claude Code CLI, Antigravity CLI o Codex CLI clonando la plantilla y ejecutando con `SKILL.md`.
- **Plantilla pública:** [github.com/cgandini/personal-web](https://github.com/cgandini/personal-web)

### Usage & Installation / Uso e Instalación

#### 1. Browser Chat (Zero Local Software) / Chat Web (Sin Instalar Nada)
Copy the kickoff prompt from [imagineai.space/recursos/personal-web/CHAT-PROMPT.md](https://imagineai.space/recursos/personal-web/CHAT-PROMPT.md) and paste it into claude.ai, gemini.google.com, or chatgpt.com.
If your chat assistant does not fetch external web links, download and attach [`FOR-CHAT.md`](./personal-web/FOR-CHAT.md).

#### 2. Agentic IDEs (Antigravity, Cursor, VS Code + Claude Code / Codex) / IDE con Agentes
Clone your copy of `https://github.com/cgandini/personal-web` inside your IDE:
- **Google Antigravity:** Open the cloned workspace and prompt the agent: *"I want to build my personal web using https://github.com/cgandini/personal-web and the personal-web skill. Guide me step by step."* (To install the skill permanently: `cp -R personal-web ~/.agents/skills/personal-web`).
- **VS Code or Cursor:** Install the **Claude Code** or **Codex** extension, open your cloned personal-web folder, and ask the assistant in the side panel to guide you through Phase 1.

#### 3. Terminal & CLI / Terminal y CLI
```bash
git clone https://github.com/cgandini/agentic-skills.git

# Claude Code
mkdir -p ~/.claude/skills/personal-web
cp -R agentic-skills/personal-web/* ~/.claude/skills/personal-web/

# Antigravity / Gemini CLI
mkdir -p ~/.gemini/config/skills/personal-web
cp -R agentic-skills/personal-web/* ~/.gemini/config/skills/personal-web/

# ChatGPT / Codex
mkdir -p ~/.codex/skills/personal-web
cp -R agentic-skills/personal-web/* ~/.codex/skills/personal-web/

# Clone personal-web template
gh repo create mi-web --template cgandini/personal-web --private --clone
```

Direct raw fetch:
```bash
curl -sO https://imagineai.space/recursos/personal-web/SKILL.md
curl -sO https://imagineai.space/recursos/personal-web/FOR-CHAT.md
curl -sO https://imagineai.space/recursos/personal-web/CHAT-PROMPT.md
```

---

## Repository Structure / Estructura del Repositorio

```
agentic-skills/
├── LICENSE                    # MIT License
├── README.md                  # This documentation
├── delegate/
│   ├── SKILL.md               # Main skill specification & configuration block
│   └── references/            # Deep-dive operational guides
│       ├── audit.md           # Audit tier specifications & pass bars
│       ├── context.md         # Context budgeting & compaction guidelines
│       ├── dimensions.md      # The 6 evaluation dimensions
│       ├── landing.md         # Verified-landing protocols
│       ├── latency.md         # Parallel background execution patterns
│       ├── plans.md           # Plan state persistence on disk
│       ├── platforms.md       # Platform-specific tool mapping
│       ├── subagent.md        # Worker prompt template & contract
│       ├── verification.md    # Acceptance command criteria
│       └── worktrees.md       # Git worktree lifecycle management
└── personal-web/
    ├── SKILL.md               # Main skill specification
    ├── FOR-CHAT.md            # All-in-one bundle for browser chats
    ├── CHAT-PROMPT.md         # Bilingual kickoff prompt (ES/EN)
    ├── prompts/               # Standalone prompt recipes (1..3)
    │   ├── 1-design-system.md
    │   ├── 2-static-page.md
    │   └── 3-install.md
    ├── references/            # Step-by-step guides (1..6)
    │   ├── 1-design-system.md
    │   ├── 2-content-and-blocks.md
    │   ├── 3-brand-files.md
    │   ├── 4-install-with-agent.md
    │   ├── 5-install-from-browser.md
    │   └── 6-daily-use.md
    └── examples/              # Fictional brand reference
        └── sample-brand/
            ├── README.md
            ├── design-system.md
            ├── theme.json
            ├── seed.json
            └── examples.json
```

---

## License

Released under the [MIT License](./LICENSE).  
Copyright (c) 2026 Carolina L. Gandini — [Imagine AI](https://imagineai.space).
