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
