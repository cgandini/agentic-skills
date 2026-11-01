# Phase 4: Install with an AI Agent (Route B: Agentic IDE & Route C: Terminal CLI)

**Goal:** Deploy the personal web and admin panel to Cloudflare Pages and D1 for free. The AI agent executes commands and writes files directly in the workspace; the user performs account creation and provides authorization.

**Deliverables:** Live personal micro-web on Cloudflare Pages, a functional `/admin/` panel accessible via password, and one verified test update published.

Reference for manual browser clicks: `references/5-install-from-browser.md`.

## Coverage: Route B vs. Route C

- **Route B — Agentic IDEs (Google Antigravity, Cursor, Windsurf, VS Code with Claude Code / Codex):**
  The user is inside a desktop IDE with an active workspace. You write `brand/theme.json`, `brand/seed.json`, and `brand/examples.json` directly into the repository files, run `npm test` to verify integrity, and guide the deployment. If the user prefers web UI over CLI authentication, guide them through browser clicks in `references/5-install-from-browser.md`. If they prefer CLI, execute the wrangler commands below.
- **Route C — Terminal / CLI Agents (Claude Code CLI, Codex CLI, Gemini CLI):**
  Execute the terminal workflow (`gh repo create`, `wrangler d1`, `npm test`, git push, `wrangler pages secret put`).

## Responsibilities

| Agent (Workspace & Terminal) | User (Browser & Secret Input) |
|---|---|
| Check Node/Git versions, clone template, write `brand/` | Create GitHub and Cloudflare accounts |
| Run `wrangler d1 create`, update `wrangler.toml` | Click **Allow** when `wrangler login` launches browser |
| Verify locally (optional), commit, and push | Authorize Pages GitHub app integration |
| Run validation and verification curl checks | Run commands that prompt for hidden secrets (`PANEL_PASSWORD`, `DEPLOY_HOOK_URL`) |

## Operational Rules

- **One action per message:** Explain what each step accomplishes before executing or asking the user to act.
- **Strict secrets privacy:** Never display, log, or accept `PANEL_PASSWORD`, `CLOUDFLARE_API_TOKEN`, or `DEPLOY_HOOK_URL` in chat. When a command requires a secret, the user executes it in their own terminal or inputs it directly in Cloudflare.
- **Zero payment credentials:** The entire architecture is 100% free. If a screen asks for a credit card, halt immediately.
- **Deterministic naming:** Use a single lowercase alphanumeric identifier `NAME` (e.g. `ana-web`) across the GitHub repository, D1 database, and Cloudflare Pages project.

---

## Step 1: Environment Check

Verify runtime prerequisites:

```bash
node --version
git --version
gh --version
```

- **Node.js must be version 20 or higher** (v20, v22...). If outdated, direct the user to install the current LTS release from nodejs.org.
- **Git** is required.
- **`gh` (GitHub CLI)** is optional. If present, verify with `gh auth status`. If unauthenticated, the user logs in with `gh auth login`.

## Step 2: Account Preparation (User)

The user logs into their GitHub account (github.com) and Cloudflare account (dash.cloudflare.com). If new, they register using the Free plan.

## Step 3: Clone the Template Repository

With `gh` authenticated:

```bash
gh repo create NAME --template cgandini/personal-web --private --clone
cd NAME
npm ci
```

Without `gh`: The user visits `https://github.com/cgandini/personal-web`, clicks **Use this template** > **Create a new repository** (`NAME`, Private), and you clone it:

```bash
git clone https://github.com/USER/NAME.git
cd NAME
npm ci
```

Ensure `package-lock.json` exists before running `npm ci`.

## Step 4: Write `brand/` Files

1. Write `brand/theme.json`, `brand/seed.json`, and `brand/examples.json` using the data finalized in Phase 3.
2. Keep `brand/images/` unchanged: it provides bundled placeholders (`perfil` and `tapa`). The user will upload their real photos via the mobile `/admin/` panel later.
3. Run the validation checks from `references/3-brand-files.md`. All checks must report `OK`.

## Step 5: Authenticate Cloudflare via Wrangler

Wrangler communicates with Cloudflare APIs. The user executes:

```bash
npx wrangler login
```

A browser window opens; the user clicks **Allow**. (In headless or remote sessions, use `npx wrangler login --device`). Confirm identity:

```bash
npx wrangler whoami
```

If multiple accounts are listed, copy the relevant **Account ID** and export it:

```bash
# macOS / Linux
export CLOUDFLARE_ACCOUNT_ID="YOUR_ACCOUNT_ID"
# Windows PowerShell
$env:CLOUDFLARE_ACCOUNT_ID="YOUR_ACCOUNT_ID"
```

## Step 6: Create D1 Database and Update `wrangler.toml`

```bash
npx wrangler d1 create NAME
```

