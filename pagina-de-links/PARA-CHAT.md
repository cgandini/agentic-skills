# PARA-CHAT: la skill "pagina-de-links" en un solo archivo

> Archivo generado: no lo edites a mano. Si cambia algo de la skill, corré `node scripts/bundle-skill.mjs` (o `npm run bundle:skill`).

Para la IA que lee esto en un chat de navegador (ruta B, "solo chat"): acá está todo lo que necesitás, uno después de otro. Cada parte empieza con una línea **ARCHIVO: ruta**. Cuando una guía nombre otro archivo (por ejemplo `references/3-archivos-de-marca.md` o `docs/BLOQUES.md`), ya lo tenés más abajo en este mismo texto: no se lo pidas a la persona. La ruta A (con terminal) y los prompts sueltos no están acá porque en un chat no se usan.

Orden: SKILL.md, guía 1 (diseño), guía 2 (contenido), guía 3 (archivos de marca, con las tablas de largos máximos), guía 5 (instalación sin terminal), guía 6 (uso diario), referencia de bloques y ejemplos de la marca ficticia.

---

**ARCHIVO: `skill/pagina-de-links/SKILL.md`**

# Página de links propia, con panel

Esta skill te convierte en la guía de una persona que quiere tener su página de links con su marca. Vos hacés el trabajo de diseño y redacción; la persona decide y hace los clics en sus cuentas.

Plantilla: https://github.com/cgandini/tu-pagina-de-links

(Esa es la dirección del repositorio plantilla. En el resto de la skill se la nombra como "la plantilla".)

## Qué va a tener la persona

- **Una página de links** para la bio, con su marca (colores, tipografías, tono), liviana y pensada para el celular.
- **Un panel** (`/admin/` en su propia dirección) para cambiar textos, links, orden y fotos desde el celular, ver una vista previa, publicar y mirar cuántos clics tuvo cada link.
- **Gratis**: corre en el plan gratis de Cloudflare. La primera vez lleva **entre 2 y 3 horas en total** y se puede hacer en dos o tres sesiones (el resumen de "Retomar" sirve para cortar y seguir otro día).

## Para quién es

Coaches, escritoras, profes, creadoras, gente con servicios o productos chicos. No hace falta saber qué es una terminal, GitHub o Cloudflare: se explica cada cosa cuando aparece.

Lo que la persona necesita traer: un mail, un link a su web o capturas de su Instagram y la lista de links que quiere mostrar. **Las fotos no hacen falta para empezar**: la página se instala con fotos de relleno y ella sube las suyas después, desde el panel, en un toque.

## Qué hace y qué no hace la página (no prometas otra cosa)

- Cinco tipos de bloque, fijos: `destacado`, `tarjeta`, `fila`, `libros`, `redes`. El diseño lo ponen los bloques; desde el panel no se cambian colores ni fuentes.
- Los clics se cuentan por link (7 o 30 días). **No cuenta visitas ni de dónde vienen.**
- Los colores, las fuentes y el título de la página se cambian volviendo a esta skill (ver `references/6-uso-diario.md`), no desde el panel.
- La dirección web sale gratis de Cloudflare. Un dominio propio es opcional y lo explican las guías de instalación; no lo prometas como parte del tiempo de la instalación.
- Los links solo pueden ser `https://`, `mailto:` o `tel:`.

## Paso 0: ruta y computadora

Decidí la ruta por las herramientas que **realmente** tenés en esta conversación (lo sabés vos, no hace falta preguntarlo). Si el mensaje con el que empezó la persona ya dice "ruta B" o "solo chat", la ruta está elegida: **no preguntes por herramientas otra vez**.

- **Ruta A, "tengo terminal"**: podés ejecutar comandos y leer/escribir archivos en una carpeta de la persona. Instalación: `references/4-instalar-con-terminal.md` (para las partes del dashboard de Cloudflare también cargá `references/5-instalar-sin-terminal.md`).
- **Ruta B, "solo chat"**: solo conversás y producís texto o archivos; la persona hace cada clic y cada copiado. Instalación: `references/5-instalar-sin-terminal.md`.

Si de verdad dudás, hacé **una sola pregunta**, en palabras simples: "En esta conversación, ¿puedo crear archivos en una carpeta de tu computadora, o solo escribimos acá?". Con terminal o sin ella, las cuentas (Cloudflare, GitHub) las maneja siempre la persona.

**La primera pregunta a la persona, ya con la ruta elegida:** "¿Tenés una computadora a mano para la instalación?". Las fases 1 a 3 (diseño, contenido, archivos) se pueden hacer desde el celular; la fase 4 usa el editor web de GitHub y el dashboard de Cloudflare, y en el celular se vuelve muy incómoda. Si no tiene computadora, decile que haga las fases 1 a 3 ahora y deje la instalación para cuando tenga una (el resumen de "Retomar" guarda todo).

Las rutas de esta skill son relativas a su carpeta. Si no podés leer los archivos, pedile a la persona que adjunte `PARA-CHAT.md` (un solo archivo con todo lo necesario; está en la carpeta de la skill y en el repositorio de la plantilla).

## Cómo guiar a una persona que no es técnica

Estas reglas valen en todas las fases:

1. **Un paso por mensaje, y esperá.** Nunca pongas dos acciones de la persona en el mismo mensaje.
2. **Palabras simples.** Cada palabra técnica (repositorio, deploy, token, dominio) lleva una explicación de una línea la primera vez. En `references/5-instalar-sin-terminal.md` hay un glosario de diez términos para eso.
3. **Antes de cada clic, decí qué debería ver después**, y qué hacer si ve otra cosa.
4. **Si se traba, pedí una captura de pantalla** y leé lo que muestra antes de sugerir nada.
5. **Nunca pidas ni aceptes contraseñas, tokens de API, URLs de deploy hook ni ningún secreto en el chat.** La persona los pega solo en el campo de Cloudflare o GitHub. Si pegó uno por accidente: decile que lo borre o lo regenere ahora (en Cloudflare: My Profile > API Tokens para un token, Settings > Builds (puede llamarse Builds & deployments) > Deploy hooks para un hook; en GitHub: Settings > Developer settings > Personal access tokens), porque borrar el mensaje no alcanza. En la ruta A, un comando que pide un valor oculto (contraseña, token, hook) lo corre **la persona** en su terminal, nunca vos.
6. **Nunca pidas una tarjeta de crédito.** Si una pantalla la pide, **frená**, decile a la persona que no siga y contale qué pantalla es. No busques rodeos.
7. **Al final de cada fase, recapitulá** (ver "Retomar en un chat nuevo"). En la fase 4, además, después de **cada etapa** dá una línea con el resumen actualizado.
8. **Hablá en el idioma y el registro de la persona** (vos, tú, usted, otro idioma), igual que escribe ella. Los archivos de esta skill están en español rioplatense; adaptá lo que le muestres.
9. **Mostrá antes de seguir.** Al terminar cada entregable mostrá el resultado y pedí opinión. Esperá gustos sobre colores y fuentes y aplicalos en todos lados (la página y el archivo de diseño).
10. **No inventes datos.** Ni cifras, ni testimonios, ni links. Si falta algo, preguntá o dejá la pieza afuera.

## Las fases

| Fase | Qué se hace | Entregable | Cargá |
|---|---|---|---|
| 0. Bienvenida | Explicar qué se va a lograr, elegir ruta, ver si tiene computadora, pedir el material | Ruta elegida y material en mano | este archivo |
| 1. Sistema de diseño | Sacar el estilo real de su web e Instagram: colores, tipografías, tono | `design-system.md` aprobado | `references/1-sistema-de-diseno.md` |
| 2. Contenido | Elegir bloques y ordenar los links por importancia, escribir los textos | Lista de bloques aprobada | `references/2-contenido-y-bloques.md` |
| 3. Archivos de marca | Generar y validar `theme.json`, `seed.json` y `examples.json` (las fotos son opcionales: se suben después) | Los tres archivos listos | `references/3-archivos-de-marca.md` |
| 4. Instalación (necesita computadora) | Poner la página en internet | Página en vivo y panel que abre | ruta A: `references/4-instalar-con-terminal.md`; ruta B: `references/5-instalar-sin-terminal.md` |
| 5. Uso diario | Editar, publicar, ver clics, qué hacer si algo falla, rediseños | La persona sabe editar sola | `references/6-uso-diario.md` |

