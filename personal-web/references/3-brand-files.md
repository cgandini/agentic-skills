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