When prompted whether to automatically write to configuration, choose **No**. Copy the printed `database_id`. Update `wrangler.toml`:

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

Do not execute `migrations apply` or `seed.mjs` on remote: database schema initialization and initial seeding are performed automatically by the **"Preparar mi página"** action in the admin panel.

## Step 7 (Optional): Local Development Preview

```bash
cp .dev.vars.example .dev.vars
npm run build:local
npm run dev
```

- With `DEV_NO_AUTH=1` in `.dev.vars`, the admin panel at `http://127.0.0.1:8788/admin/` opens without requiring a password.
- Visit `http://127.0.0.1:8788/admin/` and click **"Preparar mi página"** to load the database.
- In a second terminal, run `npm run build:local` and refresh `http://127.0.0.1:8788` to inspect the generated static page. Terminate the dev server with `Ctrl+C`. Never expose local servers through public tunnels.

## Step 8: Commit and Push to GitHub

```bash
git status -sb
git add -A brand wrangler.toml
git commit -m "feat: configure personal brand"
git push
```

Verify that `.dev.vars` and `node_modules` remain untracked.

## Step 9: Cloudflare Pages Project Setup (Browser)

The user navigates to Cloudflare dashboard > **Workers & Pages** > **Create application** > **Pages** > **Connect to Git**:

1. Select repository `NAME`.
2. Configure build settings:
   - **Project name:** `NAME`
   - **Production branch:** `main`
   - **Framework preset:** `None`
   - **Build command:** `npm ci && node scripts/build.mjs --remote`
   - **Build output directory:** `public`
3. Add two environment variables as **Secret (Encrypt)**:
   - `CLOUDFLARE_ACCOUNT_ID`: Account ID from dashboard.
   - `CLOUDFLARE_API_TOKEN`: API token created under **My Profile** > **API Tokens** > **Create Token** > **Custom token** with permission **Account · D1 · Read**.
   - Note: If **Settings > Builds** shows **Build variables and secrets**, verify that `CLOUDFLARE_ACCOUNT_ID` and `CLOUDFLARE_API_TOKEN` are present as encrypted secrets so build containers reliably access them.
   - Note: In **Settings > Bindings**, `DB` is managed automatically via `wrangler.toml` in read-only mode.
4. Click **Save and Deploy**. The initial build will produce a placeholder page stating `"Página en preparación"`.

## Step 10: Configure `PANEL_PASSWORD`

Explain password creation: pick 4 unrelated words separated by hyphens (at least 12 characters total). The user executes locally:

```bash
npx wrangler pages secret put PANEL_PASSWORD --project-name NAME
```

The user inputs the password privately in the prompt. The secret is encrypted directly into Cloudflare.

## Step 11: Trigger Deploy and Setup Deploy Hook

1. The user navigates to **Settings > Builds** (or Builds & deployments) > **Deploy hooks** > **Add deploy hook**:
   - Name: `panel`
   - Branch: `main`
   - Copy the secret URL (starts with `https://api.cloudflare.com/`).
2. Add `DEPLOY_HOOK_URL` as a secret:

```bash
npx wrangler pages secret put DEPLOY_HOOK_URL --project-name NAME
```

3. Trigger a fresh deployment so all secrets take effect:

```bash
git commit --allow-empty -m "chore: redeploy with secrets"
git push
npx wrangler pages deployment list --project-name NAME
```

In Cloudflare, go to **Settings > Builds > Branch control** and disable preview branch deployments.

## Step 12: Initialize Database via Admin Panel

1. Open `https://NAME.pages.dev/admin/` in a browser.
2. Enter `PANEL_PASSWORD`.
3. In the setup screen, click **"Preparar mi página"** (displays "Preparando…"). This initializes database tables, populates `brand/seed.json`, and queues the initial static build.
4. Within 1 to 2 minutes, the header will display **"Tu página está al día"**.
5. Open `https://NAME.pages.dev` on a mobile phone to confirm the live layout.

## Step 13: Final Verification

Run automated HTTP checks:

```bash
curl -sI https://NAME.pages.dev/ | head -1
curl -sI https://NAME.pages.dev/nada | head -1
curl -sI https://NAME.pages.dev/admin/ | head -1
```

Expected responses:
- `/`: HTTP `200`
- `/nada`: HTTP `404` (rendering brand 404 page)
- `/admin/`: HTTP `200` (rendering login screen)

Have the user verify:
1. Site loads cleanly on a mobile browser.
2. Entering an invalid password in `/admin/` displays `"La contraseña no es correcta."`.
3. Logging in from a second device (phone and desktop) registers device cookies for rate-limit protection.
4. Making an edit in `/admin/` and clicking **"Publicar"** updates the live page within 2 minutes.

Transition to `references/6-daily-use.md`.