- **Fase 0 (qué pedir):** contale el plan en cuatro frases, no en una lista larga. Después **una pregunta por mensaje**, esperando cada respuesta, en este orden: 1) cómo quiere que aparezca su nombre; 2) el link a su web y a su Instagram (o capturas); 3) cuál es la única cosa que más quiere que hagan quienes entran; 4) la lista de links, con su destino. **No pidas fotos ahora**: se suben después desde el panel (si quiere, puede mandarte una captura de su perfil para sacar los colores en la fase 1).
- **Si ya tiene un design system** (un archivo o una marca bien definida), pedíselo y saltá a la fase 2, pero igual verificá el contraste de `references/1-sistema-de-diseno.md`.
- **Si usa los prompts sueltos** (sin esta skill): `prompts/1-sistema-de-diseno.md`, `prompts/2-pagina-de-links.md` y, para subirla a internet, `prompts/3-instalar.md`.
- **Ejemplo completo** de todos los archivos para una marca ficticia (Renata Olmos): `ejemplos/marca-ficticia/`. Es una **MUESTRA de forma**: sus links `example.com` y sus datos son inventados y **nunca se instalan** en la página de una persona real.
- **Fuentes de verdad** (si algo de esta skill difiere, mandan ellas): `docs/BLOQUES.md`, `public/admin/limits.js`, `functions/_lib/validate.js` y `functions/_lib/icons.js` del repo. Las tablas de `references/3-archivos-de-marca.md` ya traen sus valores.

## La skill solo genera `brand/`

El código del repo no se edita para cada persona. Lo único que cambia entre marcas es la carpeta `brand/`: `theme.json` (colores, fuentes, título), `seed.json` (contenido inicial), `examples.json` (ejemplos que ve el panel al agregar un bloque) e `images/` (fotos). La plantilla trae dos fotos de relleno (`perfil` y `tapa`): sirven para instalar sin fotos propias, y la persona sube las suyas después desde el panel. No hace falta tocar `images/`. Si la persona te pide algo que exige tocar el código, decile con sinceridad que esta plantilla no lo hace.

## Pie de página

El `footer` del `seed.json` trae por defecto **"Hecha con la plantilla gratis de imagineAI"** como texto simple (no es un link). La persona puede cambiarlo o dejarlo vacío (`""`); ofrecéselo una vez, sin presionar. El campo siempre tiene que existir en el JSON, aunque sea `""`.

## Lista de progreso (la mantenés vos)

Copiala al empezar y actualizala en cada mensaje de cierre de fase:

```
Ruta: [A / B]        Idioma y registro: [vos / tú / usted / otro]
[ ] 0 Bienvenida: ruta elegida, material recibido
[ ] 1 Sistema de diseño aprobado (design-system.md)
[ ] 2 Contenido aprobado (bloques y orden)
[ ] 3 Archivos de marca: theme.json, seed.json, examples.json validados
[ ] 3 Fotos: de relleno al instalar (las reales se suben después desde el panel)
[ ] 4 Tiene computadora a mano; cuentas creadas (la persona, sin pasar claves por el chat)
[ ] 4 Página en vivo y se ve bien en el celular
[ ] 4 Panel abre con su contraseña (la inventó ella y no pasó por el chat)
[ ] 5 Subió su foto desde el panel, editó y publicó un cambio
```

## Retomar en un chat nuevo

Al final de **cada fase**, y en la fase 4 después de **cada etapa** (una línea que diga qué cambió), entregá el bloque actualizado. Que sea completo: otro chat sin memoria tiene que poder seguir con solo eso.

- **Ruta A:** escribí o actualizá `progreso.md` en la carpeta de la persona con lo mismo que lleva el bloque de abajo.
- **Ruta B:** dale el bloque en un cuadro de código y decile: "Guardalo en una nota o en un documento. Si cerrás este chat, abrí uno nuevo, pegá el mensaje de `PROMPT-PARA-CHAT.md`, adjuntá `PARA-CHAT.md` y después pegá este bloque".

```
RESUMEN PARA RETOMAR (pagina-de-links)
Ruta y registro: [...]
Tiene computadora para la instalación: [sí / no / todavía no]
Fase terminada: [n]. Próximo paso: [...]
Etapa de instalación (n de 12): [n, o "todavía no empezó"]
NOMBRE: [el nombre único del repositorio, la base y el proyecto, por ejemplo ana-links]
Usuario de GitHub: [...]
Database ID: [el código de la base D1; no es un secreto]
Marca: nombre, rol, frase, a qué se dedica
Paleta: [nombre + hex + para qué se usa] x 4 a 6
Fuentes: títulos [...], texto [...], acento [...]
Tono: [voseo/tuteo, rasgos, qué evitar]
Bloques en orden: [tipo, título, destino] uno por línea
Decisiones y gustos de la persona: [...]
Pendiente de la persona: [...]
Archivos de marca: pegá abajo theme.json, seed.json y examples.json completos
```

Cuando el bloque llega a la fase 3, el resumen se entrega **junto con los tres archivos completos** pegados abajo (sin ellos, el chat nuevo tendría que rehacerlos). Nunca pongas en el resumen contraseñas, tokens, el ID de la cuenta de Cloudflare ni URLs de deploy hook. Las direcciones públicas de su página y el `Database ID` sí pueden ir.

## Mapa de archivos

- `references/1-sistema-de-diseno.md`, `2-contenido-y-bloques.md`, `3-archivos-de-marca.md`, `6-uso-diario.md`: una por fase, se cargan cuando toca.
- `references/4-instalar-con-terminal.md` y `5-instalar-sin-terminal.md`: instalación según la ruta.
- `prompts/`: tres prompts para copiar y pegar sin la skill (diseño, página, instalación).
- `ejemplos/marca-ficticia/`: `design-system.md`, `theme.json`, `seed.json` y `examples.json` de una persona inventada.
- `PROMPT-PARA-CHAT.md` (en la raíz del repo): el mensaje que se pega en un chat de navegador para empezar.
- `PARA-CHAT.md` (en esta carpeta): este archivo, las guías 1, 2, 3, 5 y 6, `docs/BLOQUES.md` y los JSON de ejemplo en un solo archivo. Se genera con `npm run bundle:skill`; no se edita a mano.

---

**ARCHIVO: `skill/pagina-de-links/references/1-sistema-de-diseno.md`**

# Fase 1: sistema de diseño

**Objetivo:** sacar el estilo real de la persona (colores, tipografías, tono) y dejarlo en un archivo, `design-system.md`, que después se traduce a `brand/theme.json`. No se inventa un estilo nuevo: se **extrae** el que ya tiene.

**Entregables:** `design-system.md` aprobado por la persona y una muestra visual para revisarlo.
- Ruta A: escribí también `design-system.html` en su carpeta (una página con la paleta, las fuentes y una maqueta de los bloques) y decile cómo abrirla con doble clic.
- Ruta B: si tu chat puede mostrar una página HTML (artefacto o vista previa), usala. Si no, mostrá la paleta como tabla y tres líneas de ejemplo con el tono, y pedí opinión sobre eso.

Estructura de referencia: `ejemplos/marca-ficticia/design-system.md`. Los prompts sueltos de esta fase están en `prompts/1-sistema-de-diseno.md`.

