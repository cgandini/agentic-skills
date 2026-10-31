# Fase 4, ruta B: instalar sin terminal

**Objetivo:** poner la página y el panel en internet, gratis, con una persona que nunca usó GitHub ni Cloudflare. Vos solo conversás: la persona hace cada clic y cada copiado.

**Entregable:** la página abre en el celular, `/admin/` pide la contraseña y la persona publicó un cambio de prueba. Esta fase lleva **entre 2 y 3 horas en total** y se puede hacer en dos o tres sesiones: cortá después de la etapa 3 y después de la etapa 8, con el resumen de `SKILL.md`.

**Necesita una computadora.** Las etapas usan el editor web de GitHub y el dashboard de Cloudflare, que en un celular se vuelven muy incómodos. Si la persona no tiene una a mano, frená acá y dejá el resumen para retomar.

## Glosario (explicalo con estas palabras la primera vez que aparezca)

- **Repositorio:** la carpeta de tu proyecto guardada en GitHub.
- **Rama (branch):** una versión de esa carpeta; la principal se llama `main`.
- **Deploy:** cada vez que Cloudflare arma y publica tu página de nuevo.
- **Build:** el armado en sí, el trabajo que hace Cloudflare dentro de un deploy.
- **Log:** la lista, paso a paso, de lo que hizo un build; ahí se ve si salió bien.
- **Token:** una llave de un solo permiso que le das a Cloudflare para que lea tu base de datos.
- **Variable:** un dato que Cloudflare guarda para tu proyecto (un ID, una contraseña); las ocultas se llaman Secret.
- **Deploy hook:** una dirección secreta que, al visitarla, hace que Cloudflare arme la página de nuevo; el panel la usa al publicar.
- **Binding:** la conexión entre tu proyecto y tu base de datos; se llama `DB`.
- **Retry deployment:** el botón para repetir un deploy sin cambiar nada.

## Reglas para vos en esta fase

- **Un paso por mensaje, y esperá.** Al final de cada etapa hacé la pregunta de control y no sigas hasta que conteste. Después de cada control aprobado, dale **una línea** con el resumen actualizado (`Etapa de instalación (n de 12)`, `NOMBRE`, `Usuario de GitHub`, `Database ID` cuando exista; ver `SKILL.md`). Nunca secretos.
- **Antes de cada clic, decí qué va a ver después y qué hacer si ve otra cosa.** Cloudflare y GitHub cambian sus pantallas: en cada botón que nombres agregá "si no ves exactamente este botón, buscá uno parecido o mandame una captura".
- **Si cualquier pantalla pide tarjeta de crédito o un método de pago, frená.** Decile a la persona que no siga y qué pantalla es. En todo este camino no se paga nada.
- **Contraseña del panel, token de API, ID de la cuenta de Cloudflare y URL del deploy hook: nunca por el chat.** La persona los pega solo en el campo de Cloudflare. Si pegó uno por acá, que lo regenere ahora (ver `SKILL.md`). Lo único que sí puede pegar es el ID de la base de datos: no es un secreto.
- **Un solo nombre para todo.** Proponé `links` o `<nombre>-links` (por ejemplo `ana-links`), en minúsculas, con guiones y sin tildes ni espacios. En esta guía es `NOMBRE`: es el nombre del repositorio, de la base de datos y del proyecto de Pages. Si `links` solo ya lo usa otra persona, la dirección final cambia: usá `<nombre>-links`.
- Tené a mano los tres archivos de la fase 3 (`theme.json`, `seed.json`, `examples.json`), cada uno en su cuadro de código del chat. **No hace falta ninguna foto ni guardar ningún archivo**: se copia del chat y se pega en GitHub, y las fotos se suben después desde el panel.

---

## Etapa 1: cuenta de GitHub

GitHub es un sitio gratis donde se guardan los archivos de tu página. Cloudflare los lee de ahí cada vez que publicás.

