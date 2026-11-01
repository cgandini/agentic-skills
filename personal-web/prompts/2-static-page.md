# Prompt 2: Static Personal Web

Use this standalone prompt to generate a single-file static HTML personal micro-web using the design system created with Prompt 1. This produces a fixed HTML file. If you want a mobile admin panel (`/admin/`) to update links and photos directly from your phone, use the complete `personal-web` skill (`SKILL.md`).

## Instructions

1. Have your design system specification (from Prompt 1) and your portrait photo ready.
2. Copy the prompt below and replace all values in [BRACKETS].
3. If you do not have certain elements (e.g. books or publications), delete those lines completely.
4. List your links in descending order of priority: the first link should represent your single most important call to action.
5. Paste the prompt into chat, attaching your design system and photo.
6. Test the resulting page on a mobile device and refine copy or layout as desired.

## Prompt

```
Using the attached design system for [YOUR NAME], build a personal micro-web for mobile devices in a single self-contained HTML file. It must feel like an authentic reflection of my brand rather than a generic link aggregator.

Order the links by conversion hierarchy rather than an unweighted vertical list. If you see opportunities to improve the flow based on my design system, propose them with a one-sentence rationale for each.

1. Top header: My photo (attached), my name ([YOUR NAME]), my role ([YOUR ROLE · SPECIALTY]), and a short hook phrase matching my tone.
2. Primary featured offer: [PRIMARY OFFER] ([LINK]) with a direct action button: [BUTTON TEXT, e.g. "Book a Session"].
3. High-value secondary offer: [SECONDARY OFFER, e.g. newsletter or free guide] ([LINK]), with a clear button for [ACTION].
4. Secondary destination: [OTHER DESTINATION, e.g. WhatsApp channel or podcast] ([LINK]).
5. Publications / Media covers:
   - [FIRST TITLE]: [LINK]
   - [SECOND TITLE]: [LINK]
6. Footer social links: [NETWORK 1] ([LINK]), [NETWORK 2] ([LINK]), [NETWORK 3] ([LINK]).

Small footer note: [FOOTER COPY, or omit this line].

Rules:
- Use only the verified links provided. Do not fabricate URLs, statistics, or testimonials.
- Small text must not use the accent color; use dark ink. Accent colors are reserved for underlines, arrows, and glyphs.
- Zero emojis: use icons.
- Typefaces must match the Google Fonts specified in the design system.
- Ensure perfect responsive rendering on a 390 px mobile viewport with fast load times.
- External links must open in a new tab.
```

## Next Steps

Verify that each link opens correctly. To host this static page for free, save the file as `index.html` in an empty folder on your computer. In Cloudflare (`cloudflare.com`), navigate to **Workers & Pages** > **Create** > **Pages** tab > **Upload assets**, drag and drop the folder, and deploy. If you prefer a live mobile admin panel (`/admin/`) to manage content, use `CHAT-PROMPT.md` or `SKILL.md`.