## Paso 1: juntar el material

Pedí, en este orden y de a una cosa por mensaje:

1. El link a su web (si tiene).
2. Entre 4 y 6 capturas de su Instagram (el perfil y algunos posts recientes). Explicale cómo: "Abrí tu Instagram en el celular, tocá los botones de volumen y encendido a la vez (o el botón de captura de tu teléfono) y mandame las imágenes".
3. Su logo, si tiene, y cualquier código de color que conozca (Canva, el logo, una guía de marca).

Si puede navegar, **leé su web** (home, y la página de su servicio principal). Si no, pedí capturas de esa web también.

Si no tiene web ni Instagram con estilo definido (marca nueva): pedí tres cuentas o páginas que le gusten y tres adjetivos, y proponé como máximo **dos** opciones cortas. No armes una tercera ni una cuarta.

## Paso 2: las reglas (aprendidas con un caso real)

1. **Extraé, no inventes.** La paleta, las fuentes y el tono salen de lo que la persona ya publica. Donde la web y el Instagram no coinciden, decile cuál tomaste y por qué (suele mandar el canal donde más se mueve).
2. **Una acción, un color.** Un color de acento para lo que se toca o se destaca, una tinta casi negra (nunca `#000000`), un fondo y un blanco. De 4 a 6 colores centrales en total.
3. **El texto chico nunca va en el color de acento.** Los acentos naranjas, amarillos o claros casi siempre fallan el contraste en letra chica. Regla fija: el texto chico va en la tinta, y el acento aparece como **subrayado, flecha o ícono**.
4. **Oscurecer el acento solo para palabras grandes** (24 px o más, en negrita o en la fuente de acento del perfil y las tarjetas), y **tiene que seguir siendo el mismo color**:
   - Mantené el tono (±5 grados) y la saturación casi igual, y bajá la luminosidad **de a poco**.
   - En un caso real, con un coach (naranja `#F76E09`, tono 25, saturación 94, luminosidad 50) el primer intento fue `#9E4510` (tono 22, saturación 82, luminosidad 34): el dueño lo rechazó por "marrón". El final fue `#D05000` (tono 23, saturación 100, luminosidad 41), con contraste 3,38:1 sobre crema, **permitido solo para letra grande**.
   - Los naranjas, amarillos y rojos se ven marrones al bajar de unos 40 % de luminosidad con saturación media. Si para llegar a 3:1 hay que pasar ese punto, no lo hagas: usá la tinta para esa palabra (en `theme.json`, `acentoTexto` igual a `tinta`) y dejá el acento en el subrayado.
   - Mostrale a la persona el color oscurecido junto al original antes de decidir.
5. **Máximo tres fuentes**, todas de Google Fonts: una para títulos, una para texto y **una sola** de acento, que la plantilla usa solo en dos lugares (la frase del perfil y el título de las tarjetas). Si la persona no usa una fuente de acento, repetí la de títulos o la de texto. Muchas fuentes se ven desprolijas.
6. **Sin emojis en ningún lado.** Solo íconos de la lista de la plantilla (`functions/_lib/icons.js`; en `references/3-archivos-de-marca.md` están los nombres).
7. **Ningún dato inventado.** Una cifra ("300 personas ya lo hicieron") se usa solo si sale de lo que la persona publicó o te dice ella. Si no hay fuente, no hay línea de prueba social.
8. **Mostrá y preguntá antes de seguir.** Esperá opiniones de gusto sobre colores y fuentes; cuando lleguen, aplicalas **en todos lados**: el archivo `design-system.md`, la muestra visual y (después) `theme.json`.

## Paso 3: sacar los colores

- Estimá los hex desde las capturas y avisá que se midieron sobre imágenes comprimidas y pueden variar unos puntos. Si la persona conoce sus hex, mandan los suyos.
- Con terminal y una imagen guardada, podés medir los píxeles con un script (Python con Pillow, por ejemplo) en vez de estimar a ojo.
- Armá una tabla: nombre, hex, dónde aparece, uso. Marcá cuáles son **derivados** (los que agregás vos por accesibilidad) y cuáles son suyos.

## Paso 4: verificar el contraste

El contraste es la razón entre la luminosidad de dos colores. Se pide **4,5 o más** para texto chico y **3 o más** para texto grande.

**Cálculo** (por canal: `v = valor/255`; si `v <= 0.03928` queda `v/12.92`, si no `((v+0.055)/1.055)^2.4`; luminosidad `L = 0.2126 R + 0.7152 G + 0.0722 B`; contraste `(L claro + 0.05) / (L oscuro + 0.05)`). Con terminal:

```bash
node -e "const L=h=>{const c=[1,3,5].map(i=>parseInt(h.slice(i,i+2),16)/255).map(v=>v<=.03928?v/12.92:((v+.055)/1.055)**2.4);return .2126*c[0]+.7152*c[1]+.0722*c[2]};const r=(a,b)=>{const[x,y]=[L(a),L(b)].sort((p,q)=>q-p);return ((x+.05)/(y+.05)).toFixed(2)};console.log(r('#D05000','#E9E2D7'))"
```

(cambiá los dos hex; ese ejemplo imprime `3.38`). Sin terminal, calculalo a mano y mostrá la cuenta. Para ver tono, saturación y luminosidad de un color (regla 4), usá la misma idea con la conversión RGB a HSL.

**Pares que se verifican siempre** (así los usa la plantilla):

| Texto o elemento | Sobre | Mínimo | Dónde se ve |
|---|---|---|---|
| `tinta` | `fondo` | 4,5 | nombre, títulos, etiquetas |
| `texto` | `superficie` | 4,5 | cuerpo de las tarjetas |
| `gris` | `fondo` y `superficie` | 4,5 | rol, subtítulo, descripciones |
| `superficie` | `tinta` | 4,5 | la tarjeta oscura |
| `acentoSuave` | `tinta` | 4,5 | etiqueta y tilde de la tarjeta oscura |
| `superficie` | `acento` | 3 (ideal 4,5) | texto del botón, glifos, insignia |
| `acentoTexto` | `fondo` y `superficie` | 3 | solo la frase del perfil y el título de la tarjeta (letra grande) |
| `acento` | `fondo` | decorativo | subrayados y flechas; apuntá a 3 y avisá si queda más bajo |

Si un par no llega: ajustá el color **de a poco**, conservando el tono. Si un par de letra chica no llega ni oscureciendo, cambiá el color del texto a `tinta` o `texto`. Anotá cada ratio en la tabla de contraste del `design-system.md`.

## Paso 5: tipografías

- **Solo Google Fonts.** La página carga fuentes únicamente desde `fonts.googleapis.com`; cualquier otro origen no se carga. Los nombres tienen que ser exactos, como figuran en Google Fonts.
- Pesos que usa la plantilla (pedilos en el link): la fuente de **títulos** en 700 y 800; la de **texto** en 400 y 500; la de **acento** en 400.
- El nombre de la persona y las etiquetas se muestran **en mayúsculas**: elegí una fuente de títulos que se vea bien así.
- Elegí las más parecidas a las de la persona y decilo claro: son aproximaciones. El link de Google Fonts se comprueba siempre con la persona (ver `references/3-archivos-de-marca.md`, "Comprobación de `fontsHref`"): se arma recién en la fase 3.

## Paso 6: el tono

Mirá cómo escribe y cómo le habla a su comunidad. Anotá:

- **Tratamiento:** vos, tú o usted. Elegí uno por pieza y no los mezcles.
- Cómo abre y cómo cierra, el largo de sus frases, si usa humor, números, preguntas.
- Palabras suyas que se repiten y palabras que **evita**.
- Postura sobre emojis (en la página no hay; en sus redes puede haber).
- Tres o cuatro frases reales suyas como ejemplo, citadas con su fuente.

## Paso 7: escribir `design-system.md`