1. Abrí **github.com**. Si ya tenés cuenta, tocá **Sign in** y pasá a la etapa 2. Si no, tocá **Sign up**.
2. Poné tu mail, una contraseña (la tuya, no me la cuentes), un nombre de usuario, y resolvé la verificación. GitHub te manda un código por mail: pegalo.
3. Si te ofrece planes, elegí **Free**. Si te pide tarjeta, frená y avisame.

**Deberías ver:** la página principal de GitHub, con tu foto o un círculo arriba a la derecha. Si ves otra cosa, mandame una captura.

**Control:** "¿Estás adentro de GitHub, con tu usuario arriba a la derecha? ¿Cuál es tu nombre de usuario?" (el usuario no es un secreto: anotalo para el resumen).

## Etapa 2: copiar la plantilla

1. Pasale la dirección de la plantilla (la de la línea `Plantilla:` de `SKILL.md`) y que la abra. Tiene que estar con la sesión iniciada: si no ve el botón del paso siguiente, es por eso.
2. Arriba a la derecha tocá el botón verde **Use this template** y después **Create a new repository**.
3. En **Repository name** escribí `NOMBRE`. En **Owner** tiene que estar tu usuario. Elegí **Private**: nadie ve tus archivos y Cloudflare igual puede leerlos. No marques "Include all branches".
4. Tocá el botón verde **Create repository**.

**Deberías ver:** tu repositorio nuevo, con una lista de carpetas (`brand`, `docs`, `functions`...) y arriba a la izquierda tu usuario y `NOMBRE`.

**Control:** "¿Ves tu repositorio con las carpetas y tu nombre de usuario arriba?"

## Etapa 3: poner tus archivos de marca

Vas a reemplazar los tres archivos de ejemplo por los tuyos, de a uno. Cada vez te paso el texto completo en un cuadro de código del chat y lo copiás de ahí.

**Para cada archivo (`theme.json`, `seed.json`, `examples.json`), en ese orden:**

1. En tu repositorio abrí la carpeta **brand** y tocá el archivo.
2. Arriba a la derecha tocá el **lápiz** (Edit this file).
3. Hacé clic dentro del texto, seleccioná todo (**Ctrl+A**, o **Cmd+A** en Mac) y pegá lo que te di (**Ctrl+V** / **Cmd+V**). Tiene que quedar solo tu texto, nada de lo anterior.
4. Arriba a la derecha tocá el botón verde **Commit changes...** y en la ventanita, otra vez **Commit changes**.

**Deberías ver:** el archivo con tu texto. Si GitHub marca un error de formato en rojo, mandame una captura.

**No toques la carpeta `images`.** Ahí hay dos fotos de relleno (una silueta y una tapa) que la plantilla usa hasta que subas las tuyas desde el panel (etapa 11).

**Control:** "¿Los tres archivos de `brand` tienen tu texto?"

## Etapa 4: cuenta de Cloudflare

Cloudflare es la empresa que va a guardar y mostrar tu página. Es gratis.

1. Abrí **dash.cloudflare.com/sign-up**. Poné tu mail y una contraseña (la tuya, no me la cuentes).
2. Cloudflare te manda un mail para verificar: abrilo y tocá el botón o el link.
3. Si te propone agregar un dominio ("Add a domain") o elegir un plan, no hace falta: cerralo u omitilo. **Si en cualquier momento te pide una tarjeta, frená y avisame.**

**Deberías ver:** el panel de Cloudflare, con un menú a la izquierda que incluye **Workers & Pages**. Si no lo ves ahí, puede estar dentro de otro grupo del menú (por ejemplo "Compute"): buscalo o mandame una captura.

**Control:** "¿Ves el menú de la izquierda con Workers & Pages?"

## Etapa 5: crear la base de datos y poner su ID

La base de datos (D1) es donde se guarda tu contenido.

1. En el menú de la izquierda andá a **Storage & Databases** y después a **D1 SQL database**.
2. Tocá **Create** (o **Create database**). En el nombre escribí `NOMBRE` (el mismo de siempre) y tocá **Create**. Lo demás, como viene.
3. En la pantalla de la base buscá el **Database ID**: un código largo con guiones, parecido a `1a2b3c4d-5e6f-...`. Tocá el ícono de copiar y **pegámelo acá**: no es un secreto.
4. **Yo te paso el archivo `wrangler.toml` completo**, con tu nombre y ese ID ya puestos. Vos lo reemplazás: en tu repositorio abrí `wrangler.toml` (está afuera de las carpetas), tocá el **lápiz**, seleccioná todo, pegá, y **Commit changes** dos veces como antes.

