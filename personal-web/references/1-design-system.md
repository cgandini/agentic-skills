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
