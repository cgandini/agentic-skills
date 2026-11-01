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