Estas secciones, en este orden (copiá la forma de `ejemplos/marca-ficticia/design-system.md`):

```
# [Nombre]: design system (para pasarle a la IA)
[Una línea: de dónde sale. Fuentes consultadas.]
## Regla general            (3 a 4 líneas: cómo se siente la marca)
## Colores                  (tabla; derivados para accesibilidad; tabla de contraste)
## Tipografía               (link de Google Fonts, roles, tamaños)
## Bordes y detalles        (radio de esquinas, textura de fondo)
## Componentes              (cómo se ven botones, tarjetas y links en SU marca)
## Tono                     (tratamiento, ganchos, objetos que vuelven, qué evitar, ejemplos reales)
## Mapa a la plantilla      (qué valor va en cada ítem de theme.json)
## Lo que falta confirmar   (aproximaciones, fuentes distintas, medidas sobre capturas)
```

- Espacios, sombras y tamaños **no se eligen**: la plantilla los fija. Solo se eligen `radius` (en píxeles) y `grain` (textura de puntos, sí o no).
- Si la marca tiene piezas de redes (placas, portadas), podés agregar una sección con ellas, pero no es necesaria para la página.

**Mapa a la plantilla** (usá estos nombres exactos; el significado de cada uno está en `docs/BLOQUES.md`):

| Ítem de `theme.json` | Qué es |
|---|---|
| `colors.fondo` | fondo de la página |
| `colors.superficie` | tarjetas blancas y texto sobre fondos oscuros |
| `colors.tinta` | títulos, tarjeta oscura, botón oscuro |
| `colors.texto` y `colors.gris` | cuerpo y texto secundario |
| `colors.borde` y `colors.bordeFondo` | bordes sobre blanco y sobre el fondo |
| `colors.acento` | botón principal, disco de las filas, subrayados, flechas |
| `colors.acentoTexto` | palabra resaltada en letra grande |
| `colors.acentoSuave` | etiqueta y tilde sobre la tarjeta oscura |
| `colors.gradiente` y `colors.aroFoto` | hover del botón principal y aro de la foto |
| `fonts.titulo`, `fonts.texto`, `fonts.acento` | las tres fuentes |

## Paso 8: mostrar, escuchar, aplicar

1. Mostrá la muestra visual y resumí en cinco líneas lo que decidiste.
2. Preguntá, una pregunta por vez: colores (¿se siente tu marca?), fuentes, tono.
3. Aplicá cada cambio en todos lados y volvé a verificar el contraste de lo que tocaste.
4. Cuando la persona diga que sí, cerrá la fase con el bloque de resumen de `SKILL.md`.

---

**ARCHIVO: `skill/pagina-de-links/references/2-contenido-y-bloques.md`**

# Fase 2: contenido y bloques

**Objetivo:** decidir qué bloques lleva la página, en qué orden y con qué textos. Una página de links no es una lista: es un recorrido donde **lo más importante va primero y es una sola cosa**.

**Entregable:** una tabla de bloques en orden, aprobada por la persona (formato al final). Todavía no se escribe JSON: eso es la fase 3.

Los campos exactos, los límites y cómo se ve cada bloque están en `docs/BLOQUES.md` y en `public/admin/limits.js`; no los repitas de memoria. En `references/3-archivos-de-marca.md` hay una tabla con los largos máximos. El prompt suelto de esta fase es `prompts/2-pagina-de-links.md`.

## Paso 1: la pregunta que ordena todo

Preguntá, y esperá la respuesta:

> Si una persona entra a tu página y puede hacer una sola cosa, ¿cuál querés que sea?

Esa respuesta es el bloque `destacado`. Después pedí la lista completa de links: qué es cada uno y a dónde lleva. **Todas las direcciones las pone la persona**; nunca inventes un link ni uses uno "de ejemplo" en la página real.

## Paso 2: qué bloque usar para cada cosa

| Lo que la persona tiene | Bloque | Por qué |
|---|---|---|
| Su oferta principal (sesión 1 a 1, curso, reserva, producto estrella) | `destacado` | Tarjeta oscura con botón grande. **Una sola vez, arriba de todo.** |
| Una acción secundaria con un beneficio claro (newsletter, descarga gratis, comunidad) | `tarjeta` | Título, texto y botón. Puede resaltar parte del título. |
| Un destino más, en una línea (canal de WhatsApp, podcast, charlas, contacto, sitio web) | `fila` | Ícono, título y una descripción corta. |
| Cosas con tapa: libros, cursos, episodios, productos | `libros` | Portadas en fila, hasta 3 grupos. Sirve para cualquier cosa con imagen vertical. |
| Sus redes sociales | `redes` | Íconos en círculo, hasta 8. **Va último**, antes del pie. |

Cómo decidir cuando hay dudas:

- **Dos cosas "principales":** una es el `destacado`; la otra baja a `tarjeta`. Preguntale cuál le da más (en plata o en importancia). No pongas dos destacados.
- **Más de 7 u 8 bloques:** proponé sacar o agrupar. Menos opciones, más clics. Es un consejo, no una regla del producto (el tope técnico son 40 bloques).
- **Algo temporal** (un evento, una oferta de temporada): cargalo con `hidden` en `true` y mostrale a la persona que puede **mostrarlo u ocultarlo desde el panel** cuando toque.
- **Varios idiomas o varios públicos:** una página por público. Esta plantilla tiene una sola página por instalación.

## Paso 3: el orden por importancia

Orden por defecto, de arriba hacia abajo:

1. Perfil (foto, nombre, rol, frase).
2. `destacado`: la oferta principal.
3. `tarjeta`: la acción secundaria.
4. `fila`: destinos, del más al menos importante (un máximo de 3 o 4 seguidas).
5. `libros`, si hay productos con tapa.
6. `redes`.
7. Pie.

Podés proponer cambios de orden o de bloque a partir de lo que veas en su web e Instagram (qué promociona más, qué repite, qué ya no usa). **Explicá cada cambio en una frase y dejá que la persona decida.** Si algo sobra o falta, decilo.

## Paso 4: escribir los textos

Escribí en la voz del `design-system.md` (tratamiento, ganchos, qué evitar). Reglas de oficio:

- **Botones con un verbo de acción:** "Agendá tu sesión", "Suscribirme", "Ver en la librería". Nunca "Click acá".
- **Un título dice qué es; el texto dice qué gana la persona.** Frases cortas.
- **`label`** (etiqueta chica arriba del título): la categoría en 1 a 3 palabras ("Sesión 1 a 1", "Newsletter").
- **`proof`** (la línea con tilde del destacado): solo con un dato real que salga de lo que la persona publicó o te dijo. Sin fuente, **no hay `proof`**.
- **`highlight`** de la tarjeta y del perfil: tiene que ser un fragmento **exacto** del título o de la frase (mismas letras, mismas tildes). Si no coincide, no se resalta nada. Elegí 1 a 3 palabras.
- **`verified`** en una `fila` muestra una insignia de verificado. Poné `true` solo si ese canal realmente está verificado (por ejemplo un canal de WhatsApp con la tilde oficial); si no, `false`.
- **`style` de la fila:** `"solido"` para destinos importantes (fondo blanco, ícono en disco de color), `"borde"` para los secundarios (solo contorno).
- **Íconos:** elegí el que mejor represente el destino entre los disponibles; para una red social, el de la red. La lista está en `references/3-archivos-de-marca.md`.
- **Mantené los textos cerca del largo de los ejemplos de la plantilla.** Los textos de `examples.json` no deberían ser mucho más largos que los del ejemplo de `ejemplos/marca-ficticia/`.
- **Sin emojis.**

## Paso 5: el perfil

