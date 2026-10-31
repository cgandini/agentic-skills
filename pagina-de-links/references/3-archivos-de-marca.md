# Fase 3: archivos de marca

**Objetivo:** convertir el `design-system.md` y la tabla de bloques de la fase 2 en la carpeta `brand/`, lista para instalar. **Es lo único que se genera**: no se edita ningún otro archivo del repo.

**Entregable:** `brand/theme.json`, `brand/seed.json` y `brand/examples.json`, validados. Las fotos son opcionales (ver "Las fotos").

Modelo de forma de los tres JSON: `ejemplos/marca-ficticia/`. Es una **MUESTRA** de una persona inventada: nunca copies sus links `example.com`, sus textos ni sus datos a la página de la persona. Cómo se ve cada bloque y qué hace cada color: `docs/BLOQUES.md`.

## Los archivos

| Archivo | Qué es |
|---|---|
| `brand/theme.json` | Colores, fuentes, título de la pestaña, textura y esquinas. Sale del `design-system.md`. |
| `brand/seed.json` | Contenido inicial: perfil, bloques en orden y pie. Sale de la tabla de la fase 2. Se publica tal cual al instalar. |
| `brand/examples.json` | Un bloque de ejemplo por tipo: lo que el panel muestra en miniatura cuando la persona toca "Agregar bloque". |
| `brand/images/` | Ya trae dos fotos de relleno, `perfil` y `tapa`. No se toca para instalar. **Todo lo que esté en esta carpeta queda público en internet**, aunque la página no lo use: no subas fotos que no quieras mostrar. |

## Preguntas antes de escribir (una por mensaje)

Hacé cada pregunta sola, esperá la respuesta y recién entonces la siguiente:

1. **Idioma de la página** (`lang`): `es` o `en`. Cambia los textos automáticos (por ejemplo "Ver libro" o "Vista previa"). El panel está siempre en español.
2. **"¿Querés que Google encuentre tu página? (te recomiendo que sí)".** Sí es `"noindex": false`. No, o "todavía no", es `"noindex": true` (se cambia después, ver `references/6-uso-diario.md`).
3. **Pie de página:** el valor por defecto es `"Hecha con la plantilla gratis de imagineAI"`, texto simple (no un link). Puede cambiarlo o dejarlo en `""`. El campo `footer` **siempre existe**, aunque esté vacío.

No preguntes por fotos: ver "Las fotos".

## `theme.json`

Todas las claves son necesarias. No hay validador automático, así que revisalas con la lista de abajo.

| Clave | Regla |
|---|---|
| `lang` | `"es"` o `"en"` |
| `title`, `description` | Pestaña del navegador y vista previa al compartir el link |
| `themeColor` | Un hex; poné el mismo que `colors.fondo` |
| `noindex` | `true` o `false` (sin comillas) |
| `fontsHref` | Tiene que empezar con `https://fonts.googleapis.com/`; con otro origen no se cargan las fuentes. **Comprobación obligatoria**, ver abajo |
| `fonts` | `titulo`, `texto`, `acento`: el nombre exacto de Google Fonts, que además tiene que estar en `fontsHref` |
| `colors` | Las 12 claves de `references/1-sistema-de-diseno.md`; las diez que no son degradé van como `#RRGGBB` |
| `colors.gradiente`, `colors.aroFoto` | Un `linear-gradient(...)` con las fórmulas de abajo. No uses `;`, `{`, `}`, `<`, `>`, `\` ni `@` (la página los borra) |
| `grain`, `radius` | `true`/`false` y un número en píxeles (14 a 16 es lo habitual) |

**Fórmulas para no inventar** (con los hex ya elegidos; así lo hace el ejemplo):

- `gradiente` (botón principal al pasar el cursor): `linear-gradient(135deg,ACENTO 0%,ACENTOTEXTO 90%)`. Por ejemplo, con `acento` `#2F855A` y `acentoTexto` `#276749`: `linear-gradient(135deg,#2F855A 0%,#276749 90%)`.
- `aroFoto` (aro de la foto de perfil): `linear-gradient(180deg,ACENTOSUAVE,ACENTO)`. Por ejemplo: `linear-gradient(180deg,#9ADBB4,#2F855A)`.

