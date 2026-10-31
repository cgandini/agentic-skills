# Renata Olmos: design system (para pasarle a la IA)

Ejemplo ficticio de la skill `pagina-de-links`. Renata Olmos es una persona inventada: no existe, y su web y sus redes tampoco (todos los links son de `example.com`). Las fuentes "consultadas" de abajo simulan lo que haría la skill con una persona real.
Fuentes simuladas: su web (home y página de reservas) y 6 capturas de su Instagram. Donde web e Instagram no coinciden, manda Instagram.
Pegá este archivo al principio de cada pedido de diseño o de texto.

## Regla general

Fresco, claro y con aire. Un solo color de acción (verde salvia), tinta casi negra con un toque verdoso, fondo hueso y blanco. Títulos con serif cálida, una frase a mano para darle voz humana. Casi sin sombras. Sin emojis en la página.

## Colores

Los seis centrales:

| Nombre | Hex | Dónde aparece | Uso |
|---|---|---|---|
| Verde salvia | `#2F855A` | Botones de su web, fichas de recetas en Instagram | Botón principal, discos de íconos, subrayados y flechas |
| Verde menta | `#9ADBB4` | Detalles sobre fondos oscuros en sus placas | Solo sobre tinta: etiqueta y tilde. Nunca sobre claro |
| Tinta | `#1F2A24` | Títulos y placas oscuras | Texto fuerte y bloques oscuros. Nunca negro puro |
| Hueso | `#F2EEE4` | Fondo de su web y de sus placas, con grano sutil | Fondo de la página |
| Blanco | `#FFFFFF` | Tarjetas de su web | Tarjetas y texto sobre fondos oscuros |
| Verde profundo | `#276749` | No aparece en sus piezas | Derivado: palabra destacada en letra grande y fin del degradé del botón |

Apoyo: Texto `#3A453F`, Gris `#5A6660`, Borde `#E4E0D6` (líneas sobre blanco) y Borde sobre fondo `#D8D2C3`.

Derivados para accesibilidad (no son suyos):

- Verde profundo `#276749`: misma familia que el verde salvia (tono 152 contra 150), solo más oscuro. Se usa para la palabra destacada en letra grande.
- **Texto chico: nunca en el color de acento.** Va en tinta (`#1F2A24`) o en texto (`#3A453F`), y el verde queda como subrayado, flecha o ícono.
- Degradé del botón al pasar el cursor: de `#2F855A` a `#276749`, para que el texto blanco no pierda contraste.

Contraste (calculado; sobre 4,5 se lee cómodo en letra chica, sobre 3 en letra grande):

| Combinación | Ratio | Cuándo |
|---|---|---|
| `#1F2A24` sobre `#F2EEE4` | 12,81 | Títulos y nombre |
| `#3A453F` sobre `#FFFFFF` | 9,99 | Cuerpo de las tarjetas |
| `#5A6660` sobre `#F2EEE4` | 5,17 | Rol y subtítulo |
| `#5A6660` sobre `#FFFFFF` | 5,99 | Descripción de las filas |
| Blanco sobre `#1F2A24` | 14,84 | Tarjeta oscura |
| `#9ADBB4` sobre `#1F2A24` | 9,30 | Etiqueta y tilde de la tarjeta oscura |
| Blanco sobre `#2F855A` | 4,54 | Texto del botón |
| `#276749` sobre `#F2EEE4` | 5,80 | Frase del perfil (letra grande) |
| `#276749` sobre `#FFFFFF` | 6,73 | Título de la tarjeta (letra grande) |
| `#2F855A` sobre `#F2EEE4` | 3,92 | Solo decoración: subrayados y flechas |

## Tipografía (Google Fonts)

```html
<link href="https://fonts.googleapis.com/css2?family=Fraunces:wght@700;800&family=Nunito+Sans:wght@400;500&family=Caveat:wght@400&display=swap" rel="stylesheet">
```

| Rol | Fuente | Pesos | Dónde |
|---|---|---|---|
| Títulos | **Fraunces** | 700 y 800 | Nombre (en mayúsculas), títulos, botones, etiquetas |
| Texto | **Nunito Sans** | 400 y 500 | Cuerpo, descripciones, rol |
| Acento | **Caveat** | 400 | Solo la frase del perfil y el título de las tarjetas |

Tres fuentes en total, y la de acento en dos lugares. Fraunces se parece a la serif de sus títulos en Instagram y Caveat a su letra manuscrita en las placas de recetas.

## Bordes y detalles

| Dónde | Valor |
|---|---|
| Tarjetas y filas | radio `14px` |
| Contornos | 1 px `#E4E0D6` sobre blanco y `#D8D2C3` sobre el fondo |
| Fondo | hueso con textura de puntos muy sutil (`grain: true`) |
| Sombras | casi ninguna: solo la de las tapas de las guías |

## Componentes

**Botón principal** (en la tarjeta oscura): fondo `#2F855A`, texto blanco, Fraunces 700, forma de píldora. Al pasar el cursor, degradé hacia `#276749`.
**Tarjeta**: blanca, borde fino, título en Caveat con la palabra clave en verde profundo y subrayada en verde salvia.
**Fila**: ícono en disco verde (estilo sólido) o solo contorno (estilo borde). Sin sombra.
**Links chicos**: texto en tinta, subrayado de 2 px en verde salvia y flecha verde.

## Tono

Le habla a una persona, no a un público: como una amiga que sabe de nutrición y no te reta. Usa tuteo ("reserva", "descarga"). Evita: promesas de resultados, "detox", "quemar", culpa y exclamaciones en cadena.

- **Ganchos que desarman una creencia:** "Comer bien no tiene que ser complicado".
- **Números chicos y concretos:** "50 minutos", "20 minutos".
- **Objetos que vuelven:** la olla, la tabla de cortar, el domingo de compras.
- **Emojis:** nunca en la página. En Instagram puede haber uno al final de un gancho.
- **Línea de prueba social:** no hay ninguna en la página porque este ejemplo no tiene un dato real que la respalde.

## Mapa a la plantilla

`theme.json`: `fondo` `#F2EEE4`, `superficie` `#FFFFFF`, `tinta` `#1F2A24`, `texto` `#3A453F`, `gris` `#5A6660`, `borde` `#E4E0D6`, `bordeFondo` `#D8D2C3`, `acento` `#2F855A`, `acentoTexto` `#276749`, `acentoSuave` `#9ADBB4`, `gradiente` de `#2F855A` a `#276749`, `aroFoto` de `#9ADBB4` a `#2F855A`; fuentes Fraunces, Nunito Sans y Caveat; `grain` sí; `radius` 14.

## Lo que falta confirmar

- Las fuentes son las Google Fonts más cercanas a lo que se ve en las capturas, no las que usa ella.
- Los colores se midieron sobre capturas comprimidas y pueden variar unos puntos.
- Las fotos del ejemplo son links de `example.com`: en una página real van la foto de la persona y las tapas de sus guías.
