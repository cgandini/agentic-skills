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
