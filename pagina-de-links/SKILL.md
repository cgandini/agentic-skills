---
name: pagina-de-links
description: Guía paso a paso a cualquier persona, sin saber de código, terminal, GitHub ni Cloudflare, para tener su propia página de links para la bio (tipo Linktree pero con su marca) y un panel para editarla desde el celular, gratis. Usar cuando pidan una página de links, un link en la bio, un Linktree propio o con su marca, una página para Instagram con todos sus links, un design system para su marca personal, o en inglés a link in bio page, their own Linktree, a branded link-in-bio with an editing panel. Funciona en agentes con terminal (Claude Code, Claude desktop, Codex) y en chat de navegador (claude.ai, ChatGPT, Gemini).
---

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
