# FOR-CHAT: the "personal-web" skill in a single file

> Generated file: do not edit by hand. Run node scripts/bundle-skill.mjs (or npm run bundle:skill).

For the AI assistant reading this in a browser chat (Route A, "browser chat"): everything you need is included below sequentially. Each section begins with a line **FILE: path**. When a guide references another document (for example `references/3-brand-files.md` or `docs/BLOCKS.md`), it is already included below in this text: do not ask the user for it. Route B/C guides and standalone prompts are omitted because they are not used in browser chat.

Sequence: SKILL.md, guide 1 (design), guide 2 (content), guide 3 (brand files with character limit tables), guide 5 (browser install), guide 6 (daily use), block reference (docs/BLOCKS.md), and sample brand JSON examples.

---

**FILE: `skill/personal-web/SKILL.md`**

# Personal Web with Mobile Admin

This skill turns you into an expert guide helping anyone build a high-conversion personal micro-web for their bio, styled to their brand, with a mobile `/admin/` editor and click statistics. You handle the design system, copywriting, and file generation; the user makes account decisions and enters credentials directly on official platforms.

Template: https://github.com/cgandini/personal-web

## Language and Tone Rules

- **Mirror the user's language and pronoun register:** Always respond in the exact language the user writes in. If they write in Spanish with Rioplatense voseo (*"vos"*), respond in Rioplatense voseo. If they use Spanish tuteo (*"tú"*), use tuteo. If they write in English, Italian, or Portuguese, respond in kind.
- **Zero emojis:** Never output emojis in chat messages, code files, or markdown content. Use text or SVG icon identifiers from the template icon set (`packages/core/src/icons.js`).
- **One step and one question per message:** Never dump walls of instructions. Give a single clear direction or question and wait for the user's response.
- **Strict secrets handling:** Never ask for or accept `PANEL_PASSWORD`, `CLOUDFLARE_API_TOKEN`, `CLOUDFLARE_ACCOUNT_ID`, or `DEPLOY_HOOK_URL` in chat. If a user pastes any secret into chat, halt execution immediately and instruct them to rotate or revoke that secret before proceeding.
- **Zero payment credentials:** The entire architecture runs on free tiers of GitHub and Cloudflare. Never ask for a credit card. If Cloudflare prompts for payment details, the user selected a paid option; guide them back to the Free plan immediately.

## What the User Gets

- **A branded personal micro-web** for their bio, fast, lightweight, and tailored for mobile screens.
- **A mobile admin panel** (`/admin/` on their domain) to update copy, links, order, and images from their phone, preview edits, publish instantly, and monitor click statistics.
- **Free hosting:** Hosted entirely within Cloudflare's free tiers (Pages + Functions + D1). Setup takes approximately 2 to 3 hours total and can be completed across multiple sessions using the structured resume summary.

## Who It Is For

Independent creators, coaches, educators, authors, founders, and small service providers. No programming, command line, GitHub, or Cloudflare experience is required: technical terms are explained clearly as they arise.

The user only needs: an email address, a link to their existing website or Instagram account (or screenshots), and their list of destinations. Profile photos and cover art are not needed upfront: the site installs with placeholder graphics, and the user uploads real photos directly from the mobile admin panel later.

## Scope and Boundaries

- **Five fixed block types:** `destacado`, `tarjeta`, `fila`, `libros`, and `redes`. Structural design is determined by block types; the admin panel does not alter typography scales or color palettes.
- **Link click metrics:** Clicks are tracked per link over 7-day and 30-day windows. Total site visitor counts and referrer data are not tracked.
- **Brand token updates:** Changing site colors, fonts, or title is performed by re-running this skill (see `references/6-daily-use.md`), not inside `/admin/`.
- **Domain routing:** Sites receive a free `*.pages.dev` subdomain. Custom domains are optional and documented in the installation guide.
- **Protocol restrictions:** URLs must begin with `https://`, `mailto:`, or `tel:`.

## Step 0: Route Detection

Automatically detect your operating environment. Never ask the user technical questions to detect your route.

- **Route A — Browser Chat (`claude.ai`, `gemini.google.com`, `chatgpt.com` — no local filesystem or shell tools):**
  - Zero local software required. Phase 1 (Design System), Phase 2 (Content & Blocks), and Phase 3 (JSON file generation) happen 100% inside chat, working seamlessly on mobile or desktop.
  - **Initial Message Rule:** Do NOT ask on message #1 whether they have a computer. Greet warmly in two sentences and immediately begin Phase 1 (`references/1-design-system.md`) by asking what they do and inviting them to share screenshots of their Instagram, website, or reference images.
  - Only when Phase 3 is completed and approved (prior to starting `references/5-install-from-browser.md`), inform them: *"To publish your website for free, you will click through creating your repository on GitHub and your free Cloudflare account (since a browser chat cannot interact with external accounts on your behalf). That takes about 15 minutes and is much easier on a desktop computer. Do you have a computer handy now, or would you like a resume summary to continue there later?"*
- **Route B — Agentic IDE (Google Antigravity, Cursor, Windsurf, or VS Code with Claude Code / Codex extension — desktop IDE with workspace and file editing tools):**
  - If the user is non-technical, reassure them in plain terms: they do not need to write code or execute terminal commands themselves. You write `brand/theme.json`, `brand/seed.json`, and `brand/examples.json` directly into their workspace, run verification commands, and guide or execute the installation in `references/4-install-with-agent.md` (smoothly falling back to browser clicks in `references/5-install-from-browser.md` if they prefer web UI over CLI authentication).
- **Route C — Terminal / CLI Agent (Claude Code CLI, Codex CLI, Gemini CLI):**
  - Full automated terminal workflow detailed in `references/4-install-with-agent.md` (`gh repo create NAME --template cgandini/personal-web --private --clone`, `wrangler d1`, `npm test`, etc.).

## Guiding Non-Technical Users

1. **One action per message:** Present one discrete step or question, then pause for confirmation.
2. **Plain English / plain terms:** Explain any technical term in one simple sentence on first mention (see glossary in `references/5-install-from-browser.md`).
3. **Set visual expectations:** State what the user should see after each click, and what to do if the screen differs.
4. **Inspect screenshots:** If the user encounters an unexpected screen, request a screenshot and review it before suggesting corrections.
5. **Enforce credential privacy:** Never allow credentials or tokens in chat. If a command requires a secret, the user executes it directly on their machine or pastes it into the platform's encrypted secret field.
6. **No credit cards:** Cloudflare does not require credit card entry for this setup. If payment fields appear, redirect the user back to the Free plan.
7. **Progressive validation:** Review deliverables with the user and incorporate preferences before moving forward.
8. **No fabricated facts:** Use only verified facts, numbers, and links provided by the user.

## Phases

| Phase | Description | Deliverable | Reference Guide |
|---|---|---|---|
| 0. Welcome & Intake | Welcome, detect route, begin intake | Material received | this file |
| 1. Design System | Extract authentic brand colors, typography, tone | Approved `design-system.md` | `references/1-design-system.md` |
| 2. Content & Blocks | Select and prioritize block layout and copy | Approved block table | `references/2-content-and-blocks.md` |
| 3. Brand Files | Generate and validate `theme.json`, `seed.json`, `examples.json` | Validated JSON files | `references/3-brand-files.md` |
| 4. Installation | Deploy to Cloudflare Pages and D1 | Live URL and working `/admin/` | Route A: `references/5-install-from-browser.md`; Routes B/C: `references/4-install-with-agent.md` |
| 5. Daily Operations | Mobile editing, publishing, analytics, maintenance | Autonomous user | `references/6-daily-use.md` |

- **Standalone prompts:** Users operating without this skill can use `prompts/1-design-system.md`, `prompts/2-static-page.md`, and `prompts/3-install.md`.
- **Fictional reference brand:** Inspect `examples/sample-brand/` for valid formatting. All data for Renata Olmos (`example.com`) is synthetic and must never be copied to real sites.
- **Sources of truth:** Runtime schemas and limits in `docs/BLOCKS.md`, `packages/core/src/limits.js`, `packages/core/src/validate.js`, and `packages/core/src/icons.js` take precedence over secondary references.

## The Skill Only Generates `brand/`

The codebase remains untouched across personal brands. All customizations reside exclusively in `brand/`:
- `brand/theme.json`: palette tokens, Google Fonts links, site metadata, corner radius, texture.
- `brand/seed.json`: initial profile, blocks, and footer.
- `brand/examples.json`: preview blocks displayed in the admin panel's "Agregar bloque" sheet.
- `brand/images/`: placeholder images (`perfil` and `tapa`) used for initial deployment. Real user assets are uploaded via `/admin/`.

## Footer Attribution

`seed.json` defaults `footer` to `"Hecha con la plantilla gratis de imagineAI"`. The user may alter or clear this (`""`). The `footer` property is strictly required in `seed.json`, even when set to an empty string.

## Progress Checklist (Tracked by Agent)

Maintain and display this status block during phase milestones:

```
Route: [A (Browser Chat) / B (Agentic IDE) / C (Terminal CLI)]    Language: [ES-vos / ES-tú / EN / other]
[ ] 0 Welcome: Route selected, initial context gathered
[ ] 1 Design system approved (design-system.md)
[ ] 2 Content approved (block selection and sequence)
[ ] 3 Brand files: theme.json, seed.json, examples.json validated
[ ] 3 Photos: using placeholders for installation (real photos uploaded via panel later)
[ ] 4 Account creation completed (credentials kept private)
[ ] 4 Live site running on Cloudflare Pages and rendering cleanly on mobile
[ ] 4 Admin panel accessible with password (created privately by user)
[ ] 5 User uploaded photo via panel, edited content, and published a test update
```

## Session Resume Block

