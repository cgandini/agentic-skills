# Phase 2: Content and Blocks

**Goal:** Determine which blocks the page will contain, their priority sequence, and the exact copy. A personal web is not an uncurated directory: it is a structured journey where **the single most important offer comes first**.

**Deliverable:** A prioritized block table approved by the user. Do not generate JSON files yet: JSON generation belongs to Phase 3.

Reference limits and schemas: `docs/BLOCKS.md` and `packages/core/src/limits.js`. Standalone prompt: `prompts/2-static-page.md`.

## Step 1: The Core Question

Ask and wait for the response:

> If someone visits your page and can take only one single action, what do you want that to be?

The answer forms the `destacado` hero block. Next, gather the remaining links: what each destination offers and its destination URL. **All URLs must be provided by the user; never invent links or use placeholder domains on a production site.**

## Step 2: Block Selection

| Content Type | Block Type | Rationale |
|---|---|---|
| Primary offer (1-on-1 session, flagship program, booking, lead product) | `destacado` | Dark card with prominent button. **Use exactly once, at the very top.** |
| High-value secondary action (newsletter, free guide, community) | `tarjeta` | Headline, copy, and button. Can highlight a substring of the title. |
| Single-line destination (WhatsApp channel, podcast, speaking, contact, main site) | `fila` | Icon, title, and short subtitle. |
| Vertical cover media (books, audio courses, guides, episodes) | `libros` | Cover gallery with up to 3 groups. |
| Social channels | `redes` | Circular social icons, up to 8. **Placed last**, right above footer. |

Decision Rules:
- **Two competing "primary" offers:** Assign one to `destacado` and the other to `tarjeta`. Ask which drives greater impact or revenue. Never place two `destacado` blocks.
- **More than 7 or 8 items:** Recommend pruning or grouping into rows. Fewer choices increase conversions (technical limit is 40 blocks).
- **Seasonal or time-limited offers:** Set `hidden: true` in seed data so the user can easily toggle it visible from `/admin/` when active.
- **Multiple audiences:** Build one clear page per audience. The template supports a single curated flow per deployment.

## Step 3: Vertical Hierarchy

Standard visual order:

1. Profile (photo, name, role, hook phrase).
2. `destacado`: Flagship call to action.
3. `tarjeta`: High-value secondary offer.
4. `fila`: Row links ordered by priority (limit 3 to 4 consecutive rows).
5. `libros`: Publications or cover-based media.
6. `redes`: Social icon row.
7. Footer.

Explain proposed reordering in one concise sentence and let the user decide.

## Step 4: Copywriting Rules

Write in the voice established in `design-system.md`:

- **Action-oriented buttons:** "Schedule your session", "Get the guide", "Read on Substack". Avoid passive labels like "Click here".
- **Benefit-driven copy:** The headline states what it is; the body text clarifies what the visitor gains.
- **`label`:** Uppercase category tag in 1 to 3 words ("1-on-1 Session", "Newsletter").
- **`proof`:** Social proof line with checkmark on `destacado`. Include only if backed by real, verified facts. If no proof metric exists, omit `proof`.
- **`highlight`:** In `tarjeta` and `profile`, the highlight must be an **exact substring** of the title or phrase (identical characters, casing, and accents). If it does not match character-for-character, no highlight renders. Choose 1 to 3 words.
- **`verified`:** Boolean in `fila`. Set to `true` only for verified channels (e.g. verified WhatsApp channels).
- **`style`:** In `fila`, `"solido"` for high-priority rows (white surface, icon in accent disc), `"borde"` for subtle destinations (transparent, outline only).
- **Icons:** Pick exact identifiers from the template icon library (see `references/3-brand-files.md`).
- **Zero emojis:** Never insert emojis into copy or JSON.

## Step 5: Profile Section

| Field | Description |
|---|---|
| `photo` | User portrait (square or circular 96 px). Uses `/img/perfil` placeholder for install; user uploads real photo via `/admin/`. |
| `name` | Name rendered in uppercase heading font. |
| `role` | Role and focus in one line: "Clinical Nutritionist · Mindful Eating". |
| `phrase` & `highlight` | Short personal hook with the exact substring to highlight. |
| `sub` | Clarifying sentence describing what they do and who they serve. |

## Step 6: Specialized Block Parameters

- **`libros`:** Each group contains a title and a `layout` (`"destacado"` for a single large featured cover, or `"fila"` for a 3-column row of up to 3 covers). Uses `/img/tapa` placeholder during installation. Covers display in 2:3 vertical proportion.
- **`redes`:** Email links use `mailto:hello@...`. WhatsApp links use `https://wa.me/<country-code><number>` without `+` or spaces.
- **Phone:** `tel:+...` is supported in `fila`.

## Step 7: Approval and Sign-off

Present the summary table and ask for direct confirmation ("Shall we approve this structure?"). Once confirmed, output the resume block from `SKILL.md`.

```
| # | Block Type | Title | Destination URL | Notes |
|---|---|---|---|---|
| 1 | destacado | Welcome Session | https://... | label, body, proof line |
| 2 | tarjeta | Newsletter | https://... | highlight: "..." |
| 3 | fila (solido) | Community Chat | https://... | icon: whatsapp |
| 4 | fila (borde) | Podcast | https://... | verified: false |
| 5 | libros | Guides | https://... | N groups (covers uploaded later in panel) |
| 6 | redes | Social Links | ... | placed last |
Profile: Name / Role / Phrase (highlight: "...") / Sub
Footer: "Hecha con la plantilla gratis de imagineAI" (or custom text)
```
