# Prompt 2: tu página de links

Para usar **sin la skill**. Con el design system que armaste con el prompt 1, la IA te arma tu página de links en un solo archivo HTML. Es una página fija: para cambiar un link, le pedís el cambio a la IA. Si querés un panel para editarla vos desde el celular, usá la skill completa (`SKILL.md`).

## Cómo se usa

1. Tené a mano tu design system (el archivo del prompt 1) y tu foto.
2. Copiá el recuadro de abajo y reemplazá todo lo que está entre [CORCHETES].
3. Si no tenés alguno de los puntos (por ejemplo, libros), **borrá esa línea entera**. No dejes corchetes sin completar.
4. En la lista, poné los links **de mayor a menor importancia**: el primero es lo único que más querés que haga quien entra.
5. Pegalo en el chat, adjuntá el design system y tu foto.
6. Miralo en tu celular. Pedí los cambios que quieras.

## El prompt

```
Con el design system de [TU NOMBRE] que te adjunto, armame mi página de links para el celular, en un solo archivo HTML. Tiene que verse como mi marca y no como un Linktree genérico.

Ordená los links por importancia, en vez de ponerlos todos iguales uno abajo del otro. Si a partir de lo que ves en mi design system tenés mejoras para hacer en el orden o en los links, sentite libre de proponerlas y explicame por qué en una frase cada una.

1. Arriba de todo, mi foto (te la adjunto), mi nombre ([TU NOMBRE]), mi rol ([TU ROL · TU RUBRO]) y una frase corta con mi estilo. Proponé la frase en mi tono y mostrame un par de opciones.
2. Lo principal, destacado: [TU OFERTA PRINCIPAL] ([LINK]). Con un botón claro: [TEXTO DEL BOTÓN, por ejemplo "Agendá tu sesión"].
3. [TU ACCIÓN SECUNDARIA, por ejemplo mi newsletter o una descarga gratis] ([LINK]), con un botón claro para [LA ACCIÓN].
4. [OTRO DESTINO, por ejemplo mi canal de WhatsApp o mi podcast] ([LINK]).
5. [MIS LIBROS / CURSOS / PRODUCTOS], en una fila de tapas:
   - [NOMBRE DEL PRIMERO]: [LINK]
   - [NOMBRE DEL SEGUNDO]: [LINK]
6. Al pie, íconos de mis redes: [RED 1] ([LINK]), [RED 2] ([LINK]) y [RED 3] ([LINK]).

Al final de la página poné, chiquito: [TU TEXTO CHICO, o borrá esta línea].

Reglas:
- Usá solamente los links que te di. No inventes links, números ni testimonios. Si algo falta, dejalo afuera y avisame.
- El texto chico no va en el color de acento; va en la tinta. El acento es para subrayados, flechas e íconos.
- Sin emojis: usá íconos.
- Las tipografías son las del design system, todas de Google Fonts.
- Tiene que verse perfecta en un celular de 390 píxeles de ancho y cargar rápido.
- Cada link abre en una pestaña nueva.
```

## Después

Revisá que cada link lleve a donde tiene que llevar (tocalos todos desde el celular) y que ningún texto diga algo que no es cierto. Para publicar tu página gratis en internet si elegiste esta ruta estática, guardá el archivo como `index.html` dentro de una carpeta vacía en tu computadora. En `cloudflare.com` entrá a **Workers & Pages** > **Create**, abrí la pestaña **Pages**, tocá **Upload assets**, arrastrá esa carpeta y listo. Si en cambio querés el panel `/admin/` para editar links y subir fotos desde el celular, usá `PROMPT-PARA-CHAT.md` (o `SKILL.md`), no este archivo HTML fijo.