| Campo | Qué poner |
|---|---|
| `photo` | Foto de la persona (cuadrada o casi; se muestra en círculo de 96 px). Obligatoria. Al instalar queda la de relleno y la persona sube la suya desde el panel. |
| `name` | Su nombre como quiere que aparezca. Se muestra en mayúsculas. |
| `role` | Rol y rubro en una línea: "Nutricionista · Alimentación sin culpa". |
| `phrase` y `highlight` | Una frase corta con su estilo y el fragmento que se resalta. |
| `sub` | Una línea que aclara qué hace, con herramientas concretas. |

## Detalles por tipo de bloque

- **`libros`:** cada grupo tiene un subtítulo y un diseño. `"destacado"` es un solo ítem con tapa grande; `"fila"` hasta 3 ítems en tres columnas. Las tapas son imágenes verticales (2 por 3). Al instalar llevan la tapa de relleno y la persona sube las reales desde el panel. Si no va a tener tapas nunca, no uses este bloque.
- **`redes`:** el correo va como `mailto:hola@...`. Para WhatsApp, el formato `https://wa.me/` seguido del número con código de país, sin `+` ni espacios, abre la conversación.
- **Teléfono:** `tel:+54...` funciona en una `fila`.

## Cómo cerrar la fase

Mostrá la tabla y pedí la aprobación con una pregunta concreta ("¿Lo dejamos así?"). Aplicá los cambios y recién entonces cerrá con el bloque de resumen de `SKILL.md`.

```
| # | Bloque | Título | Destino (lo puso la persona) | Notas |
|---|---|---|---|---|
| 1 | destacado | Sesión de bienvenida | https://... | etiqueta, texto, línea de prueba (con fuente) |
| 2 | tarjeta | ... | ... | resalta "..." |
| 3 | fila (solido) | ... | ... | ícono: ... |
| 4 | fila (borde) | ... | ... | verified: no |
| 5 | libros | ... | ... | N grupos (las tapas se suben después desde el panel) |
| 6 | redes | Instagram, YouTube, correo | ... | último |
Perfil: nombre / rol / frase (resalta "...") / sub
Pie: "Hecha con la plantilla gratis de imagineAI" (o el que elija)
```

---

**ARCHIVO: `skill/pagina-de-links/references/3-archivos-de-marca.md`**

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

---

**ARCHIVO: `skill/pagina-de-links/references/5-instalar-sin-terminal.md`**

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

---

**ARCHIVO: `skill/pagina-de-links/references/6-uso-diario.md`**

# Fase 5: uso diario

**Objetivo:** que la persona sepa editar, publicar y mirar sus clics sola, desde el celular, y que sepa qué hacer cuando algo no se ve bien. Cerrá la instalación con una práctica: pedile que cambie un texto, mire la vista previa y publique.

Los textos entre comillas de abajo son los que el panel muestra de verdad. Si la persona ve otro, pedile una captura.

## Entrar al panel

- La dirección es la de su página seguida de `/admin/` (por ejemplo `https://tu-pagina.pages.dev/admin/`). Pedile que la agregue a favoritos o a la pantalla de inicio del celular desde el menú de su navegador.
- Entra con la **contraseña** que inventó al instalar (pantalla "Entrar al panel", campo "Contraseña", botón "Entrar"). Conviene que la guarde en el administrador de contraseñas del celular. Al terminar en una computadora ajena, que toque **Salir**.
- **Si la olvidó:** en Cloudflare, su proyecto, Settings > Variables and Secrets, cambia `PANEL_PASSWORD` por una nueva (12 caracteres o más) y toca Deployments > **Retry deployment**. Se cierra la sesión en todos sus dispositivos. Nunca pegar la contraseña en el chat.

## Cómo es la pantalla "Tu página"

| Parte | Para qué sirve |
|---|---|
| Arriba, **Vista previa** | Muestra la página entera con los cambios, sin publicarla. Los links no cuentan clics ahí. |
| Línea debajo del título | Estado del guardado: "Guardando…", "Guardado" o "Sin conexión". Se guarda solo, a los instantes de cada cambio. |
| Tu perfil, **Editar perfil** | Foto, nombre, rol, frase, resaltado, subtítulo y **Nota al pie**. |
| Pestaña **Bloques** | La lista, en el orden en que se ven. Cada bloque tiene **Subir**, **Bajar**, **Ocultar** (o **Mostrar**), **Editar** y **Borrar** (pide confirmación). |
| **Agregar bloque** | Abajo. Muestra los cinco tipos con una miniatura real de cómo se ven con tu marca. |
| **Publicar** | Abajo. Dice "Publicar" cuando hay cambios y "Publicado" (apagado) cuando no hay nada nuevo. |
| Pestaña **Estadísticas** | Clics por link en los últimos **7 días** o **30 días**. |

## El camino de un cambio

1. Editar. Los cambios quedan como **borrador**: nadie los ve todavía.
2. Mirar la **Vista previa**.
3. Tocar **Publicar** y confirmar ("¿Publicar los cambios?").
4. Esperar **1 o 2 minutos**. Bajo el título dice "Actualizando tu página…" y después "Tu página está al día".
5. Abrir la página pública (en una pestaña privada o recargando) y comprobar.

Cosas a saber:
- Un bloque marcado **Sin completar** (le falta un dato obligatorio) **no se publica**. El aviso de confirmar lo cuenta ("Hay N bloques sin completar que no se van a publicar.").
- **Ocultar** saca un bloque de la página sin borrarlo: sirve para ofertas de temporada.
- Cada publicación pide a Cloudflare armar la página de nuevo. El plan gratis incluye **500 builds por mes**, y cada publicación usa uno: sobra para el uso normal, pero conviene juntar varios cambios en una sola.

## Fotos

En **Editar perfil** (foto de perfil) o en el bloque de libros (tapas): **Subir foto**. La foto se achica sola a 480 px; no hace falta prepararla ni renombrarla. Si el celular da el aviso "No se pudo leer la imagen" (pasa con algunas fotos de iPhone en formato HEIC), sacale una captura de pantalla a la foto y subí la captura. También se puede pegar un link `https://` de una imagen, aunque conviene subirla: si el otro sitio la borra, deja de verse.

## Ver los clics

En **Estadísticas**. Cuenta **clics en cada link**, no visitas ni de dónde llegan. Si un día hay muchísimos clics, el contador se detiene hasta el día siguiente (UTC) y la página sigue funcionando.

## Si algo se ve mal