**Comprobación de `fontsHref` (obligatoria, en un solo mensaje).** Armá el link con las tres fuentes y pesos de `references/1-sistema-de-diseno.md` (paso 5): `https://fonts.googleapis.com/css2?family=Nombre+Uno:wght@700;800&family=Nombre+Dos:wght@400;500&family=Nombre+Tres:wght@400&display=swap`. Dáselo a la persona y pedile: "Abrí este link. ¿Ves texto que empieza con `@font-face`, o una página de error?". Si es error, el nombre de alguna fuente está mal escrito: corregilo y repetí. Con terminal podés comprobarlo vos con `curl -s "<link>" | head -3`.

## `seed.json`

Forma: `{ "version": 1, "profile": {...}, "blocks": [...], "footer": "..." }`. Los bloques van en el orden de la pantalla. **No agregues claves que no estén en `docs/BLOQUES.md`**: el validador las rechaza con "campo no permitido".

- `version` es el número `1`. `footer` tiene que existir.
- `profile`: `photo` y `name` obligatorios; `role`, `phrase`, `highlight` y `sub` opcionales.
- Cada bloque lleva `id`, `type` y `hidden` (`true` o `false`, sin comillas).
- **`id`:** exactamente 8 caracteres, solo letras minúsculas y números (a-z, 0-9), y distinto en cada bloque. **Esquema fijo, sin inventar:** `bloque01`, `bloque02` ... `bloque09`, `bloque10` ... en el orden de la página, y `redes001` para el bloque de redes (`redes002` si hubiera otro). Sin guiones, mayúsculas ni tildes.
- **Links:** empiezan con `https://`, `mailto:` o `tel:`; sin espacios; hasta 1000 caracteres. Nada de `http://` ni `javascript:`. Un `https://` no puede traer usuario y contraseña.
- **Imágenes:** `/img/<nombre>` (una foto de `brand/images/`) o un link `https://`. El `<nombre>` es el nombre del archivo sin la extensión. **Para instalar usá solo las dos de relleno:** `profile.photo` es `/img/perfil` y cada `cover` de `libros` es `/img/tapa`. Si nombrás una foto que no está en `brand/images/`, "Preparar mi página" no carga nada.
- **Sin datos inventados:** los links y cifras salen de la fase 2. Si en algún campo quedó un link de ejemplo (`example.com`, `ejemplo.com`), no se instala: antes de entregar, buscá esos dominios en los tres archivos.
- Un texto opcional vacío (`""`) no se dibuja; igual conviene directamente omitir el campo.
- `highlight` (en el perfil y en la tarjeta) tiene que ser un fragmento **exacto** de la frase o del título; el validador **no** lo comprueba y, si no coincide, no se resalta nada.

### Largos y cantidades

Copiados de `public/admin/limits.js` (si difiere, manda `limits.js`). Se cuentan **caracteres**, con espacios y tildes.

| Dónde | Campo (constante) | Máximo |
|---|---|---|
| Perfil | `name` (`profileName`) | 60 |
| Perfil | `role` (`profileRole`) | 80 |
| Perfil | `phrase` | 120 |
| Perfil | `highlight` (`profileHighlight`) | 120 |
| Perfil | `sub` | 160 |
| Pie | `footer` | 160 |
| `destacado` | `label` / `title` / `text` / `proof` | 40 / 60 / 220 / 90 |
| `destacado` y `tarjeta` | `button.text` (`button`) | 40 |
| `tarjeta` | `label` / `title` / `highlight` / `text` | 40 / 60 / 60 / 220 |
| `fila` | `title` (`filaTitle`) / `text` (`filaText`) | 50 / 90 |
| `libros` | `label` / `groups[].title` (`groupTitle`) | 40 / 80 |
| `libros` | `title` (`bookTitle`) / `author` / `linkText` | 80 / 60 / 40 |
| `libros` | `more.text` (`button`) | 40 |
| Todo | link (`url`) | 1000 |