Deliver this structured summary at the conclusion of each phase and after key installation milestones:

```
RESUMEN PARA RETOMAR (personal-web)
Route and register: [...]
Desktop computer available for install: [yes / no / pending]
Completed phase: [n]. Next step: [...]
Installation step (n of 12): [n, or "not started"]
NAME: [unique repository and project name, e.g. ana-web]
GitHub username: [...]
Database ID: [D1 database ID; public string]
Brand: name, role, hook, specialty
Palette: [name + hex + usage role] x 4 to 6
Typography: headings [...], body [...], accent [...]
Tone: [pronouns, style attributes, vocabulary to avoid]
Blocks in sequence: [type, title, destination]
User preferences: [...]
Action items: [...]
Brand files: [paste complete theme.json, seed.json, examples.json when Phase 3 is reached]
```

## File Map

- `references/1-design-system.md`: Phase 1 guide.
- `references/2-content-and-blocks.md`: Phase 2 guide.
- `references/3-brand-files.md`: Phase 3 guide and schema validation tables.
- `references/4-install-with-agent.md`: Phase 4 guide for Route B (Agentic IDE) and Route C (Terminal CLI).
- `references/5-install-from-browser.md`: Phase 4 guide for Route A (Browser Chat).
- `references/6-daily-use.md`: Phase 5 guide for mobile management and analytics.
- `prompts/`: Standalone prompts for non-skill environments.
- `examples/sample-brand/`: Synthetic sample files (`theme.json`, `seed.json`, `examples.json`).
- `CHAT-PROMPT.md`: Ready-to-copy browser chat kickoff prompts.
- `FOR-CHAT.md`: Complete skill consolidated into a single file for upload (generated via `npm run bundle:skill`).

---

**FILE: `skill/personal-web/references/1-design-system.md`**

# Phase 1: Design System

**Goal:** Extract the person's authentic visual style (colors, typography, tone) and document it in `design-system.md`, which translates into `brand/theme.json`. Do not invent an ungrounded aesthetic: extract and refine what they already produce.

**Deliverables:** An approved `design-system.md` specification and a visual review sample.
- Route B / C (Agentic IDE / Terminal): Write `design-system.html` directly in their project directory (a standalone review page displaying palette swatches, typography samples, and block mockups) and direct them to double-click to view it in a browser.
- Route A (Browser Chat): If the assistant supports rendered HTML artifacts, provide one. Otherwise, present the palette table and three sample copy lines in chat for review.

Reference implementation: `examples/sample-brand/design-system.md`. Standalone prompt: `prompts/1-design-system.md`.

## Step 1: Gather Materials

Request the following in single discrete messages:

1. Link to their current website (if available).
2. 4 to 6 screenshots of their Instagram feed (profile view and recent content posts). Instruct clearly: "Open Instagram on your phone, take screenshots of your profile and a few posts you like, and send them here."
3. Logo files or known brand guidelines / hex codes (from Canva, brand decks, or logos).

If web browsing is available, inspect their homepage and primary service/offer page.

If the brand is entirely new (no existing website or active social presence): Ask for three reference accounts or sites they admire and three descriptive adjectives. Formulate at most **two** concise design directions. Do not present excess options.

## Step 2: Core Design Rules

1. **Extract rather than invent:** Palettes, fonts, and tone derive directly from published material. When their website and social feeds diverge, state which direction you prioritized and why (typically prioritizing their highest-engagement channel).
2. **One action, one color:** One vibrant accent color for interactive targets and highlights, one near-black ink (`tinta`, never `#000000`), one paper/canvas background (`fondo`), and one pure white (`superficie`). Target 4 to 6 core colors total.
3. **Small text never uses the accent color:** Light or warm accents (orange, yellow, bright green) consistently fail contrast minimums at small font sizes. Strict rule: small body copy and metadata use ink or gray, while the accent is reserved for **underlines, arrows, glyphs, and badges**.
4. **Darken the accent solely for large text** (24 px or larger, bold or accent font in profile and cards), and **preserve the hue**:
   - Maintain the hue (within ±5 degrees) and saturation, adjusting lightness downward conservatively.
   - Example from production: For a coach using bright orange (`#F76E09`, hue 25, sat 94%, lightness 50%), an initial test at `#9E4510` (hue 22, sat 82%, lightness 34%) was perceived as brown. The final production choice was `#D05000` (hue 23, sat 100%, lightness 41%), delivering a 3.38:1 contrast ratio against cream, **permitted strictly for large display text**.
   - If achieving 3.0:1 contrast turns a warm hue muddy, keep `acentoTexto` identical to `tinta` and rely on accent underlines for visual punch.
   - Present the darkened variant alongside the original swatch before finalizing.
5. **Maximum three typefaces**, all sourced from Google Fonts: one for headings, one for body copy, and **one** optional accent face used exclusively in two positions (the profile headline phrase and card title). If no accent face fits, reuse the heading or body font.
6. **Zero emojis:** Use icons from the template library (`packages/core/src/icons.js`; enumerated in `references/3-brand-files.md`).
7. **No synthetic claims:** Social proof metrics (e.g. "Over 500 graduates") are included only if verified from user materials.
8. **Iterate and align:** Request feedback on palette and typography, then apply refinements consistently across `design-system.md`, mockups, and `theme.json`.

## Step 3: Color Extraction

- Sample hex values from screenshots, noting that JPEG compression introduces minor variations. If the user provides exact brand hex values, their values supersede sampled ones.
- With local tools, measure image pixels programmatically (e.g., Python Pillow script) for precision.
- Assemble a palette table: Name, Hex code, Source location, and System role. Clearly distinguish original brand colors from accessibility-derived tones.

## Step 4: Contrast Verification

Contrast measures relative luminance between foreground and background. WCAG requires **4.5:1 or higher** for small text and **3.0:1 or higher** for large text (>=24 px or >=18.66 px bold).

**Formula** (per channel: `v = val/255`; if `v <= 0.03928` use `v/12.92`, else `((v+0.055)/1.055)^2.4`; luminance `L = 0.2126 R + 0.7152 G + 0.0722 B`; contrast ratio `(L_light + 0.05) / (L_dark + 0.05)`). With Node.js:

```bash
node -e "const L=h=>{const c=[1,3,5].map(i=>parseInt(h.slice(i,i+2),16)/255).map(v=>v<=.03928?v/12.92:((v+.055)/1.055)**2.4);return .2126*c[0]+.7152*c[1]+.0722*c[2]};const r=(a,b)=>{const[x,y]=[L(a),L(b)].sort((p,q)=>q-p);return ((x+.05)/(y+.05)).toFixed(2)};console.log(r('#D05000','#E9E2D7'))"
```

**Required Contrast Pairs in Template:**

| Foreground Token | Surface Token | Minimum Ratio | Location |
|---|---|---|---|
| `tinta` | `fondo` | 4.5:1 | Name, titles, labels |
| `texto` | `superficie` | 4.5:1 | Card body copy |
| `gris` | `fondo` and `superficie` | 4.5:1 | Role, subtitle, descriptions |
| `superficie` | `tinta` | 4.5:1 | Dark hero card (`destacado`) |
| `acentoSuave` | `tinta` | 4.5:1 | Tag and checkmark on dark hero card |
| `superficie` | `acento` | 3.0:1 (ideal 4.5:1) | Primary button text, icons, badge |
| `acentoTexto` | `fondo` and `superficie` | 3.0:1 | Display text: profile phrase and card title (large text only) |
| `acento` | `fondo` | Decorative | Underlines and arrows (aim for >=3.0:1) |

If a pairing fails: Adjust lightness incrementally while maintaining hue. If small copy fails even after adjustment, fall back to `tinta` or `texto`. Record ratios in `design-system.md`.

## Step 5: Typography

- **Google Fonts only:** Pages load fonts strictly from `fonts.googleapis.com`. Font names must match Google Fonts directory listings exactly.
- **Required weights in Google Fonts link:** Heading font requires 700 and 800; body font requires 400 and 500; accent font requires 400.
- Heading fonts render uppercase by default for the person's name and section labels; ensure the chosen typeface renders cleanly in uppercase.
- Confirm the `fontsHref` URL directly with the user in Phase 3 (see `references/3-brand-files.md`).

## Step 6: Tone and Voice

Examine published communications:
- **Pronouns and register:** Select one consistent register (e.g., Spanish voseo, tuteo, or formal English) and maintain it across all elements.
- **Structural pacing:** Sentence length, use of questions, rhythm, and direct hooks.
- **Vocabulary:** Core recurring phrases versus forbidden jargon.
- **Emoji policy:** Zero emojis on the site (SVG icons only).
- **Representative excerpts:** Include 3 to 4 real quotes from existing material with citations.

## Step 7: Draft `design-system.md`

Structure the document following `examples/sample-brand/design-system.md`:

```
# [Brand Name]: Design System
[One-line summary and consultation sources]
## General Aesthetic Rules     (3-4 lines: core brand feeling)
## Colors                     (core palette table, accessibility derivatives, contrast matrix)
## Typography                 (Google Fonts link, roles, weights, usage rules)
## Borders and Accents        (corner radius in px, background grain flag)
## Component Styling          (buttons, cards, rows, links in this specific brand)
## Voice and Tone             (register, hooks, patterns, phrases to avoid, verified quotes)
## Template Mapping           (explicit mapping to theme.json keys)
## Open Items                 (clarifications, font approximations, compression caveats)
```

**Template Token Mapping:**

