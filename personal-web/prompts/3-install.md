# Prompt 3: Deploy Your Personal Web

Use this standalone prompt in a browser chat (claude.ai, gemini.google.com, chatgpt.com) when you already have your brand files (`theme.json`, `seed.json`, and `examples.json`) and want step-by-step guidance to deploy your personal micro-web on Cloudflare for free, complete with a mobile admin panel.

If you do not yet have those three JSON files, start with `CHAT-PROMPT.md` (or `FOR-CHAT.md`), which guides you from scratch. Prompt 2 produces a fixed static HTML file without an admin CMS.

## Instructions

1. Open a new AI chat session.
2. Copy the prompt below, replace the values in [BRACKETS], and send it as your first message.
3. Attach (or paste) `references/5-install-from-browser.md` from the template repository (`https://github.com/cgandini/personal-web`) along with your three brand files. If the AI can read web links, providing the template URL is sufficient.
4. Follow instructions one step at a time. If screens differ, share a screenshot.
5. Create your admin password privately and store it securely; never send passwords or tokens to the AI.

## Prompt

```
I want to deploy my personal web to the internet on Cloudflare, completely free without a credit card, and have a mobile admin panel to edit it from my phone. I already have my brand configuration files (theme.json, seed.json, and examples.json); I will upload real photos later via the admin panel. I do not have a technical background: explain each step in plain words on first mention.

Guide me step-by-step following the guide "5-install-from-browser.md" (from the template https://github.com/cgandini/personal-web). If you do not have it accessible, ask me for it before starting.

Rules:
1. Provide only one step per message and wait for my confirmation before continuing. Before every action, explain what I should see next and what to do if the screen differs.
2. We are operating entirely in browser interfaces: you guide conversationally and provide code snippets; I perform all clicks and paste operations. When files need editing, provide the full file contents in a code box to copy and paste directly into GitHub. I am performing the installation on a desktop computer.
3. Never ask for or accept passwords, API tokens, account IDs, or secret URLs in chat. My admin password will be created by me privately (4 unrelated words separated by hyphens, 12+ characters) and entered directly into Cloudflare. The database ID is not secret and may be shared.
4. Never ask for a credit card. If any screen prompts for payment details, tell me to stop and explain which screen it is.
5. Speak in plain English without emojis.

Project details: [YOUR NAME OR BRAND]. The identifier I want for my repository, database, and project is [NAME-IN-LOWERCASE, e.g. ana-web].

Let's begin: explain what we will accomplish in two sentences and provide the first step.
```

## Next Steps

Once installation completes, verify on your mobile phone: ensure the site loads, `/admin/` prompts for your password, and publishing a test edit updates the live site within 1 to 2 minutes. For ongoing operations, see `references/6-daily-use.md`.