| Cantidades | Valor |
|---|---|
| Bloques por página (`MAX_BLOCKS`) | 40 |
| Tamaño del JSON (`MAX_JSON_BYTES`) | 200 KB |
| Grupos en `libros` (`COUNT.groups`) | 1 a 3 |
| Ítems de un grupo `"destacado"` | exactamente 1 |
| Ítems de un grupo `"fila"` | 1 a 3 |
| Íconos de `redes` (`COUNT.redes`) | 1 a 8 |

### Campos obligatorios (`REQUIRED` de `limits.js`)

`destacado`: `title`, `button.text`, `button.url`. `tarjeta`: lo mismo. `fila`: `icon`, `title`, `url`, `verified`, `style`. `libros`: `groups` (cada uno con `title`, `layout` e `items`), cada ítem con `title`, `cover` y `url`; `more` es opcional pero, si está, lleva `text` y `url`. `redes`: `items`, cada uno con `network` y `url`. Todo lo demás es opcional.

`fila.style` es `"solido"` o `"borde"`. `groups[].layout` es `"destacado"` o `"fila"`.

### Íconos (`functions/_lib/icons.js`, nombres exactos)

- **Íconos de interfaz (`ICON_KEYS`)**: `arrow-right`, `chevron-right`, `check`, `mail`, `calendar`, `mic`, `presentation`, `book`, `user`, `globe`, `link`, `play`, `headphones`, `star`, `heart`, `message`, `phone`, `map-pin`, `gift`, `sparkles`. Valen en `fila.icon` y en `tarjeta.button.icon`.
- **Redes (`NETWORK_KEYS`)**: `instagram`, `tiktok`, `youtube`, `spotify`, `x`, `linkedin`, `facebook`, `whatsapp`, `threads`, `email`, `web`. Valen en `redes.items.network` y también en `fila.icon`, pero **no** en `tarjeta.button.icon`.

## `examples.json`

Forma: `{ "version": 1, "blocks": { "destacado": {...}, "tarjeta": {...}, "fila": {...}, "libros": {...}, "redes": {...} } }`. Siempre las **cinco** claves, cada una un bloque completo y válido de su tipo, con su `id` propio de 8 caracteres (`ejdest01`, `ejtarj01`, `ejfila01`, `ejlibr01`, `ejredes1`).

- Usá la voz y el contenido de la persona (los mismos textos del seed sirven).
- Mantené los textos con un largo parecido al de `ejemplos/marca-ficticia/examples.json`: el panel dibuja la miniatura con una altura medida para esos tamaños.
- En `libros` usá `/img/tapa` como `cover`; en todo `examples.json` solo valen las fotos de relleno (`/img/perfil`, `/img/tapa`).

## Las fotos

**Camino por defecto, sin renombrar ni preparar nada:** la plantilla trae dos fotos de relleno, `brand/images/perfil` y `brand/images/tapa`. Los JSON las nombran (`/img/perfil`, `/img/tapa`), se instala así y **después** la persona sube las reales desde el panel: **Editar perfil** > **Subir foto** para la suya, y el bloque del libro para cada tapa. El panel las achica solo a 480 px; no hace falta prepararlas. Hasta entonces la página muestra la silueta y la tapa de relleno.

- **iPhone (HEIC) y otros formatos:** el panel acepta lo que el navegador del celular pueda leer. Si una foto da el aviso "No se pudo leer la imagen", sacale una captura de pantalla a esa foto y subí la captura.
- Las tapas se ven a 90 por 135 px (verticales, 2 por 3) y la foto de perfil en un círculo de 96 px (cuadrada, con la cara al centro): decíselo a la persona al subirlas.

**Camino opcional, solo para quien tiene computadora y quiere sus fotos desde el principio** (lo normal es no hacerlo):