| `theme.json` Key | Purpose |
|---|---|
| `colors.fondo` | Page background |
| `colors.superficie` | White cards and light text over dark surfaces |
| `colors.tinta` | Primary headings, dark hero card, dark button |
| `colors.texto` / `colors.gris` | Body text and secondary captions |
| `colors.borde` / `colors.bordeFondo` | Borders on white surfaces and borders on page canvas |
| `colors.acento` | Primary CTA button, row icon disc, underlines, arrows |
| `colors.acentoTexto` | Highlighted words in display headings |
| `colors.acentoSuave` | Label tag and checkmark on dark hero card |
| `colors.gradiente` / `colors.aroFoto` | Primary button hover gradient and profile photo ring |
| `fonts.titulo`, `fonts.texto`, `fonts.acento` | Typeface families |

## Step 8: Review and Approval

1. Present the review artifact or summary table.
2. Ask for feedback: colors, typography, tone.
3. Update tokens across `design-system.md` and re-verify contrast.
4. Upon approval, conclude the phase with the structured resume block from `SKILL.md`.

---

**FILE: `skill/personal-web/references/2-content-and-blocks.md`**

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

---

**FILE: `skill/personal-web/references/3-brand-files.md`**

# Phase 3: Brand Files

**Goal:** Transform the approved `design-system.md` and content structure from Phase 2 into `brand/` configuration files ready for deployment. **Only the `brand/` directory is generated or modified.**

**Deliverable:** Validated `brand/theme.json`, `brand/seed.json`, and `brand/examples.json`. Profile photos and book covers are uploaded later via the mobile admin panel.

Reference model: `examples/sample-brand/`. Fictional sample files for Renata Olmos (`example.com`) provide formatting reference only and must never be deployed to production. Detailed schema: `docs/BLOCKS.md`.

## File Responsibilities

| File | Purpose |
|---|---|
| `brand/theme.json` | Palette tokens, Google Fonts links, page title/description, grain texture, corner radius. |
| `brand/seed.json` | Initial published state: profile info, blocks array, and footer text. Rendered on initial deployment. |
| `brand/examples.json` | One sample block per type, used by the admin panel's "Agregar bloque" sheet. |
| `brand/images/` | Bundled placeholder images (`perfil` and `tapa`). Files in this directory are publicly exposed under `/_brand/`. |

## Intake Questions

Ask each question individually and wait for a response:

1. **Page language (`lang`):** `"es"` or `"en"`. Sets automatic UI labels (e.g. "Ver libro" vs. "View book"). The `/admin/` panel remains in Spanish.
2. **Search engine indexing:** "Do you want Google to index your page?" Yes = `"noindex": false`. No / Not yet = `"noindex": true`.
3. **Footer text:** Defaults to `"Hecha con la plantilla gratis de imagineAI"`. May be customized or set to empty string `""`. The `footer` key is strictly required in `seed.json`.

## `theme.json`

Every key is required. Review against this checklist:

| Key | Format / Rule |
|---|---|
| `lang` | `"es"` or `"en"` |
| `title`, `description` | Browser tab title and Open Graph description |
| `themeColor` | Hex code matching `colors.fondo` |
| `noindex` | Boolean (`true` or `false`) |
| `fontsHref` | Must begin with `https://fonts.googleapis.com/`. Verify that URL resolves |
| `fonts` | Object with `titulo`, `texto`, `acento` keys matching font families in `fontsHref` |
| `colors` | Object with 12 keys: `fondo`, `superficie`, `tinta`, `texto`, `gris`, `borde`, `bordeFondo`, `acento`, `acentoTexto`, `acentoSuave`, `gradiente`, `aroFoto`. Solid colors use `#RRGGBB` format |
| `colors.gradiente`, `colors.aroFoto` | CSS `linear-gradient(...)` strings without characters `;`, `{`, `}`, `<`, `>`, `\`, or `@` |
| `grain` | Boolean (`true` or `false`) |
| `radius` | Integer pixel value (typically 14 to 16) |

**Gradient Formula References:**
- `colors.gradiente`: `linear-gradient(135deg,ACENTO 0%,ACENTOTEXTO 90%)`. Example with `#2F855A` and `#276749`: `linear-gradient(135deg,#2F855A 0%,#276749 90%)`.
- `colors.aroFoto`: `linear-gradient(180deg,ACENTOSUAVE,ACENTO)`. Example with `#9ADBB4` and `#2F855A`: `linear-gradient(180deg,#9ADBB4,#2F855A)`.

**Mandatory `fontsHref` Verification:**
Assemble the Google Fonts stylesheet link with all required weights:
`https://fonts.googleapis.com/css2?family=Heading+Font:wght@700;800&family=Body+Font:wght@400;500&family=Accent+Font:wght@400&display=swap`.
Have the user open the URL in a browser, or with CLI tools verify via `curl -sI "<link>" | head -1` (must return HTTP 200).

## `seed.json`

Structure: `{ "version": 1, "profile": {...}, "blocks": [...], "footer": "..." }`.

- `version` must be the integer `1`. `footer` is mandatory (string, up to 160 chars).
- `profile`: `photo` and `name` are required; `role`, `phrase`, `highlight`, and `sub` are optional.
- Every block requires `id`, `type`, and `hidden` (boolean).
- **`id`:** Exactly 8 lowercase alphanumeric characters (`[a-z0-9]`), unique across the document. Follow the deterministic naming convention: `bloque01`, `bloque02` ... `bloque10`, with `redes001` for the social row. No hyphens, uppercase letters, or accents.
- **URLs:** Must begin with `https://`, `mailto:`, or `tel:`. No spaces, max 1000 characters. `http://` and `javascript:` are strictly prohibited.
- **Images:** `/img/<name>` or external `https://`. For installation, use placeholders: `profile.photo` = `"/img/perfil"`, and `cover` in `libros` = `"/img/tapa"`.
- **`highlight`:** In `profile` and `tarjeta`, the highlight string must be an exact character-for-character substring of `phrase` or `title`.

### Character Limits and Count Rules

Enforced by `packages/core/src/limits.js`:

| Location | Field / Identifier | Max Characters |
|---|---|---|
| Profile | `name` (`profileName`) | 60 |
| Profile | `role` (`profileRole`) | 80 |
| Profile | `phrase` | 120 |
| Profile | `highlight` (`profileHighlight`) | 120 |
| Profile | `sub` | 160 |
| Footer | `footer` | 160 |
| `destacado` | `label` / `title` / `text` / `proof` | 40 / 60 / 220 / 90 |
| `destacado` and `tarjeta` | `button.text` (`button`) | 40 |
| `tarjeta` | `label` / `title` / `highlight` / `text` | 40 / 60 / 60 / 220 |
| `fila` | `title` (`filaTitle`) / `text` (`filaText`) | 50 / 90 |
| `libros` | `label` / `groups[].title` (`groupTitle`) | 40 / 80 |
| `libros` | `title` (`bookTitle`) / `author` / `linkText` | 80 / 60 / 40 |
| `libros` | `more.text` (`button`) | 40 |
| All | `url` | 1000 |

| Constraint | Limit |
|---|---|
| Maximum blocks per page (`MAX_BLOCKS`) | 40 |
| Maximum JSON document size (`MAX_JSON_BYTES`) | 200 KB |
| Groups in `libros` (`COUNT.groups`) | 1 to 3 |
| Items in a `"destacado"` group | Exactly 1 |
| Items in a `"fila"` group | 1 to 3 |
| Items in `redes` (`COUNT.redes`) | 1 to 8 |

### Required Block Fields

- `destacado`: `title`, `button.text`, `button.url`.
- `tarjeta`: `title`, `button.text`, `button.url`.
- `fila`: `icon`, `title`, `url`, `verified`, `style` (`"solido"` or `"borde"`).
- `libros`: `groups` (each containing `title`, `layout` (`"destacado"` or `"fila"`), and `items` array with `title`, `cover`, and `url`).
- `redes`: `items` (each containing `network` and `url`).

### Supported Icon Identifiers (`packages/core/src/icons.js`)

- **Interface Icons (`ICON_KEYS`):** `arrow-right`, `chevron-right`, `check`, `mail`, `calendar`, `mic`, `presentation`, `book`, `user`, `globe`, `link`, `play`, `headphones`, `star`, `heart`, `message`, `phone`, `map-pin`, `gift`, `sparkles`.
- **Network Icons (`NETWORK_KEYS`):** `instagram`, `tiktok`, `youtube`, `spotify`, `x`, `linkedin`, `facebook`, `whatsapp`, `threads`, `email`, `web`. Allowed in `redes.items.network` and `fila.icon`; not permitted in `tarjeta.button.icon`.

## `examples.json`

Structure: `{ "version": 1, "blocks": { "destacado": {...}, "tarjeta": {...}, "fila": {...}, "libros": {...}, "redes": {...} } }`.

Must contain all five block type keys with valid 8-character ids (`ejdest01`, `ejtarj01`, `ejfila01`, `ejlibr01`, `ejredes1`). Covers in `libros` use `"/img/tapa"`.

## Image Handling

- **Default Workflow:** The template includes placeholder images `brand/images/perfil` and `brand/images/tapa`. Install using these placeholders. After deployment, the user uploads their personal portrait and book covers via the mobile `/admin/` panel (**Editar perfil** > **Subir foto**). The panel automatically resizes uploads to 480 px.
- **Optional Advanced Pre-bundling:** If assets are prepared before install:
  - Filename format: lowercase alphanumeric `[a-z0-9]`, 4 to 32 characters (`.webp`, `.jpg`, `.png`).
  - Max file size: under 400 KB, max dimension 480 px.

## Validation Before Delivery

### Route B and C: Command Line Validation

Execute from the workspace repository root:

```bash
# Verify seed.json
node --input-type=module -e "import {readFileSync} from 'node:fs'; import {validatePage} from './packages/core/src/validate.js'; const d=JSON.parse(readFileSync('brand/seed.json','utf8')); const r=validatePage(d); const e=[...r.errors]; if(d.profile?.highlight&&!d.profile.phrase?.includes(d.profile.highlight))e.push('profile.highlight is not an exact substring of phrase'); d.blocks?.forEach((b,i)=>{if(b.type==='tarjeta'&&b.highlight&&!b.title?.includes(b.highlight))e.push('blocks['+i+'].highlight is not an exact substring of title')}); console.log(e.length?'seed.json: ERRORS\n- '+e.join('\n- '):'seed.json: OK')"

# Verify examples.json
node --input-type=module -e "import {readFileSync} from 'node:fs'; import {validatePage} from './packages/core/src/validate.js'; const ex=JSON.parse(readFileSync('brand/examples.json','utf8')); let bad=0; for (const t of ['destacado','tarjeta','fila','libros','redes']){ const b=ex.blocks?.[t]; if(!b||b.type!==t){console.log(t+': missing or wrong type'); bad++; continue} const r=validatePage({version:1,profile:{photo:'/img/perfil',name:'Example'},blocks:[b],footer:''}); if(!r.ok){bad++; console.log(t+':\n- '+r.errors.join('\n- '))} } console.log(bad?'examples.json: ERRORS':'examples.json: OK')"

# Verify theme.json
node --input-type=module -e "import {readFileSync} from 'node:fs'; const t=JSON.parse(readFileSync('brand/theme.json','utf8')); const c=['fondo','superficie','tinta','texto','gris','borde','bordeFondo','acento','acentoTexto','acentoSuave']; const p=[]; for(const k of ['lang','title','description','themeColor','fontsHref'])if(!t[k])p.push('missing '+k); for(const k of [...c,'gradiente','aroFoto'])if(!t.colors?.[k])p.push('missing colors.'+k); for(const k of c)if(t.colors?.[k]&&!/^#[0-9A-Fa-f]{6}$/.test(t.colors[k]))p.push('colors.'+k+' is not #RRGGBB'); for(const k of ['titulo','texto','acento']){const f=t.fonts?.[k]; if(!f)p.push('missing fonts.'+k); else if(!String(t.fontsHref).includes(f.replaceAll(' ','+')))p.push('fonts.'+k+' ('+f+') not in fontsHref')} if(!String(t.fontsHref).startsWith('https://fonts.googleapis.com/'))p.push('fontsHref must start with https://fonts.googleapis.com/'); for(const k of ['noindex','grain'])if(typeof t[k]!=='boolean')p.push(k+' must be boolean'); if(!Number.isFinite(t.radius))p.push('radius must be a number'); console.log(p.length?'theme.json: ERRORS\n- '+p.join('\n- '):'theme.json: OK')"

# Verify static rendering
node --input-type=module -e "import {readFileSync} from 'node:fs'; import {renderPage, allImageIds} from './packages/core/src/render.js'; const doc=JSON.parse(readFileSync('brand/seed.json','utf8')); const theme=JSON.parse(readFileSync('brand/theme.json','utf8')); const images=Object.fromEntries(allImageIds(doc).map(id=>[id,{mime:'image/webp',url:'/i/'+id+'.webp'}])); const html=renderPage({doc,theme,mode:'public',images}); console.log('render: OK ('+html.length+' chars)')"
```

### Route A: Browser Chat Inspection Checklist

In conversational chat where code execution is unavailable, manually audit all 14 points before sharing JSON files:

1. Valid JSON: Double quotes on all keys and strings, no trailing commas, balanced braces.
2. `seed.json`: `version` is `1`; contains `profile`, `blocks`, and `footer`. No unauthorized keys.
3. `profile`: `photo` and `name` are present; `name` <= 60 chars.
4. Block IDs: Exactly 8 alphanumeric characters each (`[a-z0-9]`), no duplicate IDs.
5. Allowed types: Every block is one of `destacado`, `tarjeta`, `fila`, `libros`, `redes`, and includes `hidden`.
6. Valid URLs: Every link starts with `https://`, `mailto:`, or `tel:`, without whitespace.
7. Length constraints: All strings comply with max character limits.
8. `fila`: Contains `icon`, `title`, `url`, `verified`, and `style` (`"solido"` or `"borde"`).
9. Icon identifiers: All icons belong to `ICON_KEYS` or `NETWORK_KEYS`.
10. `libros`: 1 to 3 groups; `"destacado"` group has 1 item; `"fila"` group has 1 to 3 items.
11. `redes`: 1 to 8 items with recognized `network` identifiers.
12. Exact highlights: `highlight` matches substring in `phrase` or `title` verbatim.
13. `examples.json` and `theme.json`: All required keys, 12 colors, 3 Google fonts in `fontsHref`.
14. Image identifiers: Placeholder paths (`/img/perfil`, `/img/tapa`) are respected; no `example.com` domains remain.

Deliver each JSON file in its own fenced code block labeled with its path (`brand/theme.json`, `brand/seed.json`, `brand/examples.json`). Conclude with the structured resume block from `SKILL.md`.

---

**FILE: `skill/personal-web/references/5-install-from-browser.md`**

# Phase 4: Install from Browser (Route A: Zero Local Software)

**Goal:** Guide a user with zero command-line experience to deploy their personal web and admin panel completely free via browser web interfaces (GitHub and Cloudflare). The AI guides conversationally; the user performs each click and copy-paste action.

**Deliverable:** A live personal website accessible on mobile, a secure `/admin/` panel protected by password, and one verified test update published.

**Desktop Browser Requirement:** This phase involves the GitHub web editor and Cloudflare dashboard, which are significantly easier to navigate on a computer browser. If the user is on mobile, offer to deliver the resume summary so they can resume on desktop.

## Glossary (Explain in Plain Words on First Mention)

- **Repository:** The private storage folder for your website project hosted on GitHub.
- **Branch:** A parallel version of your repository; the primary live branch is named `main`.
- **Deploy:** The process where Cloudflare builds and publishes your website.
- **Build:** The automated assembly job that compiles your site during a deploy.
- **Build Log:** The step-by-step progress record showing whether the build succeeded.
- **API Token:** A secure digital key with a single permission allowing Cloudflare to read your database.
- **Variable / Secret:** A private setting Cloudflare stores for your project (e.g. your database ID or admin password). Hidden variables are designated as "Secret".
- **Deploy Hook:** A private web address that triggers Cloudflare to rebuild and update the site when visited by the admin panel during publishing.
- **Binding:** The link connecting your web application to your D1 database, named `DB`.
- **Retry Deployment:** The button used to re-run a build without changing source code.

## Guiding Rules

- **One action per message:** Wait for the user's confirmation before giving the next step. After each milestone, provide an updated single-line summary (`Installation step (n of 12)`, `NAME`, `GitHub username`, `Database ID`).
- **Set visual expectations:** State what the screen should display after each action, adding: "If you see a different screen or button label, let me know or send a screenshot."
- **Zero payment credentials:** The entire setup is completely free. If any screen asks for a credit card or billing information, halt immediately and guide the user back to the Free plan.
- **Strict secrets handling:** Never ask for or allow `PANEL_PASSWORD`, `CLOUDFLARE_API_TOKEN`, `CLOUDFLARE_ACCOUNT_ID`, or `DEPLOY_HOOK_URL` in chat. The user pastes these directly into Cloudflare. The database ID is not secret and can be shared.
- **Single name identifier:** Propose `links` or `<name>-web` in lowercase alphanumeric characters with hyphens (e.g. `ana-web`). This identifier (`NAME`) serves as the repository name, database name, and Pages project name.
- Have the finalized Phase 3 brand files (`theme.json`, `seed.json`, `examples.json`) ready in code blocks so the user can easily copy and paste them directly into GitHub.

---

## Stage 1: GitHub Account

1. Open **github.com**. If you already have an account, click **Sign in** and proceed to Stage 2. Otherwise, click **Sign up**.
2. Enter your email, create a secure password, choose a username, and complete the verification puzzle. Enter the verification code sent to your email.
3. If presented with subscription plans, select **Free**. If prompted for payment details, stop and notify me.

**Expected visual:** GitHub home dashboard with your profile avatar in the upper right.

**Check question:** "Are you signed in to GitHub with your username visible in the top right? What is your username?"

## Stage 2: Copy the Template Repository

1. Open the template repository: `https://github.com/cgandini/personal-web`.
2. Click the green **Use this template** button in the upper right, then select **Create a new repository**.
3. Under **Repository name**, enter `NAME`. Ensure **Owner** is your account. Select **Private** (Cloudflare can still read private repositories). Leave "Include all branches" unchecked.
4. Click the green **Create repository** button.

**Expected visual:** Your new repository showing folders (`brand`, `docs`, `functions`, etc.) with your username and `NAME` in the header.

**Check question:** "Do you see your new repository with the folder list and your username at the top?"

## Stage 3: Paste Brand Configuration Files

Replace the three sample files in `brand/` with your custom brand data one by one.

**For each file (`theme.json`, `seed.json`, `examples.json`), in that order:**
1. In your repository, click into the **brand** folder, then click the file.
2. Click the **pencil icon** (Edit this file) in the top right.
3. Click inside the editor, select everything (**Ctrl+A** on Windows or **Cmd+A** on Mac), and paste the content provided from Phase 3 (**Ctrl+V** or **Cmd+V**).
4. Click the green **Commit changes...** button, and in the popup modal, click **Commit changes** again.

Do not touch `brand/images/`. The template includes placeholder images (`perfil` and `tapa`) used until you upload real photos via `/admin/`.

**Check question:** "Are all three files inside `brand/` updated with your custom data?"

## Stage 4: Cloudflare Account

1. Open **dash.cloudflare.com/sign-up**. Enter your email and a password.
2. Confirm your email address by clicking the verification link sent by Cloudflare.
3. If prompted to "Add a domain" or select paid plans, dismiss or skip them. **If a credit card is requested, stop immediately.**