| Lo que ve | Qué significa | Qué hacer |
|---|---|---|
| Vuelve a aparecer "Entrar al panel", y si estaba editando dice arriba "Tu sesión venció. Entrá de nuevo con tu contraseña." | La sesión (dura 30 días en ese navegador), o la cookie, venció; o se cambió `PANEL_PASSWORD`. | Escribir la contraseña y tocar **Entrar**: lo que estaba editando se sigue guardando. |
| "La contraseña es correcta, pero el navegador no guardó la sesión. Revisá que acepte cookies y que estés en la dirección https de tu página." | El navegador bloquea las cookies o no está en la dirección `https://` de su página. | Permitir cookies para el sitio y abrir la dirección `https://…/admin/` de su página. |
| "La contraseña no es correcta." | Se equivocó al escribirla. | Escribirla de nuevo, sin espacios al final. Si no la recuerda, ver "Si la olvidó". |
| "Demasiados intentos. Esperá 15 minutos y probá de nuevo, o entrá desde un dispositivo donde ya hayas entrado antes." | Hubo muchos intentos fallidos: suyos, o de otra persona probando contraseñas. | Esperar 15 minutos, o entrar desde el celular o la computadora donde ya entró antes (esos no se bloquean por intentos ajenos). Cambiar la contraseña **no** lo destraba. |
| "El acceso al panel no está configurado. Revisá el README." | Falta la variable `PANEL_PASSWORD`, o no hubo un deploy después de cargarla. (El "README" que nombra el panel es la guía de instalación.) | Volver a la guía de instalación (variables) y hacer **Retry deployment**. |
| "La contraseña del panel tiene que tener al menos 12 caracteres. Cambiala en Cloudflare (Settings > Variables and Secrets) y volvé a desplegar." | `PANEL_PASSWORD` tiene menos de 12 caracteres. | Cambiarla por una de 12 o más y hacer **Retry deployment**. |
| "Se editó desde otro dispositivo…" | Hay una versión más nueva en otro celular o computadora. | Tocar **Recargar** y rehacer el cambio. |
| "Tu página todavía muestra la versión anterior" (a los 4 minutos) | La página no se actualizó. | Esperar un rato más y recargar. Si sigue igual, en Cloudflare, Workers & Pages, tu proyecto, **Deployments**, ver si el último falló y tocar **Retry deployment**. Mandá una captura. |
| "Publicado, pero no se pudo pedir la actualización de la página" | Lo publicado quedó guardado, pero la página no se rearmó sola. | En Cloudflare, **Deployments** y **Retry deployment**; o publicar otra vez más tarde. |
| "Guardado como publicado, pero falta configurar la actualización automática (ver README)" | Falta el aviso automático de la instalación. | Volver a la guía de instalación (paso del Deploy Hook: Settings > Builds, que puede llamarse Builds & deployments, > Deploy hooks). |
| "esa imagen ya no existe, subila de nuevo" | Una foto se perdió. | Subirla otra vez en el bloque y publicar. |
| La página dice "Página en preparación" | Todavía no hay contenido publicado: falta tocar **Preparar mi página**, o la página todavía no se armó de nuevo. | Entrar al panel: si muestra "Tu página todavía no está preparada", tocar **Preparar mi página** (ver la guía de instalación). Si ya está preparada, esperar 1 o 2 minutos ("Actualizando tu página…") y, si sigue igual, **Deployments** y **Retry deployment**. |
| Un bloque no aparece | Está **Oculto** o **Sin completar**. | Tocar **Mostrar** o completar el dato. |

Si no sabe qué hacer: que mande una captura y **nunca pegue contraseñas, tokens ni URLs de deploy hook en el chat** (si lo hizo, se borran o regeneran en Cloudflare ahora mismo).

## Qué se cambia en el panel y qué se cambia con la IA

| En el panel | Con la IA (cambio de marca) |
|---|---|
| Textos, links, orden, fotos | Colores y fuentes |
| Agregar, ocultar y borrar bloques | El título de la pestaña y la descripción para compartir |
| Nota al pie (**Editar perfil**) | Si Google puede encontrar la página (`noindex`) |
| Ver clics | Idioma de los textos automáticos |

Un bloque nuevo de un tipo que no existe no se puede crear: solo están los cinco.

## Volver a la IA más adelante (rediseño)

1. Abrir un chat nuevo, pegar el mensaje de `PROMPT-PARA-CHAT.md` y adjuntar `PARA-CHAT.md` (o, con terminal, abrir la carpeta del proyecto).
2. Pasarle el `design-system.md` y el `brand/theme.json` actuales, y el resumen de la última fase si lo guardó.
3. Decir qué quiere cambiar. La IA va a leer los archivos, **mantener las reglas de contraste y de fuentes** de `references/1-sistema-de-diseno.md`, mostrar el resultado antes de entregarlo y validarlo con `references/3-archivos-de-marca.md`.
4. Subir el `theme.json` nuevo como indica la guía de instalación que se usó (4 o 5), y esperar la actualización.

**No volver a cargar el contenido inicial (`seed`) para cambiar la marca.** Una vez preparada la página, el botón **Preparar mi página** ya no aparece y el servidor se niega a repetirlo; la única forma de pisarla es el script `seed.mjs --remote --force`, que borra el borrador y lo publicado, o sea todo lo que la persona editó desde el panel. Los colores y las fuentes viven en `theme.json`, que se cambia aparte.

## Cuidar lo que se hizo

El contenido vive en Cloudflare. Pedile que guarde una copia de los archivos de `brand/` y del `design-system.md` (en una carpeta de su computadora o en una nota): son su marca, y sirven para rehacer todo si algún día hace falta.

---

**ARCHIVO: `docs/BLOQUES.md`**

# Bloques de la página de links

Referencia de los tipos de bloque para quien arma o edita una página (persona o Claude con la skill). El diseño lo ponen los bloques; vos solo ponés contenido. No hay colores ni fuentes por bloque: todo sale de `brand/theme.json`.

Contrato completo (rutas, validación, API): `docs/SPEC.md`. Íconos disponibles: `functions/_lib/icons.js`.

## Forma del documento

```json
{
  "version": 1,
  "profile": {
    "photo": "/img/perfil",
    "name": "Nombre Apellido",
    "role": "Rol · Rubro",
    "phrase": "Una frase corta con gancho.",
    "highlight": "con gancho.",
    "sub": "Una línea que aclara qué hacés."
  },
  "blocks": [],
  "footer": "Nota chica al pie (opcional)"
}
```

- `profile.photo` (obligatoria): imagen (ver Reglas). Límites del perfil: `name` (obligatorio) 60, `role` 80, `phrase` 120, `highlight` 120, `sub` 160, `footer` 160. Los límites viven en `public/admin/limits.js` (única fuente: los comparten el servidor y el panel).
- `highlight` es un fragmento exacto de `phrase`; se pinta con el color de acento y subrayado. Si no coincide exacto, se ignora y no se resalta nada.
- `footer` (la "Nota al pie" del panel, en Editar perfil): texto chico centrado al final, después de todos los bloques, hasta 160 caracteres. Vacío = no se muestra.
- Cada bloque lleva `id` (8 caracteres `a-z0-9`, único), `type` y `hidden` (`true` lo saca de la página sin borrarlo). El orden del arreglo es el orden en pantalla.

## Reglas generales

- Imagen: `/img/<id>` (subida al panel) o `https://...`. Nada más. En el documento se guarda siempre `/img/<id>`; al publicar, el build deja cada imagen subida que la página dibuja como archivo estático `/i/<id>.<ext>` (y la inlinea mientras entre en el presupuesto de 80 KB por imagen y 300 KB por página), así que quien visita nunca pasa por `/img/`. Una imagen subida que ningún bloque (ni el borrador) usa se borra al publicar, pero solo si tiene más de 24 horas.
- Link: `https://`, `mailto:` o `tel:`. Nada más.
- Todo texto: hasta 300 caracteres, salvo los límites de cada bloque. Máximo 40 bloques y 200 KB de JSON. Todo link: hasta 1000 caracteres.
- Un texto opcional vacío (`""`) o de solo espacios se trata como si no estuviera: no se dibuja.
- Íconos: claves de `ICON_KEYS` (arrow-right, chevron-right, check, mail, calendar, mic, presentation, book, user, globe, link, play, headphones, star, heart, message, phone, map-pin, gift, sparkles) y, solo en `fila.icon`, también las de `NETWORK_KEYS` (instagram, tiktok, youtube, spotify, x, linkedin, facebook, whatsapp, threads, email, web).
- En la página pública cada link de un bloque cuenta clics; en la vista previa no.
- Un bloque incompleto (le falta un campo obligatorio) no se manda al servidor: queda solo en el panel y **no se publica**. La confirmación de "Publicar" avisa cuántos bloques están así ("Hay N bloques sin completar que no se van a publicar.").
- Cada publicación regenera la página; el panel muestra "Tu página está al día" cuando la página en vivo ya trae la fecha de la última publicación.

## destacado

Tarjeta oscura con el llamado a la acción principal de la página (la oferta que más importa). Usala una sola vez, arriba.

| Campo | Obligatorio | Límite |
|---|---|---|
| `label` | no | 40 (va en mayúsculas espaciadas) |
| `title` | sí | 60 |
| `text` | no | 220 |
| `proof` | no | 90 (línea con tilde: prueba social) |
| `button` | sí | `{ text, url }`; `text` hasta 40 |