- **Nombre = id.** El archivo `perfil.webp` es la imagen `/img/perfil`. El nombre solo lleva letras minúsculas y números, de **4 a 32** caracteres, sin guiones, espacios, tildes ni mayúsculas (`tapa1.webp`, sí; `Mi-Foto 2.jpg`, no). Extensiones válidas: `.webp`, `.jpg`, `.jpeg`, `.png`. Una foto con el nombre de una de relleno la reemplaza.
- **Tamaño:** cada archivo, **menos de 400 KB**, lado largo de **480 px** como mucho. En **squoosh.app** (gratis, funciona en el navegador y la foto no sale de tu equipo): arrastrá la foto, activá "Resize" con 480 en el lado largo, elegí WebP, bajá la calidad hasta pesar menos de 400 KB y descargala. Si no es cuadrada, recortala antes con el editor del celular o de la computadora.
- **Tienen que estar todas las fotos que nombran `seed.json` y `examples.json`**: si falta una, "Preparar mi página" no carga nada y dice cuál falta. Si alguna pesa de más, dice: «La imagen «perfil.webp» pesa más de 400 KB. Achicala en brand/images/. No se cargó nada.»

## Validar antes de entregar

**Ruta A: con terminal.** Desde la carpeta del repo (donde está `package.json`). Si es la primera vez, `npm ci`. Cada comando imprime `OK` o la lista de errores.

```bash
# seed.json: reglas completas del servidor + que los resaltados coincidan
node --input-type=module -e "import {readFileSync} from 'node:fs'; import {validatePage} from './functions/_lib/validate.js'; const d=JSON.parse(readFileSync('brand/seed.json','utf8')); const r=validatePage(d); const e=[...r.errors]; if(d.profile?.highlight&&!d.profile.phrase?.includes(d.profile.highlight))e.push('profile.highlight no es un fragmento exacto de phrase'); d.blocks?.forEach((b,i)=>{if(b.type==='tarjeta'&&b.highlight&&!b.title?.includes(b.highlight))e.push('blocks['+i+'].highlight no es un fragmento exacto de title')}); console.log(e.length?'seed.json: ERRORES\n- '+e.join('\n- '):'seed.json: OK')"
```

```bash
# examples.json: los cinco tipos, cada uno válido
node --input-type=module -e "import {readFileSync} from 'node:fs'; import {validatePage} from './functions/_lib/validate.js'; const ex=JSON.parse(readFileSync('brand/examples.json','utf8')); let bad=0; for (const t of ['destacado','tarjeta','fila','libros','redes']){ const b=ex.blocks?.[t]; if(!b||b.type!==t){console.log(t+': falta o es de otro tipo'); bad++; continue} const r=validatePage({version:1,profile:{photo:'/img/perfil',name:'Ejemplo'},blocks:[b],footer:''}); if(!r.ok){bad++; console.log(t+':\n- '+r.errors.join('\n- '))} } console.log(bad?'examples.json: ERRORES':'examples.json: OK')"
```

```bash
# theme.json: claves, colores y fuentes
node --input-type=module -e "import {readFileSync} from 'node:fs'; const t=JSON.parse(readFileSync('brand/theme.json','utf8')); const c=['fondo','superficie','tinta','texto','gris','borde','bordeFondo','acento','acentoTexto','acentoSuave']; const p=[]; for(const k of ['lang','title','description','themeColor','fontsHref'])if(!t[k])p.push('falta '+k); for(const k of [...c,'gradiente','aroFoto'])if(!t.colors?.[k])p.push('falta colors.'+k); for(const k of c)if(t.colors?.[k]&&!/^#[0-9A-Fa-f]{6}$/.test(t.colors[k]))p.push('colors.'+k+' no es #RRGGBB'); for(const k of ['titulo','texto','acento']){const f=t.fonts?.[k]; if(!f)p.push('falta fonts.'+k); else if(!String(t.fontsHref).includes(f.replaceAll(' ','+')))p.push('fonts.'+k+' ('+f+') no está en fontsHref')} if(!String(t.fontsHref).startsWith('https://fonts.googleapis.com/'))p.push('fontsHref tiene que empezar con https://fonts.googleapis.com/'); for(const k of ['noindex','grain'])if(typeof t[k]!=='boolean')p.push(k+' tiene que ser true o false'); if(!Number.isFinite(t.radius))p.push('radius tiene que ser un número'); console.log(p.length?'theme.json: PROBLEMAS\n- '+p.join('\n- '):'theme.json: OK')"
```

