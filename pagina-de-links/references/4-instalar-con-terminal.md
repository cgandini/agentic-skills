# Fase 4, ruta A: instalar con terminal

**Objetivo:** poner la página y el panel en internet, gratis. Vos ejecutás los comandos y escribís los archivos; la persona hace **todas las acciones de cuenta** en su navegador.

**Entregable:** la página abre en el celular, `/admin/` pide la contraseña y la persona publicó un cambio de prueba. Lleva **entre 2 y 3 horas en total** y se puede hacer en dos o tres sesiones.

**Cargá también `references/5-instalar-sin-terminal.md`**: las partes que se hacen en el dashboard de Cloudflare (token, proyecto de Pages, variables, deploy hook, dominio) están ahí, con el paso a paso para una persona sin experiencia. Esta guía dice cuándo usarlas.

## Qué hacés vos y qué hace la persona

| Vos (con la terminal) | La persona (en el navegador o tecleando ella) |
|---|---|
| Revisar Node, traer la plantilla, escribir `brand/` | Crear la cuenta de GitHub y la de Cloudflare |
| `wrangler d1 create`, editar `wrangler.toml` | Tocar **Allow** cuando `wrangler login` abre el navegador |
| Vista previa local, `git commit` y `git push` | Conectar Pages con GitHub (wrangler **no** puede crear un proyecto conectado a Git) |
| Verificar con `curl` y `wrangler pages deployment list` | Crear el token y las variables en Cloudflare |
| | **Correr ella** los comandos que piden un valor oculto (`gh auth login`, `wrangler login` si lo pide, `wrangler pages secret put`) y escribir ahí la contraseña y la URL del deploy hook |

## Reglas para vos en esta fase

- **Un paso por mensaje, y esperá.** Antes de cada comando decí en una frase qué hace; antes de cada acción de la persona decí qué va a ver y qué hacer si ve otra cosa. En los botones de Cloudflare y GitHub agregá "si no ves exactamente este botón, buscá uno parecido o mandame una captura".
- **Si una pantalla pide tarjeta o método de pago, frená** y avisale a la persona. No se paga nada en este camino.
- **No escribas ni veas la contraseña del panel, el token ni la URL del deploy hook.** Todo comando que pide un valor oculto en un prompt (`wrangler pages secret put ...`, `gh auth login`, `wrangler login` si pregunta algo) **lo corre la persona en su propia terminal, nunca vos**: si lo corrieras vos, el valor pasaría por esta conversación. En Claude Code se hace escribiendo `!` seguido del comando (por ejemplo `! npx wrangler pages secret put PANEL_PASSWORD --project-name NOMBRE`); en otra herramienta, que abra su terminal y lo pegue. Decile "No me escribas el valor a mí". Nunca los guardes en un archivo ni los muestres en pantalla. Nunca pongas secretos en `progreso.md`.
- **Después de cada paso**, actualizá `progreso.md` con una línea (`Etapa de instalación (n de 12)`, `NOMBRE`, `Usuario de GitHub`, `Database ID` cuando exista; ver `SKILL.md`).
- **Un solo nombre para todo:** `NOMBRE` (`links` o `<nombre>-links`, minúsculas, guiones, sin tildes) para el repositorio, la base de datos y el proyecto de Pages.
- Trabajá en la carpeta que la persona elija (por ejemplo `Documentos`) y no toques nada fuera de ella.

---

## Paso 1: revisar las herramientas

```bash
node --version
git --version
gh --version
```

- **Node tiene que ser 20 o más** (v20, v22...). Si no está o es más viejo: guiá a la persona a **nodejs.org**, que descargue la versión **LTS**, la instale con todo por defecto y **cierre y vuelva a abrir** la terminal. Repetí `node --version`.
- **Git** es necesario. Si falta, guiala a **git-scm.com/downloads** (en Mac, la terminal ofrece instalarlo sola).
- **`gh`** (el programa de GitHub) es opcional. Si está, comprobá `gh auth status`: si dice que no iniciaste sesión, la persona tiene que correr ella `gh auth login` (con `!` en Claude Code) y seguir las preguntas en el navegador.

## Paso 2: cuentas (la persona)

- **GitHub:** etapa 1 de `5-instalar-sin-terminal.md`.
- **Cloudflare:** etapa 4 del mismo archivo. Si pide tarjeta, frená.