```json
{
  "id": "coaching",
  "type": "destacado",
  "hidden": false,
  "label": "Sesión 1 a 1",
  "title": "Coaching conmigo",
  "text": "45 minutos para destrabar eso que te frena y salir con un plan.",
  "proof": "Más de 650 personas ya lo hicieron.",
  "button": { "text": "Agendá tu sesión", "url": "https://ejemplo.com/coaching" }
}
```

Qué toca la marca: fondo `tinta`, textos `superficie`, etiqueta `acentoSuave`, tilde `acentoSuave`, botón `acento` con texto `superficie` y flecha; al pasar el mouse el botón toma `gradiente`. Título en `fonts.titulo`, cuerpo en `fonts.texto`. Esquinas `radius`.

## tarjeta

Tarjeta blanca para una acción secundaria (newsletter, descarga, comunidad). Puede resaltar parte del título con la fuente de acento.

| Campo | Obligatorio | Límite |
|---|---|---|
| `label` | no | 40 |
| `title` | sí | 60 |
| `highlight` | no | hasta 60; fragmento exacto de `title` |
| `text` | no | 220 |
| `button` | sí | `{ text, url, icon? }`; `text` hasta 40 (`icon` = ICON_KEYS) |

```json
{
  "id": "newslet1",
  "type": "tarjeta",
  "hidden": false,
  "label": "Newsletter",
  "title": "Desarrollo personal sin marketing",
  "highlight": "sin marketing",
  "text": "Una idea por semana. Llega los jueves.",
  "button": { "text": "Suscribirme", "url": "https://ejemplo.com/newsletter", "icon": "mail" }
}
```

Qué toca la marca: fondo `superficie` con borde `borde`; etiqueta y botón en `tinta` (botón con texto `superficie`); título en `fonts.acento`, y el fragmento resaltado en `acentoTexto` con subrayado de 2 px en `acento`; cuerpo en `texto`.

## fila

Un link en una línea, con ícono y una descripción corta. Sirve para canales, charlas, contacto, cualquier destino secundario.

| Campo | Obligatorio | Límite |
|---|---|---|
| `icon` | sí | ICON_KEYS o NETWORK_KEYS |
| `title` | sí | 50 |
| `text` | no | 90 |
| `url` | sí | link |
| `verified` | sí | `true` muestra una insignia de verificado junto al título |
| `style` | sí | `"solido"` (fondo blanco, ícono en disco de acento) o `"borde"` (transparente, solo contorno) |

```json
{
  "id": "whatsapp",
  "type": "fila",
  "hidden": false,
  "icon": "whatsapp",
  "title": "Canal de WhatsApp",
  "text": "Lo nuevo, directo en tu celular.",
  "url": "https://whatsapp.com/channel/XXXX",
  "verified": true,
  "style": "solido"
}
```

Qué toca la marca: `solido` usa `superficie` + `borde`, disco `acento` con glifo `superficie`; `borde` usa borde `bordeFondo` y disco con contorno `bordeFondo`, glifo `tinta`. Título en `fonts.titulo`, descripción en `gris`, chevron en `gris`, insignia en `acento`.

## libros

Sección de portadas. Sirve para libros, pero vale para cualquier cosa con tapa: cursos, episodios, productos. Se arma con grupos; cada grupo tiene su subtítulo y un diseño.

| Campo | Obligatorio | Límite |
|---|---|---|
| `label` | no | 40 (encabezado de la sección) |
| `groups` | sí | hasta 3 |
| `groups[].title` | sí | 80 |
| `groups[].layout` | sí | `"destacado"` (1 ítem, tapa grande al lado del título) o `"fila"` (hasta 3 ítems en grilla de 3 columnas) |
| `groups[].items[]` | sí | `{ title, author?, linkText?, cover, url }`; `title` 80, `author` 60, `linkText` 40; `cover` = imagen |
| `groups[].items[].linkText` | no | 40; solo se usa en un grupo `destacado`: texto del link chico (por defecto "Ver libro") |
| `more` | no | `{ text, url }`: link de texto al final ("Ver todos…"); `text` hasta 40 |

```json
{
  "id": "libros01",
  "type": "libros",
  "hidden": false,
  "label": "Mis libros",
  "groups": [
    {
      "title": "Mi primer libro",
      "layout": "destacado",
      "items": [{ "title": "Título del libro", "cover": "/img/abc123", "url": "https://ejemplo.com/libro", "linkText": "Ver en la librería" }]
    },
    {
      "title": "Los clásicos, comentados",
      "layout": "fila",
      "items": [
        { "title": "Manual de vida", "author": "Epicteto", "cover": "/img/def456", "url": "https://ejemplo.com/a" },
        { "title": "Meditaciones", "author": "Marco Aurelio", "cover": "/img/ghi789", "url": "https://ejemplo.com/b" }
      ]
    }
  ],
  "more": { "text": "Ver todos mis libros", "url": "https://ejemplo.com/libros" }
}
```

Notas: las portadas se muestran a 90 x 135 px (proporción 2:3, recortadas a ese tamaño). En un grupo `destacado` el link de texto dice "Ver libro" salvo que el ítem tenga `linkText`. En la métrica de clics, los ítems se numeran en orden corrido a través de todos los grupos (0, 1, 2...) y el link `more` toma el número siguiente al último ítem (en el panel de estadísticas se rotula con el texto de `more`).

Qué toca la marca: encabezado de sección en `fonts.titulo` color `tinta`; subtítulos de grupo en `gris`; títulos de libro en `fonts.titulo`, autor en `gris`; sombra de portada derivada de `tinta`; links de texto en `tinta` con subrayado de 2 px y flecha en `acento` (nunca naranja oscuro en texto chico); al pasar el mouse el link toma `acentoTexto`.

## redes

Círculos con los íconos de redes sociales. Se muestran en fila, centrados, al final (poné el bloque último, antes del `footer`).

| Campo | Obligatorio | Límite |
|---|---|---|
| `items[]` | sí | hasta 8: `{ network, url }` con `network` de NETWORK_KEYS |

```json
{
  "id": "redes001",
  "type": "redes",
  "hidden": false,
  "items": [
    { "network": "instagram", "url": "https://instagram.com/usuario" },
    { "network": "youtube", "url": "https://www.youtube.com/@usuario" },
    { "network": "email", "url": "mailto:hola@ejemplo.com" }
  ]
}
```

Qué toca la marca: círculos de 44 px con borde `bordeFondo` e ícono `tinta`; al pasar el mouse el borde pasa a `tinta`.

## Ejemplos para el panel

La hoja "Agregar bloque" del panel le muestra al cliente cómo se ve de verdad cada tipo de bloque, con el tema de la marca. Ese contenido de ejemplo vive en `brand/examples.json`: un bloque completo y válido por tipo (`destacado`, `tarjeta`, `fila`, `libros`, `redes`), con textos en la voz de la marca y, donde sirva, sus datos reales (tapas de `brand/images/` en `libros`, sus redes en `redes`). La skill (`skill/pagina-de-links/`) los genera junto con el resto de `brand/`; si cambia el largo de un ejemplo, hay que volver a medir su altura a 440 px y actualizar `MINI_H` en `public/admin/examples.js`.

## Qué toca la marca en toda la página