**Para vos (la IA):** armá el archivo con esta forma, cambiando solo los tres valores. Los comentarios del original no hacen falta.

```toml
name = "NOMBRE"
pages_build_output_dir = "public"
compatibility_date = "2026-10-01"

[[d1_databases]]
binding = "DB"
database_name = "NOMBRE"
database_id = "EL-ID-QUE-PEGO-LA-PERSONA"
migrations_dir = "migrations"
```

**Deberías ver:** el archivo guardado con tu nombre y tu ID. Si el ID tiene espacios de más, no va a funcionar.

**Control:** "¿La base `NOMBRE` aparece en D1 y el `wrangler.toml` quedó guardado?"

## Etapa 6: el token (se crea en la 7c)

Un token es una llave con un solo permiso: deja que Cloudflare lea tu base de datos cuando arma la página. Se muestra **una sola vez** y no pasa por el chat ni por ninguna nota: va **directo** desde la pantalla donde se crea al campo donde se guarda. Por eso **no lo crees todavía**: se crea dentro de la etapa 7c, con ese campo abierto en otra pestaña.

Por ahora solo ubicá el lugar: arriba a la derecha tocá tu perfil y entrá a **My Profile**; en el menú de la izquierda elegí **API Tokens** (o abrí **dash.cloudflare.com/profile/api-tokens**).

**Control:** "¿Ves una pantalla de API Tokens con un botón **Create Token**? No lo toques todavía."

## Etapa 7a: conectar GitHub con Cloudflare

Pages es la parte de Cloudflare que muestra tu página. Tiene que quedar **conectado a GitHub**: subir los archivos arrastrándolos a Cloudflare no sirve para esta plantilla.

1. Andá a **Workers & Pages** y tocá **Create application**. Elegí la pestaña **Pages** (a veces es un link chico que dice "Looking to deploy Pages?"). Después **Connect to Git** (o "Import an existing Git repository").
2. Elegí **GitHub**. Se abre una ventana de GitHub: tocá **Install & Authorize**. Si pregunta qué repositorios, elegí **Only select repositories** y marcá `NOMBRE`.
3. De vuelta en Cloudflare, elegí el repositorio `NOMBRE` y tocá **Begin setup**.

**Control:** "¿Ves una pantalla para configurar el proyecto, con tu repositorio `NOMBRE` arriba?"

## Etapa 7b: configuración del build

Completá así:

| Campo | Valor |
|---|---|
| Project name | `NOMBRE` (igual que el `name` del `wrangler.toml`) |
| Production branch | `main` |
| Framework preset | None |
| Build command | `npm ci && node scripts/build.mjs --remote` |
| Build output directory | `public` |

Si Cloudflare dice que el nombre está ocupado, elegí otro y avisame: hay que cambiar también `name` en el `wrangler.toml`.

**Antes de tocar nada más, mirá la pantalla:** ¿hay un desplegable **Environment variables (advanced)**?

- **Si lo ves:** abrilo y hacé la etapa 7c **ahí mismo**, antes de **Save and Deploy**. El primer build ya sale bien.
- **Si no lo ves:** avisale antes: "Va a aparecer un error rojo en el primer intento. Es normal; no tocaste nada mal." Tocá **Save and Deploy** y seguí con la 7c en la configuración del proyecto.

**Control:** "¿Dice la pantalla que el proyecto se está creando, o ves el desplegable de variables abierto?"

## Etapa 7c: variables y token