**Expected visual:** Cloudflare dashboard with a left-hand navigation sidebar including **Workers & Pages**.

**Check question:** "Do you see the Cloudflare dashboard with Workers & Pages in the left sidebar?"

## Stage 5: Create D1 Database and Update `wrangler.toml`

1. In the left navigation, click **Storage & Databases** > **D1 SQL database**.
2. Click **Create** (or **Create database**). Enter `NAME` as the database name, and click **Create**.
3. In the database details view, locate the **Database ID** (a UUID string like `1a2b3c4d-5e6f-...`). Copy and paste it here in chat (this string is not a secret).
4. I will provide the updated `wrangler.toml` content. In GitHub, open `wrangler.toml` in the repository root, click the **pencil icon**, replace the entire contents with the updated text, and click **Commit changes** twice.

```toml
name = "NAME"
pages_build_output_dir = "public"
compatibility_date = "2026-10-01"

[[d1_databases]]
binding = "DB"
database_name = "NAME"
database_id = "PASTE_DATABASE_ID_HERE"
migrations_dir = "migrations"
```

**Check question:** "Is the database created in D1 and is `wrangler.toml` updated in GitHub with your database ID?"

## Stage 6: Prepare API Token Location (Created in 7c)

The API token allows Cloudflare Pages build containers to query your D1 database during build. Because tokens are displayed only once, do not generate it until Stage 7c when the destination field is open.

Locate the page: In Cloudflare, click your user profile icon in the top right > **My Profile** > select **API Tokens** in the left menu (or visit `dash.cloudflare.com/profile/api-tokens`).

**Check question:** "Do you see the API Tokens screen with the 'Create Token' button? Do not click it yet."

## Stage 7a: Connect GitHub to Cloudflare Pages

1. In the Cloudflare dashboard, navigate to **Workers & Pages** > click **Create application** > select the **Pages** tab > click **Connect to Git**.
2. Select **GitHub**. In the authorization window, click **Install & Authorize**. Under repository access, choose **Only select repositories** and select `NAME`.
3. Back in Cloudflare, select repository `NAME` and click **Begin setup**.

**Check question:** "Do you see the project setup screen with your repository `NAME` displayed?"

## Stage 7b: Build Configuration

Fill in the build configuration:

| Field | Value |
|---|---|
| Project name | `NAME` (must match `name` in `wrangler.toml`) |
| Production branch | `main` |
| Framework preset | None |
| Build command | `npm ci && node scripts/build.mjs --remote` |
| Build output directory | `public` |

Inspect the screen: Is there an expandable section labeled **Environment variables (advanced)**?
- **If visible:** Expand it and proceed directly with Stage 7c before clicking **Save and Deploy**. The first build will succeed immediately.
- **If not visible:** Note that the initial automated build will produce a temporary red error. This is normal. Click **Save and Deploy** and proceed to Stage 7c in project Settings.

## Stage 7c: Variables and Secrets

Add three variables, **all set to Secret (Encrypt)**. With a `wrangler.toml` present, plaintext variables may be locked in the dashboard; encrypted secrets avoid this restriction. In your Pages project, go to **Settings** > **Variables and Secrets** > click **Add** for each:

1. **`CLOUDFLARE_ACCOUNT_ID`:** Your Cloudflare account ID, found on the main **Workers & Pages** overview under **Account details**. Copy and paste it directly. Never send it to the chat.
2. **`CLOUDFLARE_API_TOKEN`:** In the API Tokens tab prepared in Stage 6: Click **Create Token** > scroll to **Custom token** > click **Get started** > name it `NAME-build` > under **Permissions**, select **Account**, **D1**, **Read** > click **Continue to summary** > click **Create Token**. Copy the displayed token immediately and paste it into the `CLOUDFLARE_API_TOKEN` secret field. Never paste this token into chat.
3. **`PANEL_PASSWORD`:** Your private admin password. Create a strong passphrase: 4 unrelated words separated by hyphens (at least 12 characters total, e.g. `mesa-bosque-reloj-arena`). Save it immediately in your mobile password manager or a private note. **Never type or paste this password into chat.**

Note on Build Safeguard: If your Cloudflare dashboard displays a separate section under **Settings > Builds** called **Build variables and secrets** (or if deploy logs report that `CLOUDFLARE_API_TOKEN` was not found during `build.mjs`), add `CLOUDFLARE_ACCOUNT_ID` and `CLOUDFLARE_API_TOKEN` there as encrypted secrets as well.
Note on Database Binding: In **Settings > Bindings**, the `DB` binding is displayed in read-only mode because Cloudflare Pages manages it directly via `wrangler.toml`.

Click **Save**.

**Check question:** "Are all three secrets (`CLOUDFLARE_ACCOUNT_ID`, `CLOUDFLARE_API_TOKEN`, `PANEL_PASSWORD`) saved as encrypted secrets?"

## Stage 8: First Deployment

1. In your Pages project, go to **Deployments**. If the initial build failed, click the **three dots** icon next to it and select **Retry deployment**. Allow 1 to 2 minutes for completion.
2. Click the deployment to view the log. Scroll near the end:
   - **Success:** Status is **Success**, and the log displays `Página generada (todavía no hay nada publicado): public/index.html = página en preparación.`.
   - **Failure:** A line begins with `build:` followed by an error. If it mentions authorization or authentication, the token permissions require adjustment. In Cloudflare, edit token `NAME-build`, change **Read** to **Edit** under D1, and retry deployment.
3. Open `https://NAME.pages.dev`. The page should display **"Página en preparación"**. This confirms the static build pipeline and placeholder images are active.

**Check question:** "Does the deployment log show Success, and does `https://NAME.pages.dev` display 'Página en preparación'?"

## Stage 9: Automated Publish Trigger (Deploy Hook)

The deploy hook triggers automated static rebuilds whenever you publish changes from `/admin/`.

1. In your Pages project, go to **Settings > Builds** (or Builds & deployments) > scroll to **Deploy hooks** > click **Add deploy hook**.
2. Set Hook name to `panel`, choose branch `main`, and click **Save**.
3. Copy the generated URL (begins with `https://api.cloudflare.com/`). This URL acts as a secret key; do not share it in chat.
4. Navigate to **Settings > Variables and Secrets**, click **Add**, enter variable name `DEPLOY_HOOK_URL`, select **Secret (Encrypt)**, and paste the URL. Click **Save**.
5. Go to **Deployments**, click the three dots on the latest deployment, and click **Retry deployment**.
6. Under **Settings > Builds > Branch control**, set preview branches to **None** to avoid running unnecessary builds on branches.

**Check question:** "Is `DEPLOY_HOOK_URL` saved as an encrypted secret, and did the retry deployment complete with Success?"

## Stage 10: Initialize Database in Admin Panel

1. Open `https://NAME.pages.dev/admin/` in your browser. You will see **"Entrar al panel"** with a password prompt. Enter your `PANEL_PASSWORD`.
2. Inside the panel, you will see **"Tu página todavía no está preparada"** and a button labeled **"Preparar mi página"**.
3. Click **"Preparar mi página"** (the button indicates "Preparando…"). This generates database tables and seeds initial brand content.
4. The dashboard displays **"Tu página"** with your blocks. The subheader will indicate "Actualizando tu página…" and within 1 to 2 minutes will confirm **"Tu página está al día"**.
5. Open `https://NAME.pages.dev` on your mobile phone and refresh. Your personal micro-web is live with placeholder images.

**Check question:** "Does your personal web render on your phone with your custom colors, title, and blocks?"

## Stage 11: Upload Photo, Test Edit, and Device Pairing

1. In the admin panel, tap **Editar perfil**, tap **Subir foto**, and choose your portrait photo (automatically compressed to 480 px). If an iPhone image shows an error ("No se pudo leer la imagen"), take a screenshot of the photo on your phone and upload the screenshot.
2. Edit a phrase, tap **Vista previa** to inspect, then tap **Publicar** and confirm. Book cover images are uploaded directly within their respective blocks.
3. Wait 1 to 2 minutes until the panel says "Tu página está al día", then refresh your live page to verify the update.
4. **Two-Device Registration for Rate-Limit Immunity:** Log in to `/admin/` from a second device (e.g. from your phone if you used desktop for setup). Successful login sets an independent, long-lived device cookie (`__Host-panel-device`). If an external bot ever triggers failed attempt lockouts, devices that have logged in previously retain their own dedicated attempt lane and are not locked out.

## Stage 12 (Optional): Custom Domain

A custom domain is optional. The `NAME.pages.dev` domain remains completely free forever.

- **Subdomain setup (e.g. `links.yourdomain.com`):** In Pages project, go to **Custom domains** > **Set up a domain** > enter `links.yourdomain.com`. In your DNS provider, create a **CNAME** record: name `links`, target `NAME.pages.dev`.
- **Apex domain setup (`yourdomain.com`):** Requires managing nameservers on Cloudflare, which is outside the scope of this guide.

---

## Troubleshooting Reference

The table below lists exact verbatim messages shown by the `/admin/` panel or Cloudflare builds, with corresponding resolutions:

