# Prompt 3: subir tu página de links a internet

Para usar **sin la skill**, en un chat de navegador (claude.ai, ChatGPT, Gemini). Sirve cuando ya tenés los archivos de tu marca (`theme.json`, `seed.json` y `examples.json`; las fotos no hacen falta, se suben después desde el panel) y querés que una IA te guíe, paso a paso, para ponerlos online con un panel para editar desde el celular. Todo gratis, sin tarjeta.

Si todavía no tenés esos tres archivos JSON, empezá directamente por `PROMPT-PARA-CHAT.md` (junto con `PARA-CHAT.md`), que te guía desde cero hasta tenerlos listos; el prompt 2 arma una página HTML fija sin panel y no genera estos archivos.

## Cómo se usa

1. Abrí un chat nuevo.
2. Copiá el recuadro de abajo, reemplazá lo que está entre [CORCHETES] y pegalo como primer mensaje.
3. Adjuntá (o pegá) el archivo `skill/pagina-de-links/references/5-instalar-sin-terminal.md` de la plantilla y tus tres archivos de marca. Si la IA puede abrir links, alcanza con la dirección de la plantilla (`https://github.com/cgandini/tu-pagina-de-links`).
4. Hacé lo que te pida, de a un paso. Si lo que ves no coincide, mandale una captura.
5. **Tu contraseña del panel la inventás vos y la guardás en tu celular. No se la escribas a la IA.**

## El prompt

```
Quiero subir mi página de links a internet con Cloudflare, gratis y sin tarjeta de crédito, y tener un panel para editarla desde el celular. Ya tengo los archivos de mi marca (theme.json, seed.json y examples.json); mis fotos las subo después desde el panel. No sé qué es una terminal, GitHub ni Cloudflare: explicame cada cosa en palabras simples la primera vez que aparece.

Guiame paso a paso siguiendo la guía "5-instalar-sin-terminal.md" que te adjunto (de la plantilla https://github.com/cgandini/tu-pagina-de-links). Si no la tengo a mano, pedímela antes de empezar.

Reglas:
1. Un solo paso por mensaje, y esperá a que te conteste. Antes de cada clic decime qué voy a ver después y qué hacer si veo otra cosa. Si lo que veo no coincide, te voy a mandar una captura.
2. No tengo terminal: vos solo conversás. Yo hago cada clic y cada copiado. Cuando haya que editar un archivo, dame el texto completo en un cuadro de código para copiarlo y pegarlo directo en GitHub, sin guardarlo en el celular. Voy a hacer la instalación desde una computadora.
3. Nunca me pidas contraseñas, tokens ni direcciones secretas por acá, y no me dejes pegarlas en el chat. Mi contraseña del panel la invento yo (4 palabras sin relación entre sí, separadas por guiones, de 12 caracteres o más) y la pego solo en Cloudflare, igual que el token y el ID de mi cuenta. Sí puedo pegarte el ID de la base de datos: no es un secreto.
4. Nunca me pidas una tarjeta de crédito. Si alguna pantalla la pide, decime que frene y qué pantalla era.
5. Hablame en mi idioma y como yo te escribo.

Mis datos: [TU NOMBRE O MARCA]. El nombre que quiero para todo (repositorio, base de datos y proyecto) es [NOMBRE-EN-MINÚSCULAS, por ejemplo ana-links].

Empecemos: decime en dos frases qué vamos a hacer y cuál es el primer paso.
```

## Después

Cuando termines, probá todo desde el celular: que la página abra, que `/admin/` pida la contraseña, que puedas cambiar un texto, publicarlo y verlo en la página en uno o dos minutos. Para el uso de todos los días, mirá `skill/pagina-de-links/references/6-uso-diario.md`.