Son tres ahora (la cuarta, `DEPLOY_HOOK_URL`, va en la etapa 9). **Las tres se cargan como Secret (Encrypt)**: con `wrangler.toml` en el repositorio, Cloudflare puede dejar bloqueadas las variables de texto simple en el dashboard. Si estás en el proyecto ya creado: **Settings** y después **Variables and Secrets**; con **Add** cargá cada una y **Save**. Si en tu pantalla de Cloudflare en **Settings > Builds** aparece una sección separada llamada **Build variables and secrets** (o si el log del deploy dice que no encuentra `CLOUDFLARE_API_TOKEN` durante `build.mjs`), cargá `CLOUDFLARE_ACCOUNT_ID` y `CLOUDFLARE_API_TOKEN` ahí también como secretos cifrados para que el contenedor de build los reciba siempre.

1. **`CLOUDFLARE_ACCOUNT_ID`**: el ID de tu cuenta. Está en **Workers & Pages** (la pantalla general), en **Account details**: tocá copiar y pegalo en el campo. No me lo pases a mí.
2. **`CLOUDFLARE_API_TOKEN`**: **dejá esta pestaña abierta con el campo del valor a la vista** y abrí **otra pestaña** de Cloudflare (etapa 6). Ahí: **Create Token**, bajá hasta **Custom token** y **Get started** (o "Create Custom Token"); **Token name** `NOMBRE-build`; en **Permissions** elegí en las tres listas **Account**, **D1**, **Read** (si pregunta en qué cuenta, la tuya); **Continue to summary** y **Create Token**. Aparece **una sola vez**: tocá **Copy**, volvé a la primera pestaña y pegalo en el campo del valor. No lo guardes en ningún otro lado ni lo pegues en el chat.
3. **`PANEL_PASSWORD`**: la contraseña del panel. La inventás vos y es lo único que protege tu panel. Explicale el método: **elegí 4 palabras sin relación entre sí, por ejemplo mirando objetos de la habitación, separadas por guiones**, de al menos **12 caracteres** en total. Que no sea la de su mail ni la de Cloudflare. Que la guarde **ya mismo** en el administrador de contraseñas del celular o en una nota privada, porque si la pierde hay que cambiarla. **No la escribas en el chat, ni "para chequear".**

*Para vos:* el panel también se podría proteger con Cloudflare Access; es una **opción avanzada que pide tarjeta** aun en el plan gratis, así que en esta guía no se usa.

**Deberías ver:** las tres variables en la lista, ocultas: es lo normal. Si cargaste todo antes de **Save and Deploy**, ahora tocalo y seguí con la etapa 8.

**Control:** "¿Ves las tres variables, y guardaste la contraseña en un lugar seguro?"

## Etapa 8: primer deploy

Un deploy es cada vez que Cloudflare arma tu página de nuevo.

1. En el proyecto entrá a **Deployments**. Si el primer intento falló (error rojo), en ese intento tocá los **tres puntos** y **Retry deployment** (o "Retry build"). Esperá 1 o 2 minutos.
2. Tocá ese intento para abrir el **log**. Buscá, cerca del final:
   - **Bien:** el estado **Success** y una línea que empieza con `Página generada`. En este momento todavía no cargaste tu contenido, así que la línea tiene que decir exactamente `Página generada (todavía no hay nada publicado): public/index.html = página en preparación.`: **es correcto**. (Más adelante dice `Página generada: public/index.html ... KB, N imágenes en public/i/, publicado ...`.)
   - **Mal:** una línea que empieza con `build:` seguida de un error. Mandame una captura de ese texto (el log no muestra tus claves). Si habla de autorización, permisos o "authentication" de wrangler: el token no alcanza. Entrá a la pantalla de **API Tokens** (etapa 6), editá el token `NOMBRE-build`, cambiá **Read** por **Edit** en D1 y seguí hasta guardarlo; después **Retry deployment**. Si sigue igual, creá un token nuevo con **Edit** y reemplazá el valor de `CLOUDFLARE_API_TOKEN` pegándolo directo (etapa 7c, paso 2). Si el error no habla de permisos, mirá la tabla de problemas al final.
3. Abrí `https://NOMBRE.pages.dev`. La dirección exacta aparece arriba en el proyecto. **Deberías ver** una página que dice **"Página en preparación"**. Es lo correcto por ahora. Este primer build también deja disponibles las fotos de relleno para el botón de la etapa 10.