| Observed Behavior / Message | Cause | Resolution |
|---|---|---|
| Build terminates with `build:` and wrangler authorization error | API token has insufficient D1 permissions | In Cloudflare > API Tokens, edit `NAME-build`, change **Read** to **Edit** in D1, save, and click **Retry deployment**. |
| Build log states token not found or "not authenticated" | Misnamed or missing secret | Verify secret is named exactly `CLOUDFLARE_API_TOKEN`. If Settings > Builds contains **Build variables and secrets**, add `CLOUDFLARE_ACCOUNT_ID` and `CLOUDFLARE_API_TOKEN` there as encrypted secrets, then retry deployment. |
| First deployment fails before variables are configured | Expected behavior if variables were not added during project creation | Add variables in Settings > Variables and Secrets, then click **Retry deployment**. |
| Build succeeds with `Página generada (todavía no hay nada publicado)...` and page shows "Página en preparación" | Normal state prior to database preparation | Proceed to Stage 10 and click **"Preparar mi página"**. |
| Build fails during `npm ci` | Missing `package-lock.json` in repository | Check repository files in GitHub. Ensure `package-lock.json` was copied from template. |
| "Use this template" button is missing | Not signed in to GitHub | Log in to github.com and reload the template page. |
| Cloudflare cannot see repository | GitHub authorization scope | In GitHub: Settings > Applications > Cloudflare Pages > Configure > add repository `NAME`. |
| Panel shows `"El acceso al panel no está configurado. Revisá el README."` | `PANEL_PASSWORD` variable is missing or deploy has not completed | Add `PANEL_PASSWORD` secret in Settings > Variables and Secrets and click **Retry deployment**. |
| Panel shows `"La contraseña del panel tiene que tener al menos 12 caracteres. Cambiala en Cloudflare (Settings > Variables and Secrets) y volvé a desplegar."` | Password is shorter than 12 characters | Update `PANEL_PASSWORD` to 12+ characters and retry deployment. |
| Panel shows `"Demasiados intentos. Esperá 15 minutos y probá de nuevo, o entrá desde un dispositivo donde ya hayas entrado antes."` | Failed login limit triggered | Wait 15 minutes, or log in from a paired device. Changing password does not clear the lockout timer. |
| Login shows `"No se pudo comprobar la contraseña ahora. Revisá que la base de datos (DB) esté conectada al proyecto, o probá de nuevo en un rato."` | Missing D1 binding | In Settings > Bindings, `DB` is read-only. Verify `database_id` and `database_name` in `wrangler.toml` on GitHub match your D1 database, then retry deployment. |
| Login shows `"La contraseña es correcta, pero el navegador no guardó la sesión. Revisá que acepte cookies y que estés en la dirección https de tu página."` | Cookies disabled or non-HTTPS URL | Enable cookies in browser settings and verify you are accessing the exact `https://NAME.pages.dev/admin/` URL. |
| **"Preparar mi página"** shows `"Falta la imagen «x» (brand/images/x.webp, .jpg o .png) o no es una imagen válida. ... No se cargó nada."` | Brand JSON references an image outside placeholder set | Update `seed.json` to use `/img/perfil` and `/img/tapa`, wait for build success, and click button again. |
| **"Preparar mi página"** shows `"No se pudo preparar la página. Probá de nuevo; si sigue fallando, avisale a quien te dio el proyecto."` | Interrupted network request or race condition | Click **"Preparar mi página"** again. Partial tables do not conflict. |
| **"Preparar mi página"** shows `"La base de datos no está conectada al proyecto (falta el binding DB). Revisá Settings > Bindings."` or `"El servidor no tiene acceso a los archivos de la marca (brand/images/). Volvé a desplegar el proyecto."` | Binding issue or incomplete build | In Settings > Bindings verify `DB` binding; check `wrangler.toml` in GitHub and click **Retry deployment**. |
| Forgotten password | Lost password | Change `PANEL_PASSWORD` in Cloudflare Settings > Variables and Secrets, then click **Retry deployment**. All existing sessions will expire. |
| Publishing does not update live site | Missing or invalid `DEPLOY_HOOK_URL` | Check Stage 9. Manually click **Retry deployment** under Deployments in the interim. |
| Custom domain displays error 522 | CNAME created before domain registration in Pages | Register domain first under Pages project **Custom domains** (Stage 12). |
| Image upload fails | Unsupported mobile camera format | Take a screenshot of the photo and upload the screenshot. |

---

**FILE: `skill/personal-web/references/6-daily-use.md`**

# Phase 5: Daily Operations

**Goal:** Ensure the user can independently edit, publish, and review click analytics from their mobile phone, and understands how to troubleshoot minor issues. Conclude onboarding with a live drill: request that they edit a line of copy, review the preview, and publish.

Exact text strings displayed by the `/admin/` panel interface are quoted in Spanish below.

## Accessing the Admin Panel

- The admin interface is located at your website address followed by `/admin/` (for example: `https://your-page.pages.dev/admin/`). Bookmark this address or add it to your mobile phone home screen.
- Log in with the passphrase created during setup (screen displays **"Entrar al panel"**, password field labeled **"Contraseña"**, submit button **"Entrar"**). Tap **"Salir"** when finished on shared computers.
- **If you forget your password:** In the Cloudflare dashboard, go to your Pages project > Settings > Variables and Secrets > edit `PANEL_PASSWORD` (must be 12+ characters) > go to Deployments and click **Retry deployment**. This securely terminates existing sessions across all devices. Never paste your password into chat.

## Admin Panel Layout ("Tu página")

| Section | Functionality |
|---|---|
| Top bar, **"Vista previa"** | Previews the live layout with unsaved draft changes. Clicks inside preview are not logged. |
| Status indicator below title | Indicates draft save state: `"Guardando…"`, `"Guardado"`, or `"Sin conexión"`. Saves automatically seconds after edits. |
| Profile card, **"Editar perfil"** | Modify portrait photo, name, role, hook phrase, highlight substring, subtitle, and **"Nota al pie"** (footer). |
| Tab **"Bloques"** | Block list in screen display order. Each block includes actions: **"Subir"**, **"Bajar"**, **"Ocultar"** (or **"Mostrar"**), **"Editar"**, and **"Borrar"** (with confirmation dialog). |
| **"Agregar bloque"** | Opens bottom sheet displaying the five block types with live previews styled in your brand tokens. |
| **"Publicar"** | Button states: Active **"Publicar"** when uncommitted changes exist; dimmed **"Publicado"** when live page matches draft. |
| Tab **"Estadísticas"** | Tracks link clicks over rolling **7 días** or **30 días** intervals. |

## The Publishing Workflow

1. Edit content. Changes save automatically as a local draft.
2. Tap **"Vista previa"** to review the layout.
3. Tap **"Publicar"** and confirm (**"¿Publicar los cambios?"**).
4. Allow **1 to 2 minutes** for the static rebuild. The status line will indicate `"Actualizando tu página…"` followed by `"Tu página está al día"`.
5. Open your public site in a browser tab or mobile window and refresh to view updates.

Operational notes:
- Blocks marked **"Sin completar"** (missing required fields) are omitted from publication. The confirmation dialog explicitly warns: `"Hay N bloques sin completar que no se van a publicar."`.
- **"Ocultar"** temporarily hides a block from public view without deleting its data (ideal for seasonal promotions).
- Each publish triggers a Cloudflare Pages static build. The Cloudflare Free plan includes **500 builds per month**; bundle related edits into a single publish when practical.

## Photo Management

In **"Editar perfil"** (profile portrait) or inside a `libros` block (cover images), tap **"Subir foto"**. The panel automatically compresses images to 480 px. If an iPhone photo generates the notice `"No se pudo leer la imagen"`, take a screenshot of the photo on your phone and upload the screenshot.

## Click Analytics

Under the **"Estadísticas"** tab, clicks are counted per link (over 7 or 30 days). Total visitor numbers and referring sites are not tracked. A daily safety cap (`CLICK_DAILY_CAP`, 20,000 clicks/day) protects D1 write allowances; if reached, click tracking pauses until 00:00 UTC while the public site continues serving traffic normally.

## Troubleshooting Reference

| Interface Message / Symptom | Underlying Cause | Corrective Action |
|---|---|---|
| Screen returns to `"Entrar al panel"`, displaying `"Tu sesión venció. Entrá de nuevo con tu contraseña."` | 30-day session cookie expired or `PANEL_PASSWORD` was changed | Enter password and tap **"Entrar"**. Draft edits are preserved in storage. |
| `"La contraseña es correcta, pero el navegador no guardó la sesión. Revisá que acepte cookies y que estés en la dirección https de tu página."` | Browser blocking cookies or insecure HTTP protocol | Enable browser cookies and ensure URL uses `https://`. |
| `"La contraseña no es correcta."` | Typo in entered password | Re-enter passphrase carefully without trailing whitespace. |
| `"Demasiados intentos. Esperá 15 minutos y probá de nuevo, o entrá desde un dispositivo donde ya hayas entrado antes."` | Rate limit triggered by repeated failed attempts | Wait 15 minutes, or log in from a previously authenticated paired device. Changing the password does not bypass the lockout timer. |
| `"El acceso al panel no está configurado. Revisá el README."` | `PANEL_PASSWORD` variable is missing or deployment pending | Verify `PANEL_PASSWORD` in Cloudflare Variables and Secrets and trigger **Retry deployment**. |
| `"La contraseña del panel tiene que tener al menos 12 caracteres. Cambiala en Cloudflare (Settings > Variables and Secrets) y volvé a desplegar."` | Passphrase shorter than 12 characters | Update secret in Cloudflare to 12+ characters and retry deployment. |
| `"Se editó desde otro dispositivo…"` | Concurrent edits made from a different session | Tap **"Recargar"** to synchronize latest state. |
| `"Tu página todavía muestra la versión anterior"` (after 4 minutes) | Build delayed or failed | Check Cloudflare Pages > Deployments log. If failed, click **Retry deployment**. |
| `"Publicado, pero no se pudo pedir la actualización de la página"` | Changes saved in D1, but deploy hook call timed out | Trigger manual **Retry deployment** in Cloudflare Deployments, or publish a minor change later. |
| `"Guardado como publicado, pero falta configurar la actualización automática (ver README)"` | Missing `DEPLOY_HOOK_URL` secret | Add `DEPLOY_HOOK_URL` secret in Cloudflare Pages settings (see Phase 4). |
| `"esa imagen ya no existe, subila de nuevo"` | Referenced image removed from storage | Re-upload image in block editor and publish. |
| Public page says `"Página en preparación"` | Initial database setup not yet executed | Open `/admin/` and click **"Preparar mi página"**. |
| A block does not display on public site | Block is marked `"Oculto"` or `"Sin completar"` | In block editor, tap **"Mostrar"** or complete missing fields. |