Control: "¿Tenés cuenta en GitHub y en Cloudflare, y las dos ya iniciadas en el navegador?"

## Paso 3: traer la plantilla

Con `gh` instalado y con sesión iniciada (usando la plantilla `cgandini/tu-pagina-de-links` indicada en `SKILL.md`):

```bash
gh repo create NOMBRE --template cgandini/tu-pagina-de-links --private --clone
cd NOMBRE
```

Sin `gh`: la persona hace la etapa 2 de `5-instalar-sin-terminal.md` (Use this template) y vos clonás su repositorio:

```bash
git clone https://github.com/SU-USUARIO/NOMBRE.git
cd NOMBRE
```

Después, siempre dentro de la carpeta `NOMBRE`:

```bash
npm ci
```

Comprobá que existe `package-lock.json` (si no, `npm ci` falla). Si `npm ci` muestra avisos amarillos (`warn`), no son errores.

## Paso 4: escribir `brand/`

1. Escribí `brand/theme.json`, `brand/seed.json` y `brand/examples.json` con lo de la fase 3 (reemplazan a los de la plantilla).
2. **No toques `brand/images/`**: trae dos fotos de relleno (`perfil` y `tapa`) y los JSON nombran solo esas. La persona sube las suyas desde el panel después (etapa 11 de `5-instalar-sin-terminal.md`). Solo si ya las tiene preparadas y quiere instalarlas desde el principio, seguí el camino opcional de `references/3-archivos-de-marca.md` (nombre = id, menos de 400 KB).
3. Corré las validaciones de `references/3-archivos-de-marca.md` (sección "Ruta A"). Todas tienen que dar `OK`.

## Paso 5: entrar a Cloudflare con wrangler

`wrangler` es el programa que habla con Cloudflare. Avisale a la persona que se va a abrir una pestaña del navegador y que tiene que tocar **Allow**. El comando lo corre ella (en Claude Code, `!` y el comando), porque abre el navegador y puede preguntar cosas:

```bash
npx wrangler login
```

Si no se abre el navegador o la página no carga (por ejemplo en una conexión remota), probá con `npx wrangler login --device`. Después:

```bash
npx wrangler whoami
```

Tiene que mostrar el mail de la persona y su cuenta. **Si muestra más de una cuenta**, anotá el **Account ID** de la que va a usar y poné esta variable **antes de cada comando de wrangler** (wrangler 4 no acepta `account_id` dentro de `wrangler.toml`):

```bash
# Mac y Linux
export CLOUDFLARE_ACCOUNT_ID=ID-DE-LA-CUENTA
# Windows (PowerShell)
$env:CLOUDFLARE_ACCOUNT_ID="ID-DE-LA-CUENTA"
```

La variable vale solo mientras la terminal esté abierta.

## Paso 6: crear la base de datos y completar `wrangler.toml`

```bash
npx wrangler d1 create NOMBRE
```

Si pregunta si querés que wrangler agregue la base a tu configuración, respondé que **no** (el archivo se escribe a mano). Copiá el `database_id` que imprime (no es un secreto). Reemplazá `wrangler.toml` por esto, con los tres valores completados. Si el del repositorio trae algo más, conservalo:

```toml
name = "NOMBRE"
pages_build_output_dir = "public"
compatibility_date = "2026-10-01"

[[d1_databases]]
binding = "DB"
database_name = "NOMBRE"
database_id = "EL-ID-QUE-IMPRIMIO-WRANGLER"
migrations_dir = "migrations"
```

Si dice que la base ya existe, la persona la creó antes: usá el ID de esa (`npx wrangler d1 info NOMBRE`).

**No corras `migrations apply` ni `seed.mjs` contra la base de internet.** Las tablas y el contenido inicial los carga el botón **Preparar mi página** del panel (paso 12), igual que en la ruta sin terminal. (`scripts/seed.mjs` y `scripts/migrate.mjs` quedan en el repositorio para quien mantiene la plantilla; no son parte de esta instalación.)

## Paso 7 (opcional): verla en la computadora antes de subir

Sirve para que la persona vea su marca sin esperar a internet. Si hay apuro, saltalo. La base local arranca vacía y se carga con el mismo botón **Preparar mi página** que se usa en internet (no se migra ni se siembra a mano).

