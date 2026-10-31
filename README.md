# Agentic Skills & Protocols

**By Carolina L. Gandini, PhD** — Co-Founder @ [Imagine AI](https://imagineai.space) & Founder @ Padeler  
[LinkedIn](https://www.linkedin.com/in/carolina-gandini/) · [Skills & Recursos (`imagineai.space/recursos/`)](https://imagineai.space/recursos/)

A collection of production-tested, deterministic agentic skills, orchestration patterns, and workflows for **Claude Code**, **Antigravity**, and **ChatGPT / Codex**.

---

## Skills Catalog

| Skill | Category | Description | Specification & Guides |
|---|---|---|---|
| **`delegate`** | Orchestration | Judgment vs. Execution pattern: frontier model keeps context lean; cost-effective models execute in parallel worktrees. | [Interactive Guide](https://imagineai.space/recursos/delegate/) · [`SKILL.md`](./delegate/SKILL.md) |
| **`pagina-de-links`** | Personal Brand & Web | Step-by-step guidance to launch a branded link-in-bio page + mobile `/admin/` panel on Cloudflare Pages + D1 for USD 0/month. | [Interactive Guide](https://imagineai.space/recursos/pagina-de-links/) · [Template Repo](https://github.com/cgandini/tu-pagina-de-links) · [`SKILL.md`](./pagina-de-links/SKILL.md) |

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

## 2. `pagina-de-links` — Branded Link-in-Bio & Mobile Admin Panel

### EN · Overview & Problem

Most creators and independent professionals rely on generic link-in-bio services that look identical, charge monthly subscriptions for basic customizations, or require technical knowledge to update.

**`pagina-de-links`** turns any AI assistant (in browser chat or terminal) into a patient, step-by-step guide that helps anyone—regardless of technical background—build a custom link-in-bio page matching their personal brand, backed by a private mobile `/admin/` panel and click analytics on Cloudflare Pages + D1 for USD 0/month.

Key elements:
- **Zero code required:** Works in browser chats (claude.ai, ChatGPT, Gemini) with `PARA-CHAT.md` or in terminal agents (Claude Code, Antigravity, Codex) with `SKILL.md`.
- **5 Structured Phases:** Design System extraction from Instagram/web, Content & Block hierarchy, Brand JSON generation, Cloudflare Pages + D1 setup, and Daily mobile administration.
- **Cost USD 0/month:** Fully runs on Cloudflare's free tiers with edge HTML for instant loading (<100ms) and zero tracking cookies.
- **Template Repository:** [github.com/cgandini/tu-pagina-de-links](https://github.com/cgandini/tu-pagina-de-links)
- **Interactive Guide & Downloads:** [imagineai.space/recursos/pagina-de-links/](https://imagineai.space/recursos/pagina-de-links/)

### ES · Resumen y Propósito

La mayoría de los creadores y profesionales usan servicios genéricos de enlaces que se ven todos iguales, cobran mensualidades por funciones básicas o requieren editar código a mano cada vez que se quiere actualizar una foto o enlace.

**`pagina-de-links`** transforma a cualquier asistente de IA en una guía que acompaña paso a paso a cualquier persona (sin conocimientos técnicos de terminal, GitHub ni Cloudflare) a tener su propia página de links con su marca, panel privado `/admin/` en el celular y métricas de clics en Cloudflare Pages + D1 por USD 0/mes.

- **5 Fases Deterministas:** Sistema de diseño desde Instagram, contenido por jerarquía de conversión, archivos de marca (`brand/{theme,seed,examples}.json`), instalación en Cloudflare y uso diario desde el teléfono.
- **Dos caminos de ejecución:**
  - **Ruta A (Agentes en terminal):** Claude Code, Antigravity o Codex con `SKILL.md` + plantilla pública `cgandini/tu-pagina-de-links`.
  - **Ruta B (Solo chat en navegador):** claude.ai, ChatGPT o Gemini adjuntando `PARA-CHAT.md` y pegando `PROMPT-PARA-CHAT.md`.
- **Plantilla pública:** [github.com/cgandini/tu-pagina-de-links](https://github.com/cgandini/tu-pagina-de-links)

### Installation / Instalación

```bash
git clone https://github.com/cgandini/agentic-skills.git

# Claude Code
mkdir -p ~/.claude/skills/pagina-de-links
cp -R agentic-skills/pagina-de-links/* ~/.claude/skills/pagina-de-links/

# Antigravity / Gemini CLI
mkdir -p ~/.gemini/config/skills/pagina-de-links
cp -R agentic-skills/pagina-de-links/* ~/.gemini/config/skills/pagina-de-links/

# ChatGPT / Codex
mkdir -p ~/.codex/skills/pagina-de-links
cp -R agentic-skills/pagina-de-links/* ~/.codex/skills/pagina-de-links/
```

Direct raw fetch:
```bash
curl -sO https://imagineai.space/recursos/pagina-de-links/SKILL.md
curl -sO https://imagineai.space/recursos/pagina-de-links/PARA-CHAT.md
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
└── pagina-de-links/
    ├── SKILL.md               # Main skill specification
    ├── PARA-CHAT.md           # All-in-one bundle for browser chats
    ├── PROMPT-PARA-CHAT.md    # Kickoff prompt for browser chats
    ├── prompts/               # Standalone prompt recipes (1..3)
    │   ├── 1-sistema-de-diseno.md
    │   ├── 2-pagina-de-links.md
    │   └── 3-instalar.md
    └── references/            # Step-by-step guides (1..6)
        ├── 1-sistema-de-diseno.md
        ├── 2-contenido-y-bloques.md
        ├── 3-archivos-de-marca.md
        ├── 4-instalar-con-terminal.md
        ├── 5-instalar-sin-terminal.md
        └── 6-uso-diario.md
```

---

## License

Released under the [MIT License](./LICENSE).  
Copyright (c) 2026 Carolina L. Gandini — [Imagine AI](https://imagineai.space).
