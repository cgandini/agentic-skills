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