## Content Editing vs. Brand Redesign

| Handled in Mobile Admin Panel | Handled via AI Skill (Brand Redesign) |
|---|---|
| Copy, links, vertical order, images | Color palette and font families |
| Adding, toggling, and removing blocks | Browser tab title and Open Graph metadata |
| Footer attribution copy (**"Editar perfil"**) | Search engine indexing rules (`noindex`) |
| Viewing click analytics | System localization language |

## Future Brand Redesigns

1. Start a new AI chat, paste the prompt from `CHAT-PROMPT.md`, and provide `FOR-CHAT.md`.
2. Provide your current `design-system.md` and `brand/theme.json`.
3. Specify requested visual changes. The AI updates tokens, re-verifies contrast guidelines from `references/1-design-system.md`, and validates JSON structure.
4. Replace `brand/theme.json` in GitHub via the web editor and commit. Cloudflare automatically rebuilds the site in 1 to 2 minutes.

**Do not click "Preparar mi página" to update brand tokens.** Once initialized, the database retains published content. Modifying colors or typography only requires updating `brand/theme.json`.

## Backups

Website state resides in Cloudflare D1. Keep a private backup of your `brand/` configuration files and `design-system.md` in local storage or notes to ensure complete portability.

---

**FILE: `docs/BLOCKS.md`**

# Personal Web Blocks

Block type reference for anyone assembling or editing a page (user or AI agent using the skill). Layout is governed by block types; you only provide content. Individual blocks do not specify custom colors or fonts: everything is styled via tokens in `brand/theme.json`.

Full technical specification (routes, validation, API): `docs/SPEC.md`. Supported icons: `packages/core/src/icons.js`.

## Document Structure

```json
{
  "version": 1,
  "profile": {
    "photo": "/img/perfil",
    "name": "Firstname Lastname",
    "role": "Role · Specialty",
    "phrase": "A short, memorable hook.",
    "highlight": "memorable hook.",
    "sub": "A one-line summary clarifying what you offer."
  },
  "blocks": [],
  "footer": "Small footer note (optional)"
}
```

- `profile.photo` (required): image reference (see Rules). Profile field limits: `name` (required) 60, `role` 80, `phrase` 120, `highlight` 120, `sub` 160, `footer` 160. Defined in `packages/core/src/limits.js` (single source of truth shared by runtime and admin panel).
- `highlight`: exact substring of `phrase`; styled using accent color and underline. If it does not match character-for-character, no highlight is rendered.
- `footer` ("Nota al pie" in admin panel under Editar perfil): small centered text at the end of the page, after all blocks, up to 160 characters. Empty string `""` = not rendered.
- Every block requires `id` (exactly 8 alphanumeric characters `[a-z0-9]`, unique across page), `type`, and `hidden` (`true` hides block without deleting it). Array order matches vertical screen order.

## General Rules

- Images: `/img/<id>` (uploaded via admin panel) or `https://...`. In storage, uploaded images use `/img/<id>`; during build/publish, `scripts/build.mjs` generates an immutable static file `/i/<id>.<ext>` for each rendered image (and inlines it as a data URI if within budget: 80 KB per image and 300 KB total per page). Visitors never hit `/img/`. Unreferenced uploaded images older than 24 hours are pruned on publish.
- Links: `https://`, `mailto:`, or `tel:`. Nothing else is allowed.
- Text: up to 300 characters, subject to specific block field limits. Maximum 40 blocks and 200 KB JSON size per document. Links: up to 1000 characters.
- Empty optional strings (`""`) or whitespace-only values are treated as absent and not rendered.
- Icons: keys from `ICON_KEYS` (`arrow-right`, `chevron-right`, `check`, `mail`, `calendar`, `mic`, `presentation`, `book`, `user`, `globe`, `link`, `play`, `headphones`, `star`, `heart`, `message`, `phone`, `map-pin`, `gift`, `sparkles`) and, in `fila.icon` only, also keys from `NETWORK_KEYS` (`instagram`, `tiktok`, `youtube`, `spotify`, `x`, `linkedin`, `facebook`, `whatsapp`, `threads`, `email`, `web`).
- Public page links track click metrics; preview links do not.
- Incomplete blocks (missing required fields) are not sent to runtime: they remain saved in draft and are skipped on publish. The publish confirmation dialog warns if incomplete blocks exist ("Hay N bloques sin completar que no se van a publicar.").
- Every publish regenerates static HTML; the admin panel indicates "Tu página está al día" once live output matches the published timestamp.

## destacado

Dark hero card with primary call to action (the single most important offer). Use once at the top of the page.

| Field | Required | Character Limit |
|---|---|---|
| `label` | no | 40 (uppercase, spaced) |
| `title` | yes | 60 |
| `text` | no | 220 |
| `proof` | no | 90 (checkmarked social proof line) |
| `button` | yes | `{ text, url }`; `text` up to 40 |

```json
{
  "id": "coaching",
  "type": "destacado",
  "hidden": false,
  "label": "1-on-1 Session",
  "title": "Coaching with me",
  "text": "45 minutes to unblock your immediate challenges and leave with a roadmap.",
  "proof": "Over 650 clients guided.",
  "button": { "text": "Book your session", "url": "https://example.com/coaching" }
}
```

Brand token mapping: background `tinta`, text `superficie`, label `acentoSuave`, checkmark `acentoSuave`, button `acento` with `superficie` text and arrow icon; button hover transitions to `gradiente`. Title uses `fonts.titulo`, body uses `fonts.texto`. Border radius uses `radius`.

## tarjeta

Light card for secondary actions (newsletter, lead magnet, community). Can emphasize part of the title with the accent font.

| Field | Required | Character Limit |
|---|---|---|
| `label` | no | 40 |
| `title` | yes | 60 |
| `highlight` | no | up to 60; exact substring of `title` |
| `text` | no | 220 |
| `button` | yes | `{ text, url, icon? }`; `text` up to 40 (`icon` from `ICON_KEYS`) |

```json
{
  "id": "newslet1",
  "type": "tarjeta",
  "hidden": false,
  "label": "Newsletter",
  "title": "Personal growth without gimmicks",
  "highlight": "without gimmicks",
  "text": "One actionable idea every Thursday morning.",
  "button": { "text": "Subscribe", "url": "https://example.com/newsletter", "icon": "mail" }
}
```

Brand token mapping: background `superficie` with `borde` line; label and button in `tinta` (button text `superficie`); title uses `fonts.acento` with highlighted substring in `acentoTexto` and a 2 px underline in `acento`; body text uses `texto`.

## fila

Single-line link row with icon and brief description. Used for chat channels, speaking inquiries, contact options, or secondary destinations.

| Field | Required | Character Limit / Allowed Values |
|---|---|---|
| `icon` | yes | `ICON_KEYS` or `NETWORK_KEYS` |
| `title` | yes | 50 |
| `text` | no | 90 |
| `url` | yes | link (`https://`, `mailto:`, `tel:`) |
| `verified` | yes | boolean (`true` renders verified badge next to title) |
| `style` | yes | `"solido"` (solid surface background, icon in accent disc) or `"borde"` (transparent, outline only) |

```json
{
  "id": "whatsapp",
  "type": "fila",
  "hidden": false,
  "icon": "whatsapp",
  "title": "WhatsApp Channel",
  "text": "Latest updates sent straight to your phone.",
  "url": "https://whatsapp.com/channel/XXXX",
  "verified": true,
  "style": "solido"
}
```

Brand token mapping: `solido` style uses `superficie` + `borde` outline, disc `acento` with glyph `superficie`; `borde` style uses `bordeFondo` outline and ring with `tinta` glyph. Title uses `fonts.titulo`, description uses `gris`, chevron uses `gris`, verified badge uses `acento`.

## libros

Media cover gallery. Intended for books, guides, courses, podcasts, or products featuring vertical covers. Built with groups; each group has a subtitle and layout style.

| Field | Required | Character Limit / Rules |
|---|---|---|
| `label` | no | 40 (section header) |
| `groups` | yes | 1 to 3 groups |
| `groups[].title` | yes | 80 |
| `groups[].layout` | yes | `"destacado"` (1 item with large cover) or `"fila"` (1 to 3 items in a 3-column row) |
| `groups[].items[]` | yes | `{ title, author?, linkText?, cover, url }`; `title` 80, `author` 60, `linkText` 40; `cover` = image ref |
| `groups[].items[].linkText` | no | 40; used only in `"destacado"` group for text link (defaults to "Ver libro") |
| `more` | no | `{ text, url }`: trailing link ("View all..."); `text` up to 40 |

```json
{
  "id": "libros01",
  "type": "libros",
  "hidden": false,
  "label": "Publications",
  "groups": [
    {
      "title": "Featured Release",
      "layout": "destacado",
      "items": [{ "title": "Field Guide to Design", "cover": "/img/abc123", "url": "https://example.com/book", "linkText": "Order copy" }]
    },
    {
      "title": "Annotated Classics",
      "layout": "fila",
      "items": [
        { "title": "Enchiridion", "author": "Epictetus", "cover": "/img/def456", "url": "https://example.com/a" },
        { "title": "Meditations", "author": "Marcus Aurelius", "cover": "/img/ghi789", "url": "https://example.com/b" }
      ]
    }
  ],
  "more": { "text": "Browse full catalog", "url": "https://example.com/books" }
}
```