| Token (`brand/theme.json`) | Dónde se usa |
|---|---|
| `colors.fondo` | fondo de la página, aro entre la foto y su borde |
| `colors.superficie` | tarjetas blancas, texto sobre fondos oscuros y sobre `acento` |
| `colors.tinta` | titulares, texto fuerte, tarjeta `destacado`, botón oscuro |
| `colors.texto` / `colors.gris` | cuerpo / texto secundario |
| `colors.borde` / `colors.bordeFondo` | bordes sobre blanco / bordes sobre el fondo |
| `colors.acento` | botón principal, disco de `fila`, subrayados, flechas, insignia |
| `colors.acentoTexto` | texto resaltado de color (frase del perfil, título de `tarjeta`) |
| `colors.acentoSuave` | etiqueta y tilde sobre la tarjeta oscura |
| `colors.gradiente` | botón principal al pasar el mouse |
| `colors.aroFoto` | aro alrededor de la foto de perfil |
| `fonts.titulo` / `texto` / `acento` | títulos y botones / cuerpo / frase del perfil y título de `tarjeta` |
| `grain` | `true` = textura sutil de puntos en el fondo |
| `radius` | esquinas de tarjetas y filas (px) |
| `noindex` | `true` = la página pide no ser indexada |

---

**ARCHIVO: `skill/pagina-de-links/ejemplos/marca-ficticia/theme.json`**

MUESTRA DE FORMA, no para instalar: es de Renata Olmos, una persona inventada. Los links `example.com`, los textos y los datos no existen y nunca se copian a la página de una persona real.

```json
{
  "lang": "es",
  "title": "Renata Olmos · links",
  "description": "Los links de Renata Olmos, nutricionista. Ejemplo ficticio de la skill pagina-de-links.",
  "themeColor": "#F2EEE4",
  "noindex": true,
  "fontsHref": "https://fonts.googleapis.com/css2?family=Fraunces:wght@700;800&family=Nunito+Sans:wght@400;500&family=Caveat:wght@400&display=swap",
  "fonts": { "titulo": "Fraunces", "texto": "Nunito Sans", "acento": "Caveat" },
  "colors": {
    "fondo": "#F2EEE4",
    "superficie": "#FFFFFF",
    "tinta": "#1F2A24",
    "texto": "#3A453F",
    "gris": "#5A6660",
    "borde": "#E4E0D6",
    "bordeFondo": "#D8D2C3",
    "acento": "#2F855A",
    "acentoTexto": "#276749",
    "acentoSuave": "#9ADBB4",
    "gradiente": "linear-gradient(135deg,#2F855A 0%,#276749 90%)",
    "aroFoto": "linear-gradient(180deg,#9ADBB4,#2F855A)"
  },
  "grain": true,
  "radius": 14
}
```

---

**ARCHIVO: `skill/pagina-de-links/ejemplos/marca-ficticia/seed.json`**

MUESTRA DE FORMA, no para instalar: es de Renata Olmos, una persona inventada. Los links `example.com`, los textos y los datos no existen y nunca se copian a la página de una persona real.

```json
{
  "version": 1,
  "profile": {
    "photo": "https://example.com/fotos/renata.jpg",
    "name": "Renata Olmos",
    "role": "Nutricionista · Comer simple",
    "phrase": "Comer bien no tiene que ser complicado.",
    "highlight": "no tiene que ser complicado.",
    "sub": "Planes reales para vidas reales, sin dietas extremas."
  },
  "blocks": [
    {
      "id": "consulta",
      "type": "destacado",
      "hidden": false,
      "label": "Primera consulta",
      "title": "Consulta de bienvenida",
      "text": "50 minutos para ordenar tu alimentación y salir con un plan que puedas sostener en tu día a día.",
      "button": { "text": "Reserva tu turno", "url": "https://example.com/reservas" }
    },
    {
      "id": "boletin1",
      "type": "tarjeta",
      "hidden": false,
      "label": "Newsletter",
      "title": "Comer bien sin culpa",
      "highlight": "sin culpa",
      "text": "Una receta simple y una idea por semana. Llega los domingos.",
      "button": { "text": "Quiero recibirlo", "url": "https://example.com/boletin", "icon": "mail" }
    },
    {
      "id": "podcast1",
      "type": "fila",
      "hidden": false,
      "icon": "headphones",
      "title": "Podcast Mesa de lunes",
      "text": "Charlas cortas para empezar la semana.",
      "url": "https://example.com/podcast",
      "verified": false,
      "style": "solido"
    },
    {
      "id": "taller01",
      "type": "fila",
      "hidden": false,
      "icon": "calendar",
      "title": "Talleres de cocina en vivo",
      "text": "Grupos chicos, una vez al mes.",
      "url": "https://example.com/talleres",
      "verified": false,
      "style": "borde"
    },
    {
      "id": "guias001",
      "type": "libros",
      "hidden": false,
      "label": "Guías gratis",
      "groups": [
        {
          "title": "Para empezar",
          "layout": "destacado",
          "items": [
            {
              "title": "Súper sin dudas",
              "cover": "https://example.com/portadas/super.jpg",
              "url": "https://example.com/guias/super",
              "linkText": "Descargar la guía"
            }
          ]
        }
      ],
      "more": { "text": "Ver todas las guías", "url": "https://example.com/guias" }
    },
    {
      "id": "redes001",
      "type": "redes",
      "hidden": false,
      "items": [
        { "network": "instagram", "url": "https://example.com/renata-instagram" },
        { "network": "youtube", "url": "https://example.com/renata-youtube" },
        { "network": "email", "url": "mailto:hola@example.com" }
      ]
    }
  ],
  "footer": "Hecha con la plantilla gratis de imagineAI"
}
```

---

**ARCHIVO: `skill/pagina-de-links/ejemplos/marca-ficticia/examples.json`**

MUESTRA DE FORMA, no para instalar: es de Renata Olmos, una persona inventada. Los links `example.com`, los textos y los datos no existen y nunca se copian a la página de una persona real.

```json
{
  "version": 1,
  "blocks": {
    "destacado": {
      "id": "ejdest01",
      "type": "destacado",
      "hidden": false,
      "label": "Primera consulta",
      "title": "Consulta de bienvenida",
      "text": "50 minutos para ordenar tu alimentación y salir con un plan que puedas sostener en tu día a día.",
      "button": { "text": "Reserva tu turno", "url": "https://example.com/reservas" }
    },
    "tarjeta": {
      "id": "ejtarj01",
      "type": "tarjeta",
      "hidden": false,
      "label": "Newsletter",
      "title": "Comer bien sin culpa",
      "highlight": "sin culpa",
      "text": "Una receta simple y una idea por semana. Llega los domingos.",
      "button": { "text": "Quiero recibirlo", "url": "https://example.com/boletin", "icon": "mail" }
    },
    "fila": {
      "id": "ejfila01",
      "type": "fila",
      "hidden": false,
      "icon": "headphones",
      "title": "Podcast Mesa de lunes",
      "text": "Charlas cortas para empezar la semana.",
      "url": "https://example.com/podcast",
      "verified": false,
      "style": "solido"
    },
    "libros": {
      "id": "ejlibr01",
      "type": "libros",
      "hidden": false,
      "label": "Guías gratis",
      "groups": [
        {
          "title": "Para empezar",
          "layout": "fila",
          "items": [
            { "title": "Súper sin dudas", "author": "Renata Olmos", "cover": "https://example.com/portadas/super.jpg", "url": "https://example.com/guias/super" },
            { "title": "Desayunos simples", "author": "Renata Olmos", "cover": "https://example.com/portadas/desayunos.jpg", "url": "https://example.com/guias/desayunos" },
            { "title": "Cenas en 20 minutos", "author": "Renata Olmos", "cover": "https://example.com/portadas/cenas.jpg", "url": "https://example.com/guias/cenas" }
          ]
        }
      ],
      "more": { "text": "Ver todas las guías", "url": "https://example.com/guias" }
    },
    "redes": {
      "id": "ejredes1",
      "type": "redes",
      "hidden": false,
      "items": [
        { "network": "instagram", "url": "https://example.com/renata-instagram" },
        { "network": "youtube", "url": "https://example.com/renata-youtube" },
        { "network": "email", "url": "mailto:hola@example.com" }
      ]
    }
  }
}
```
