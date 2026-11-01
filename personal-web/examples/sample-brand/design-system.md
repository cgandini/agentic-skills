# Renata Olmos: Design System (Specification for AI)

Fictional example for the `personal-web` skill. Renata Olmos is an invented persona: she does not exist, and her website and social accounts are synthetic (`example.com` domains). The simulated sources below demonstrate what the skill extracts for a real person.
Simulated sources: Her website (homepage and booking page) and 6 Instagram screenshots. Where website and Instagram diverge, Instagram takes precedence.

## General Aesthetic Rules

Fresh, airy, and grounded. A single action color (sage green), dark forest ink (never pure black), warm bone canvas, and crisp white card surfaces. Warm serif headlines paired with handwritten accent text for human voice. Minimal shadows. Zero emojis on page.

## Colors

Core palette:

| Name | Hex | Origin | Role |
|---|---|---|---|
| Sage green | `#2F855A` | Website buttons, Instagram recipe cards | Primary button, icon discs, underlines, arrows |
| Mint green | `#9ADBB4` | Accent details on dark cards | Dark surfaces only: label tag and checkmark. Never on light |
| Ink | `#1F2A24` | Headlines and dark promo cards | Strong typography, dark hero blocks. Never pure black |
| Bone | `#F2EEE4` | Website canvas and card background | Page background canvas |
| White | `#FFFFFF` | Website cards | Card surfaces and light text over dark surfaces |
| Deep green | `#276749` | Derived accessibility tone | Highlighted word in large display text, button hover end |

Supporting neutrals: Body text `#3A453F`, Gray `#5A6660`, Surface border `#E4E0D6`, Canvas border `#D8D2C3`.

Accessibility-derived tones:
- Deep green `#276749`: Same hue family as sage green (hue 152 vs 150), darkened to achieve compliant contrast on display text.
- Small copy never uses accent color: Rendered in ink (`#1F2A24`) or body text (`#3A453F`), with green reserved for underlines, arrows, or icon discs.
- Button hover gradient: Transitions from `#2F855A` to `#276749` to preserve white label contrast during interaction.

Contrast Matrix:

| Combination | Ratio | Context |
|---|---|---|
| `#1F2A24` on `#F2EEE4` | 12.81:1 | Name and primary headings |
| `#3A453F` on `#FFFFFF` | 9.99:1 | Card body text |
| `#5A6660` on `#F2EEE4` | 5.17:1 | Role and subtitles |
| `#5A6660` on `#FFFFFF` | 5.99:1 | Row descriptions |
| White on `#1F2A24` | 14.84:1 | Dark hero card (`destacado`) |
| `#9ADBB4` on `#1F2A24` | 9.30:1 | Label tag and checkmark on dark card |
| White on `#2F855A` | 4.54:1 | Primary button text |
| `#276749` on `#F2EEE4` | 5.80:1 | Profile phrase (large text) |
| `#276749` on `#FFFFFF` | 6.73:1 | Card title (large text) |
| `#2F855A` on `#F2EEE4` | 3.92:1 | Decorative: underlines and arrows |

## Typography (Google Fonts)

```html
<link href="https://fonts.googleapis.com/css2?family=Fraunces:wght@700;800&family=Nunito+Sans:wght@400;500&family=Caveat:wght@400&display=swap" rel="stylesheet">
```

| Role | Font Family | Weights | Usage |
|---|---|---|---|
| Headings | **Fraunces** | 700, 800 | Uppercase name, headings, buttons, tags |
| Body | **Nunito Sans** | 400, 500 | Body paragraphs, descriptions, role |
| Accent | **Caveat** | 400 | Profile hook phrase and card titles only |

Three typefaces total, with the accent font used strictly in two display locations.

## Borders and Details

| Property | Value |
|---|---|
| Card and row radius | `14px` |
| Borders | 1 px `#E4E0D6` on white; `#D8D2C3` on canvas background |
| Canvas texture | Bone background with subtle SVG noise texture (`grain: true`) |
| Shadows | Minimal: soft shadow on book covers only |

## Component Styling

- **Primary Button** (on dark hero card): `#2F855A` background, white text, Fraunces 700 pill shape. Hover transitions to `#276749`.
- **Card**: White surface, hairline border, Caveat title with highlighted keyword in deep green and underlined in sage green.
- **Row**: Icon in sage green disc (`solido`) or hairline outline (`borde`).
- **Text Links**: Ink text, 2 px sage green underline, trailing green arrow.

## Voice and Tone

Speaks directly to one individual rather than broadcasting to a crowd. Supportive and practical, avoiding extreme diet claims, guilt, or hyperbole.
- Hooks reframe beliefs: "Eating well does not have to be complicated."
- Concrete numbers: "50 minutes", "20 minutes".
- Grounded imagery: cutting boards, Sunday grocery routines.
- Emojis: Zero on website.

## Template Mapping

`theme.json`: `fondo` `#F2EEE4`, `superficie` `#FFFFFF`, `tinta` `#1F2A24`, `texto` `#3A453F`, `gris` `#5A6660`, `borde` `#E4E0D6`, `bordeFondo` `#D8D2C3`, `acento` `#2F855A`, `acentoTexto` `#276749`, `acentoSuave` `#9ADBB4`, `gradiente` from `#2F855A` to `#276749`, `aroFoto` from `#9ADBB4` to `#2F855A`; fonts Fraunces, Nunito Sans, and Caveat; `grain: true`; `radius: 14`.

## Open Items

- Typefaces are Google Fonts equivalents matching source screenshots.
- Swatches were measured from compressed imagery.
- Sample links use `example.com` domains; production deployments must replace them with authentic user destinations.
