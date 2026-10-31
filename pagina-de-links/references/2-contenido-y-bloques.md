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