```bash
# que la página se dibuje con este tema (las fotos se simulan)
node --input-type=module -e "import {readFileSync} from 'node:fs'; import {renderPage, allImageIds} from './functions/_lib/render.js'; const doc=JSON.parse(readFileSync('brand/seed.json','utf8')); const theme=JSON.parse(readFileSync('brand/theme.json','utf8')); const images=Object.fromEntries(allImageIds(doc).map(id=>[id,{mime:'image/webp',url:'/i/'+id+'.webp'}])); const html=renderPage({doc,theme,mode:'public',images}); console.log('render: OK ('+html.length+' caracteres)')"
```

Si algún comando muestra errores, corregí el archivo y repetí. En Windows, si el comando no corre tal cual, pedile a la persona una captura y adaptá las comillas. Cuando todo da `OK`, entregá y cerrá la fase.

**Ruta B: solo chat.** No podés correr nada, así que **recorré esta lista vos mismo, en voz alta, antes de entregar el JSON**, y mostrale a la persona el resultado ("revisé: 14 puntos, todo en orden"):

1. Es JSON válido: comillas dobles en todo, sin coma después del último elemento, llaves y corchetes balanceados, `true`/`false` sin comillas.
2. `seed.json`: `version` es `1`; hay `profile`, `blocks` y `footer` (aunque sea `""`); sin claves de más.
3. `profile.photo` y `profile.name` están, y `name` no pasa de 60 caracteres.
4. Cada `id` tiene 8 caracteres exactos (a-z, 0-9), contalos uno por uno, y ninguno se repite.
5. Cada `type` es uno de `destacado`, `tarjeta`, `fila`, `libros`, `redes`, y cada bloque tiene `hidden`.
6. Cada link empieza con `https://`, `mailto:` o `tel:`, sin espacios.
7. Cada texto está dentro de su máximo de la tabla de arriba (contá los caracteres de los más largos: `text`, `sub`, `phrase`, `footer`).
8. Cada `fila` tiene `icon`, `title`, `url`, `verified` y `style`, y el `style` es `"solido"` o `"borde"`.
9. Todos los nombres de ícono están en las dos listas de arriba, y `tarjeta.button.icon` no es una red.
10. `libros`: de 1 a 3 grupos; un grupo `"destacado"` tiene 1 ítem y un `"fila"` de 1 a 3; cada ítem tiene `title`, `cover` y `url`.
11. `redes` tiene de 1 a 8 ítems, cada uno con `network` válida y `url`.
12. Cada `highlight` es un fragmento exacto de su frase o título.
13. `examples.json` tiene las cinco claves y ids propios; `theme.json` tiene las 12 claves de color, las tres fuentes dentro de `fontsHref` y `noindex`, `grain` y `radius` con el tipo correcto.
14. Cada `/img/<nombre>` es `/img/perfil` o `/img/tapa` (las de relleno), salvo que la persona haya traído fotos con el camino opcional; no queda ningún `example.com` ni `ejemplo.com`.

**Cómo entregar en la ruta B:** un archivo por mensaje, con su ruta arriba (por ejemplo `brand/theme.json`) y el contenido en un cuadro de código. **No le pidas que lo guarde como archivo en el celular**: en la fase 4 lo va a copiar de ese cuadro y pegar directo en GitHub (etapa 3 de `references/5-instalar-sin-terminal.md`). Pedile solo que confirme que lo vio. Al terminar los tres, entregá el resumen de `SKILL.md` con los tres archivos completos pegados: **ese bloque es su marca** y que lo guarde en una nota, porque sin él hay que rehacer la fase.

## Cierre de la fase

Recapitulá con el bloque de `SKILL.md` (con los tres archivos pegados abajo), recordale que sus fotos reales se suben después desde el panel y dejá claro el próximo paso: la instalación, que necesita una computadora (ruta A: `references/4-instalar-con-terminal.md`; ruta B: `references/5-instalar-sin-terminal.md`).