**Control:** "¿El último deploy dice Success y la dirección muestra 'Página en preparación'?"

## Etapa 9: el aviso automático para publicar (deploy hook)

Sin esto, publicar desde el panel guarda el cambio pero la página no se actualiza sola.

1. En el proyecto andá a **Settings > Builds** (puede llamarse "Builds & deployments") y buscá **Deploy hooks**. Tocá **Add deploy hook**.
2. Nombre: `panel`. Rama: `main`. Guardá.
3. Aparece una **URL** que empieza con `https://api.cloudflare.com/`. Copiala. **Es como una contraseña: no me la pases.**
4. Volvé a **Settings > Variables and Secrets** y con **Add** cargá `DEPLOY_HOOK_URL`, tipo **Secret (Encrypt)**, con esa URL. **Save**.
5. Para que tome efecto: **Deployments**, los tres puntos del último intento y **Retry deployment**. Esperá a **Success**.
6. Los deploys de prueba por rama (preview) comparten la misma base de datos y el panel no anda en sus direcciones. Apagalos: en **Settings > Builds > Branch control**, en las ramas de preview elegí **None** (puede verse distinto: si no lo encontrás, mandame una captura; no es urgente). El panel se abre siempre desde la dirección de producción (`NOMBRE.pages.dev` o tu dominio), nunca desde una dirección de prueba.

**Control:** "¿Cargaste el secreto `DEPLOY_HOOK_URL` y el último deploy dice Success?"

## Etapa 10: abrir el panel y preparar la página

1. Abrí `https://NOMBRE.pages.dev/admin/`. Deberías ver **"Entrar al panel"**, un campo **Contraseña** y el botón **Entrar**. Poné la contraseña que inventaste.
2. Si la contraseña es incorrecta, dice "La contraseña no es correcta." Probá de nuevo despacio, sin espacios al final.
3. Adentro vas a ver **"Tu página todavía no está preparada"**, el texto "Vamos a cargar tu contenido inicial (lo que preparaste en la carpeta brand/). Tarda unos segundos." y un botón **Preparar mi página**. Tocalo (mientras trabaja dice "Preparando…"). Si aparece un aviso en rojo, leelo (tabla de problemas): **no se cargó nada**, así que se puede arreglar y volver a tocar el botón.
4. Después aparece la pantalla "Tu página" con tus bloques. Bajo el título dice "Actualizando tu página…" y en 1 o 2 minutos "Tu página está al día".
5. Abrí `https://NOMBRE.pages.dev` en el celular y recargá. **Deberías ver** tu página con tu marca (con la silueta de relleno en vez de tu foto, por ahora).

Si dice "El acceso al panel no está configurado. Revisá el README.": falta `PANEL_PASSWORD` o falta el redeploy (tabla de problemas; el "README" que nombra el panel es esta guía).

**Control:** "¿Se ve tu página con tu marca en el celular?"

## Etapa 11: tu foto, un cambio de prueba y revisión

1. En el panel entrá a **Editar perfil**, tocá **Subir foto** y elegí tu foto del celular (se achica sola). Si el celular da el aviso "No se pudo leer la imagen" (pasa con algunas fotos de iPhone), sacale una captura de pantalla a esa foto y subí la captura. Cambiá también la frase, mirá la **Vista previa** y tocá **Publicar** y confirmá. Las tapas de los libros se suben igual, desde cada bloque.
2. Esperá 1 o 2 minutos hasta "Tu página está al día" y recargá la página pública. **Debe mostrar el cambio.**
3. Revisión final, de a una:
   - La página abre en el celular.
   - `/admin/` pide la contraseña (probalo en una pestaña privada).
   - Una contraseña equivocada muestra "La contraseña no es correcta." (probá una sola vez).
   - Una dirección que no existe, por ejemplo `/nada`, muestra la página 404 con tu marca.