Notes: covers render at 90 x 135 px (2:3 aspect ratio, cropped). In a `"destacado"` group, the text link defaults to "Ver libro" unless `linkText` is explicitly set. For click tracking, items receive sequential indices (0, 1, 2...) across groups, with the `more` link assigned the index immediately following the final item (labeled in stats with `more.text`).

Brand token mapping: section header uses `fonts.titulo` in `tinta`; group titles use `gris`; book titles use `fonts.titulo`, authors use `gris`; cover shadow derived from `tinta`; text links use `tinta` with a 2 px underline and arrow in `acento`; hover transitions text link to `acentoTexto`.

## redes

Row of circular social icons. Rendered centered near bottom of page (place this block last, immediately above `footer`).

| Field | Required | Rules |
|---|---|---|
| `items[]` | yes | 1 to 8 items: `{ network, url }` with `network` from `NETWORK_KEYS` |

```json
{
  "id": "redes001",
  "type": "redes",
  "hidden": false,
  "items": [
    { "network": "instagram", "url": "https://instagram.com/username" },
    { "network": "youtube", "url": "https://www.youtube.com/@username" },
    { "network": "email", "url": "mailto:hello@example.com" }
  ]
}
```

Brand token mapping: 44 px circles with `bordeFondo` border and `tinta` icon; hover state transitions border to `tinta`.

## Panel Block Examples

The "Agregar bloque" sheet in the admin panel previews each block type styled with brand tokens. These previews are defined in `brand/examples.json`: one valid, complete block per type (`destacado`, `tarjeta`, `fila`, `libros`, `redes`), written in brand voice with real URLs where applicable. The skill generates this file alongside the rest of `brand/`.

## Full Page Brand Tokens

| Token (`brand/theme.json`) | Application |
|---|---|
| `colors.fondo` | page background, profile photo border padding |
| `colors.superficie` | light card surface, light text on dark backgrounds and on `acento` |
| `colors.tinta` | primary headings, strong text, `destacado` card surface, dark buttons |
| `colors.texto` / `colors.gris` | body text / secondary text |
| `colors.borde` / `colors.bordeFondo` | borders on white / borders on page background |
| `colors.acento` | primary button, `fila` disc, highlights, arrows, verified badge |
| `colors.acentoTexto` | highlighted text in headlines (profile phrase, `tarjeta` title) |
| `colors.acentoSuave` | label and checkmark in `destacado` card |
| `colors.gradiente` | primary button hover state |
| `colors.aroFoto` | decorative ring around profile photo |
| `fonts.titulo` / `texto` / `acento` | headings & buttons / body / profile phrase & `tarjeta` title |
| `grain` | `true` activates subtle SVG point texture on background |
| `radius` | corner radius for cards and rows (in pixels) |
| `noindex` | `true` adds `<meta name="robots" content="noindex">` |

---

**FILE: `skill/personal-web/examples/sample-brand/theme.json`**

FORMAT REFERENCE ONLY, not for deployment: Fictional sample for Renata Olmos. The `example.com` links, copy, and data are synthetic and must never be copied to a real person's website.

```json
{
  "lang": "es",
  "title": "Renata Olmos · links",
  "description": "Los links de Renata Olmos, nutricionista. Ejemplo ficticio de la skill personal-web.",
  "themeColor": "#F2EEE4",
  "noindex": true,
  "fontsHref": "https://fonts.googleapis.com/css2?family=Fraunces:wght@700;800&family=Nunito+Sans:wght@400;500&family=Caveat:wght@400&display=swap",
  "fonts": { "titulo": "Fraunces", "texto": "Nunito Sans", "acento": "Caveat" },
  "colors": {
    "fondo": "#F2EEE4",
    "superficie": "#FFFFFF",
    "tinta": "#1F2A24",
    "texto": "#3A453F",
    "gris": "#5A6660",
    "borde": "#E4E0D6",
    "bordeFondo": "#D8D2C3",
    "acento": "#2F855A",
    "acentoTexto": "#276749",
    "acentoSuave": "#9ADBB4",
    "gradiente": "linear-gradient(135deg,#2F855A 0%,#276749 90%)",
    "aroFoto": "linear-gradient(180deg,#9ADBB4,#2F855A)"
  },
  "grain": true,
  "radius": 14
}
```

---

**FILE: `skill/personal-web/examples/sample-brand/seed.json`**

FORMAT REFERENCE ONLY, not for deployment: Fictional sample for Renata Olmos. The `example.com` links, copy, and data are synthetic and must never be copied to a real person's website.

```json
{
  "version": 1,
  "profile": {
    "photo": "https://example.com/fotos/renata.jpg",
    "name": "Renata Olmos",
    "role": "Nutricionista · Comer simple",
    "phrase": "Comer bien no tiene que ser complicado.",
    "highlight": "no tiene que ser complicado.",
    "sub": "Planes reales para vidas reales, sin dietas extremas."
  },
  "blocks": [
    {
      "id": "consulta",
      "type": "destacado",
      "hidden": false,
      "label": "Primera consulta",
      "title": "Consulta de bienvenida",
      "text": "50 minutos para ordenar tu alimentación y salir con un plan que puedas sostener en tu día a día.",
      "button": { "text": "Reserva tu turno", "url": "https://example.com/reservas" }
    },
    {
      "id": "boletin1",
      "type": "tarjeta",
      "hidden": false,
      "label": "Newsletter",
      "title": "Comer bien sin culpa",
      "highlight": "sin culpa",
      "text": "Una receta simple y una idea por semana. Llega los domingos.",
      "button": { "text": "Quiero recibirlo", "url": "https://example.com/boletin", "icon": "mail" }
    },
    {
      "id": "podcast1",
      "type": "fila",
      "hidden": false,
      "icon": "headphones",
      "title": "Podcast Mesa de lunes",
      "text": "Charlas cortas para empezar la semana.",
      "url": "https://example.com/podcast",
      "verified": false,
      "style": "solido"
    },
    {
      "id": "taller01",
      "type": "fila",
      "hidden": false,
      "icon": "calendar",
      "title": "Talleres de cocina en vivo",
      "text": "Grupos chicos, una vez al mes.",
      "url": "https://example.com/talleres",
      "verified": false,
      "style": "borde"
    },
    {
      "id": "guias001",
      "type": "libros",
      "hidden": false,
      "label": "Guías gratis",
      "groups": [
        {
          "title": "Para empezar",
          "layout": "destacado",
          "items": [
            {
              "title": "Súper sin dudas",
              "cover": "https://example.com/portadas/super.jpg",
              "url": "https://example.com/guias/super",
              "linkText": "Descargar la guía"
            }
          ]
        }
      ],
      "more": { "text": "Ver todas las guías", "url": "https://example.com/guias" }
    },
    {
      "id": "redes001",
      "type": "redes",
      "hidden": false,
      "items": [
        { "network": "instagram", "url": "https://example.com/renata-instagram" },
        { "network": "youtube", "url": "https://example.com/renata-youtube" },
        { "network": "email", "url": "mailto:hola@example.com" }
      ]
    }
  ],
  "footer": "Hecha con la plantilla gratis de imagineAI"
}
```

---

**FILE: `skill/personal-web/examples/sample-brand/examples.json`**

FORMAT REFERENCE ONLY, not for deployment: Fictional sample for Renata Olmos. The `example.com` links, copy, and data are synthetic and must never be copied to a real person's website.

```json
{
  "version": 1,
  "blocks": {
    "destacado": {
      "id": "ejdest01",
      "type": "destacado",
      "hidden": false,
      "label": "Primera consulta",
      "title": "Consulta de bienvenida",
      "text": "50 minutos para ordenar tu alimentación y salir con un plan que puedas sostener en tu día a día.",
      "button": { "text": "Reserva tu turno", "url": "https://example.com/reservas" }
    },
    "tarjeta": {
      "id": "ejtarj01",
      "type": "tarjeta",
      "hidden": false,
      "label": "Newsletter",
      "title": "Comer bien sin culpa",
      "highlight": "sin culpa",
      "text": "Una receta simple y una idea por semana. Llega los domingos.",
      "button": { "text": "Quiero recibirlo", "url": "https://example.com/boletin", "icon": "mail" }
    },
    "fila": {
      "id": "ejfila01",
      "type": "fila",
      "hidden": false,
      "icon": "headphones",
      "title": "Podcast Mesa de lunes",
      "text": "Charlas cortas para empezar la semana.",
      "url": "https://example.com/podcast",
      "verified": false,
      "style": "solido"
    },
    "libros": {
      "id": "ejlibr01",
      "type": "libros",
      "hidden": false,
      "label": "Guías gratis",
      "groups": [
        {
          "title": "Para empezar",
          "layout": "fila",
          "items": [
            { "title": "Súper sin dudas", "author": "Renata Olmos", "cover": "https://example.com/portadas/super.jpg", "url": "https://example.com/guias/super" },
            { "title": "Desayunos simples", "author": "Renata Olmos", "cover": "https://example.com/portadas/desayunos.jpg", "url": "https://example.com/guias/desayunos" },
            { "title": "Cenas en 20 minutos", "author": "Renata Olmos", "cover": "https://example.com/portadas/cenas.jpg", "url": "https://example.com/guias/cenas" }
          ]
        }
      ],
      "more": { "text": "Ver todas las guías", "url": "https://example.com/guias" }
    },
    "redes": {
      "id": "ejredes1",
      "type": "redes",
      "hidden": false,
      "items": [
        { "network": "instagram", "url": "https://example.com/renata-instagram" },
        { "network": "youtube", "url": "https://example.com/renata-youtube" },
        { "network": "email", "url": "mailto:hola@example.com" }
      ]
    }
  }
}
```