```bash
cp .dev.vars.example .dev.vars
npm run build:local
npm run dev
```

- `.dev.vars` trae `DEV_NO_AUTH=1`: en la computadora (y solo ahí) el panel abre sin pedir contraseña. No hace falta tocarlo.
- `npm run build:local` deja las fotos de `brand/images/` en `public/_brand/` (las lee el botón) y escribe una página "Página en preparación": con una base vacía, es lo esperado. Tiene que terminar con `Página generada (todavía no hay nada publicado): public/index.html = página en preparación.`
- `npm run dev` queda andando en esa terminal. Si hace falta otra, abrí una aparte para lo que sigue.

Mostrale a la persona **http://127.0.0.1:8788/admin/**: tiene que ver "Tu página todavía no está preparada". Que toque **Preparar mi página**: tiene que aparecer "Tu página" con sus bloques. En local no hay aviso automático, así que el panel dice "falta configurar la actualización automática": es lo esperado. Después, en la otra terminal:

```bash
npm run build:local
```

Esta vez termina con `Página generada: public/index.html ... KB, N imágenes en public/i/, publicado ...`. Mostrale **http://127.0.0.1:8788** (la página con su marca). Cada cambio que publique en el panel local se ve después de repetir `npm run build:local` y recargar. Para cortar, `Ctrl+C` en la terminal del servidor. **Nunca expongas este servidor con un túnel.** Esta base local no se sube: la de internet se prepara después desde el panel, con el mismo botón.

Para empezar la vista previa de cero, cortá el servidor y borrá la carpeta `.wrangler`. (`npm run db:migrate:local` y `npm run db:seed:local` existen para quien mantiene la plantilla; en esta guía no hacen falta.)

## Paso 8: subir los archivos a GitHub

```bash
git status -sb
git add -A brand wrangler.toml
git commit -m "feat: mi marca"
git push
```

- Antes de commitear, comprobá con `git status -sb` que no entran carpetas como `node_modules` ni `.dev.vars` (están ignoradas) ni nada que la persona no reconozca.
- Si `git commit` dice que no sabe quién sos, preguntale a la persona su nombre y su mail de GitHub y corré `git config user.name "..."` y `git config user.email "..."` (sin `--global`).
- Si `git push` pide usuario y contraseña, no uses la contraseña de GitHub: que la persona corra ella `gh auth login` (con `!` en Claude Code) o te diga si prefiere otra forma.

## Paso 9: proyecto de Pages (la persona, en el navegador)

Seguí **las etapas 6, 7a, 7b y 7c de `5-instalar-sin-terminal.md`** (el proyecto de Pages conectado a GitHub y el token, que se crea en la 7c con el campo de la variable abierto al lado) con estas diferencias:

- **Cargá solo dos variables en el dashboard, las dos como Secret (Encrypt):** `CLOUDFLARE_ACCOUNT_ID` y `CLOUDFLARE_API_TOKEN`. La contraseña y el deploy hook van por la terminal (pasos 10 y 11).
- El **Project name** es `NOMBRE`, igual que el `name` de `wrangler.toml`.
- Si el primer build falla porque todavía no están las dos variables, es esperado; si la pantalla trae "Environment variables (advanced)", cargalas ahí y no falla.
- Si en la pantalla de Cloudflare en **Settings > Builds** ves una sección separada llamada **Build variables and secrets** (o si el log del deploy dice que no encuentra `CLOUDFLARE_API_TOKEN` durante `build.mjs`), cargá `CLOUDFLARE_ACCOUNT_ID` y `CLOUDFLARE_API_TOKEN` ahí también como secretos cifrados para que el contenedor de build los reciba siempre.

## Paso 10: la contraseña del panel (la persona escribe)

Explicale cómo se hace una buena contraseña: **elegí 4 palabras sin relación entre sí, por ejemplo mirando objetos de la habitación, separadas por guiones**, de al menos **12 caracteres** en total, distinta de las demás, y guardada en el administrador de contraseñas del celular o en una nota privada. Después, **que la persona corra** (en Claude Code, con `!` adelante):

```bash
npx wrangler pages secret put PANEL_PASSWORD --project-name NOMBRE
```

Decile: "Ahora te pide el valor. Escribilo vos en la terminal (no se ve mientras escribís) y apretá Enter. **No me lo escribas a mí.**" Tiene que terminar diciendo que el secreto se creó.