4. **Entrá al panel también desde el otro dispositivo** (si empezaste en la computadora, ahora desde el celular, o al revés). Así, si un día alguien prueba contraseñas en tu panel, los dos siguen entrando sin problema.
5. Cerrá la sesión con el botón **Salir** cuando termines en una computadora ajena. Que agregue `/admin/` a favoritos o a la pantalla de inicio del celular.
6. Cerrá la fase con el resumen de `SKILL.md` y seguí con `references/6-uso-diario.md`.

## Etapa 12 (opcional): dominio propio

Hasta acá la dirección es gratis: `NOMBRE.pages.dev`. Un dominio propio es opcional y se compra aparte (no es gratis).

- **Con subdominio** (por ejemplo `links.tudominio.com`): 1) en el proyecto andá a **Custom domains** y **Set up a domain**; escribí `links.tudominio.com` y seguí. **Primero** agregalo acá. 2) Cloudflare te muestra un registro **CNAME**. Entrá a donde compraste el dominio (su sección de DNS) y creá un registro **CNAME**: nombre `links`, destino `NOMBRE.pages.dev`. 3) Esperá de unos minutos a unas horas hasta que diga **Active**. No hace falta cambiar nada más.
- **Dominio raíz** (`tudominio.com` sin nada antes): exige mover los servidores de nombres del dominio a Cloudflare. Está **fuera de esta guía**: decile a la persona que se puede, pero que no es parte de esta instalación.

El panel pasa a estar en `https://links.tudominio.com/admin/`.

---

## Cambiar colores o fuentes más adelante

Volvé con la IA y `references/1-sistema-de-diseno.md`, generá el `theme.json` nuevo, y reemplazalo en GitHub como en la etapa 3 (**brand > theme.json > lápiz > pegar > Commit changes**). Cloudflare arma la página sola en 1 o 2 minutos. Los textos, links y fotos se cambian desde el panel.

## Si algo falla

