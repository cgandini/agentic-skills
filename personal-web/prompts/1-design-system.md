# Prompt 1: Brand Design System

Use this standalone prompt in any AI chat assistant (claude.ai, gemini.google.com, chatgpt.com) to extract your personal brand design system without loading the full skill. It outputs your brand guidelines as an inspection artifact and a reusable specification file.

## Instructions

1. Gather: Your website link (if any) and 4 to 6 screenshots of your Instagram feed (profile view and recent posts).
2. Copy the prompt block below.
3. Replace the placeholder values in [BRACKETS] with your details.
4. Paste the prompt into your chat assistant and attach your screenshots.
5. Review the proposed design system. Request adjustments to colors, fonts, or voice until satisfied, then save the final file.

## Prompt

```
I want to create a design system for my personal brand. My name is [YOUR NAME] and I specialize in [WHAT YOU DO, IN ONE SENTENCE].

Review my website at [LINK TO YOUR WEBSITE, or write "I do not have a website"], and inspect the attached Instagram screenshots. Extract my authentic visual identity without inventing an ungrounded style:
- A core palette of 4 to 6 colors, including hexadecimal values and functional roles for each.
- Two Google Fonts typefaces (one for headlines, one for body copy) that match my current aesthetic, plus one optional accent font for display phrases.
- Type scales, spacing, border radiuses, and shadow treatments.
- Component styling for buttons, cards, and link rows.
- Voice and tone rules [REGISTER: e.g. formal English, casual direct, or Spanish voseo/tuteo].

Rules to follow:
1. Extract authentic patterns rather than inventing new aesthetics. If my website and Instagram diverge, state which you prioritized and why.
2. One clear action color. The ink color must be near-black, never pure #000000.
3. Warm or light accent colors frequently fail accessibility contrast on small text. Reserve the accent color for underlines, glyphs, arrows, and badges; use ink or gray for small copy. If applying the accent color to display headlines (>=24 px), adjust lightness slightly while preserving hue and saturation.
4. Calculate contrast ratios for every text/surface combination in a structured matrix. Small text requires >=4.5:1; large display text requires >=3.0:1.
5. Maximum three typefaces, all available in Google Fonts.
6. Do not fabricate metrics or social proof.
7. Zero emojis on the site; use SVG icons only.
8. Note any items requiring confirmation (e.g. font approximations or compression artifacts from screenshots).

Present the design system in a review artifact, and deliver the final specification as a file I can save and reuse.
```

## Next Steps

Use the generated design system as the input for `2-static-page.md`. If you also want a mobile admin panel to edit your links from your phone, use the complete `personal-web` skill (`SKILL.md`).