## Paso 11: primer deploy y deploy hook

Para que tome la contraseña y las variables, pedí un deploy nuevo sin cambiar nada:

```bash
git commit --allow-empty -m "chore: nuevo deploy"
git push
npx wrangler pages deployment list --project-name NOMBRE
```

Repetí el último comando cada medio minuto hasta que el más reciente diga éxito. Para ver el log, la persona abre en Cloudflare el proyecto > **Deployments** > ese deploy (ver la etapa 8 de `5-instalar-sin-terminal.md`): tiene que haber una línea `Página generada`. La página `https://NOMBRE.pages.dev` debe decir **"Página en preparación"**: es lo correcto todavía.

Ahora el deploy hook: la persona hace los pasos 1 a 3 de la **etapa 9** de `5-instalar-sin-terminal.md` (Settings > Builds, que puede llamarse Builds & deployments, > Deploy hooks: crearlo y copiar la URL, sin pegarla en el chat). Después:

```bash
npx wrangler pages secret put DEPLOY_HOOK_URL --project-name NOMBRE
```

Igual que antes, **lo corre ella** y pega la URL en el prompt. Pedí otro deploy:

```bash
git commit --allow-empty -m "chore: nuevo deploy"
git push
```

Apagá también los deploys de preview (paso 6 de la etapa 9; puede verse distinto): el panel no anda en sus direcciones, así que el panel se abre siempre desde `https://NOMBRE.pages.dev`, nunca desde una dirección de prueba.

## Paso 12: abrir el panel y preparar la página (la persona)

Etapas 10 y 11 de `5-instalar-sin-terminal.md`: entrar a `https://NOMBRE.pages.dev/admin/` con la contraseña, tocar **Preparar mi página** (es lo que crea las tablas y carga `brand/`; si muestra un aviso en rojo, la tabla de problemas de esa guía dice qué hacer), esperar 1 o 2 minutos, ver la página en el celular y publicar un cambio de prueba.

## Paso 13: verificar

Vos corrés lo que se puede desde la terminal:

```bash
curl -sI https://NOMBRE.pages.dev/ | head -1
curl -sI https://NOMBRE.pages.dev/nada | head -1
curl -sI https://NOMBRE.pages.dev/admin/ | head -1
```

La primera da `200`, la segunda `404` (con la página 404 de la marca, que la persona mira en el navegador) y la tercera `200` (la pantalla de entrada). El resto lo comprueba la persona:

- La página abre en el celular.
- `/admin/` pide la contraseña y una equivocada muestra "La contraseña no es correcta.".
- Publicar un cambio lo muestra en la página en 1 o 2 minutos.

Después, cierre de fase con el resumen de `SKILL.md` y `references/6-uso-diario.md`.

## Dominio propio (opcional)

Etapa 12 de `5-instalar-sin-terminal.md` (con subdominio; el dominio raíz queda fuera de esta guía).

## Cambiar la marca más adelante

Editá `brand/theme.json`, validalo y: `git add -A brand && git commit -m "feat: nuevos colores" && git push`. Cloudflare arma la página sola. **No vuelvas a preparar la página desde cero para cambiar la marca.**

## Si algo falla

La tabla de problemas de `5-instalar-sin-terminal.md` ("Si algo falla") sirve igual. Además:

| Lo que pasa | Causa probable | Qué hacer |
|---|---|---|
| `node: command not found` o versión menor a 20 | Falta Node o es viejo | Paso 1 |
| `wrangler login` no abre el navegador | Terminal remota o bloqueada | `npx wrangler login --device` |
| wrangler dice que hay más de una cuenta | Cuenta de trabajo y personal | Variable `CLOUDFLARE_ACCOUNT_ID` (paso 5) |
| `d1 create` falla por autenticación | La sesión venció | `npx wrangler login` otra vez |
| `git push` rechazado o pide credenciales | Falta iniciar sesión en GitHub desde la terminal | `gh auth login` (la persona, con `!` en Claude Code) |
| `pages secret put` dice que no existe el proyecto | El proyecto de Pages todavía no se creó, o el nombre no coincide | Paso 9; revisá el nombre con la persona |
| La página no se actualiza al publicar | Falta `DEPLOY_HOOK_URL` o no hubo deploy después | Paso 11 |