| Lo que pasa | Causa probable | Qué hacer |
|---|---|---|
| El build termina con `build:` y un error de autorización de wrangler | El token no tiene permiso suficiente | Etapa 8, rama "Mal": cambiar **Read** por **Edit** en D1. **Retry deployment** |
| El build dice que no encuentra el token o "not authenticated" | El valor se pegó mal, o el nombre de la variable no es exacto | Revisá que se llame exactamente `CLOUDFLARE_API_TOKEN` y borrala. Creá un token nuevo (etapa 7c, paso 2), pegalo directo en la variable (Secret); si en Settings > Builds ves una sección separada de **Build variables and secrets**, cargá `CLOUDFLARE_ACCOUNT_ID` y `CLOUDFLARE_API_TOKEN` ahí también como secretos cifrados, y hacé **Retry deployment** |
| El primer build falla y todavía no cargaste las variables | Esperado (etapa 7b) | Cargalas (etapa 7c) y **Retry deployment** |
| El build termina bien con `Página generada (todavía no hay nada publicado)...` y la página dice "Página en preparación" | Todavía no tocaste **Preparar mi página** | Es lo esperado; seguí con la etapa 10. Si en cambio el build **falla** (`build:` seguido de un error), mandame una captura |
| El build falla en `npm ci` | Falta `package-lock.json` en el repositorio | Abrí el repositorio en GitHub y fijate que esté en la lista de archivos de la raíz. Si no está, volvé a copiar la plantilla |
| No veo "Use this template" | No iniciaste sesión en GitHub | Iniciá sesión y recargá la plantilla |
| Cloudflare no muestra mi repositorio | GitHub no le dio permiso a ese repo | GitHub > Settings > Applications > Cloudflare Pages > Configure > agregá el repo |
| El panel dice "El acceso al panel no está configurado. Revisá el README." | Falta `PANEL_PASSWORD` o no hubo un deploy después de cargarla | Cargala (tipo Secret) y **Retry deployment** |
| El panel dice "La contraseña del panel tiene que tener al menos 12 caracteres. Cambiala en Cloudflare (Settings > Variables and Secrets) y volvé a desplegar." | `PANEL_PASSWORD` tiene menos de 12 caracteres | Cambiala por una de 12 o más y **Retry deployment** |
| "Demasiados intentos. Esperá 15 minutos y probá de nuevo, o entrá desde un dispositivo donde ya hayas entrado antes." | Muchos intentos fallidos (suyos o ajenos) | Esperar 15 minutos, o entrar desde un dispositivo donde ya entró antes. Cambiar la contraseña no lo destraba |
| Al entrar dice "No se pudo comprobar la contraseña ahora. Revisá que la base de datos (DB) esté conectada al proyecto, o probá de nuevo en un rato." | El proyecto no tiene la base conectada (binding `DB`) | En Settings > Bindings solo se ve `DB` en modo de solo lectura (Pages lo administra desde `wrangler.toml`). Revisá en GitHub que `database_id` y `database_name` en `wrangler.toml` sean los de tu base (etapa 5) y hacé **Retry deployment** |
| Al entrar dice "La contraseña es correcta, pero el navegador no guardó la sesión. Revisá que acepte cookies y que estés en la dirección https de tu página." | Cookies bloqueadas, o no está en la dirección `https://` de producción | Permitir cookies para el sitio y abrir `https://NOMBRE.pages.dev/admin/` |
| **Preparar mi página** dice "Falta la imagen «x» (brand/images/x.webp, .jpg o .png) o no es una imagen válida. ... No se cargó nada." | Un JSON de `brand` nombra una foto que no es `/img/perfil` ni `/img/tapa` | Corregí el nombre en `seed.json` / `examples.json` (etapa 3), esperá el deploy (Deployments > Success) y tocá el botón otra vez |
| **Preparar mi página** dice "No se pudo preparar la página. Probá de nuevo; si sigue fallando, avisale a quien te dio el proyecto." | Falló a mitad de camino (por ejemplo, dos pedidos a la vez) | Tocar el botón otra vez; las tablas que quedaron no estorban. Si sigue, mandame una captura |
| **Preparar mi página** dice "La base de datos no está conectada al proyecto (falta el binding DB). Revisá Settings > Bindings." o "El servidor no tiene acceso a los archivos de la marca (brand/images/). Volvé a desplegar el proyecto." | Falta la base conectada, o falta un deploy completo | Lo mismo que la fila de arriba (Settings > Bindings solo muestra `DB` en modo de solo lectura; revisá `database_id` y `database_name` en `wrangler.toml` en GitHub y hacé **Retry deployment**); en el segundo caso, **Retry deployment** y esperar **Success** |
| Olvidó la contraseña | | Cambiá `PANEL_PASSWORD` en Settings > Variables and Secrets y **Retry deployment**. Se cierra la sesión en todos sus dispositivos |
| Publiqué y la página no cambia | Falta `DEPLOY_HOOK_URL` o no hubo redeploy | Etapa 9. Mientras tanto: Deployments > **Retry deployment** a mano |
| Mi dominio da error 522 | Se creó el CNAME antes de agregar el dominio en Pages | Agregalo en **Custom domains** del proyecto (etapa 12) |
| Una foto no se sube o no aparece | Formato que el navegador no lee | Ver la etapa 11 (captura de pantalla de la foto) y subirla otra vez desde el panel |
| Veo una pantalla que no está en esta guía | Cloudflare cambió el diseño | Mandame una captura y buscamos el botón equivalente |

## Sin verificar en una cuenta real

Esta guía todavía no se recorrió de punta a punta en una cuenta nueva de Cloudflare y de GitHub. Estos puntos son los más inciertos; si la pantalla de la persona difiere, no insistas con el texto: pedí una captura y adaptá.

- **Token con solo D1 Read:** que alcance para que el build lea la base. Si no, la etapa 8 ("Mal") lo sube a **Edit**.
- **Las tres variables y `DEPLOY_HOOK_URL` como Secret (Encrypt)**, sin ninguna en texto simple: que el build las reciba todas.
- **"Environment variables (advanced)"** en la pantalla de creación del proyecto: que exista y qué lugar ocupa. Si no existe, el primer error rojo es esperado.
- **Los nombres de los menús** de Cloudflare (Workers & Pages, Storage & Databases, Builds, Branch control) y de GitHub.
