# Especificación de Suma2Pantalla

Documento basado en la lectura de `suma2.html`, `AGENTS.md` y los recursos locales. Describe la implementación actual; no certifica pruebas en dispositivos reales.

## Nombre y objetivo general

- Nombre mostrado: Suma2 / SUMA2. Proyecto: Suma2Pantalla.
- Objetivo observable en la mecánica: practicar sumas y obtener puntos al resolverlas durante una partida con tiempo limitado.
- Archivo principal: `suma2.html`.

## Jugadores y duración

- De 1 a 4 jugadores locales en una misma pantalla; selección inicial de 4.
- Cada jugador tiene ejercicios y puntuación propios; todos comparten el temporizador.
- Duración configurada: 60 segundos (`TOTAL_TIME`). Se descuenta una unidad mediante `setInterval` cada 1000 ms; no se utiliza un reloj absoluto para compensar retrasos del navegador.
- Antes de jugar se muestra 3, 2, 1 y luego «¡YA!» o «GO!» durante 700 ms. Esta preparación no consume el tiempo de partida.

## Mecánica, puntuación y generación de ejercicios

- Cada ejercicio suma dos enteros aleatorios entre 1 y 9, ambos incluidos.
- La operación se representa horizontalmente, con dos grupos de manzanas y en formato vertical.
- Se ofrecen cuatro respuestas distintas entre 2 y 18: una correcta y tres distractores. Su orden se mezcla aleatoriamente.
- Acertar suma 1 punto al jugador, muestra feedback positivo, intenta reproducir un sonido y programa otro ejercicio tras 260 ms.
- El botón acertado queda bloqueado contra otra puntuación durante esa transición.
- Fallar no resta puntos ni cambia el ejercicio: permite volver a intentar, muestra feedback negativo e intenta reproducir un sonido.
- Las respuestas solo puntúan durante una partida activa y para jugadores seleccionados.
- No hay progresión de dificultad ni almacenamiento persistente de puntuaciones en el código.
- Reiniciar cancela los `setTimeout` registrados y el intervalo de partida, borra ejercicios y puntos, restaura 60 segundos y vuelve a espera. Conserva el número de jugadores, idioma y estado de música; requiere pulsar Iniciar nuevamente.

## Sistema de ranking

- `generateRanking()` incluye únicamente los jugadores seleccionados, ordenados por puntuación descendente.
- Los empates comparten posición; la siguiente posición tiene en cuenta cuántos jugadores la preceden: 1, 1, 3, 4 o 1, 2, 2, 4.
- La posición se representa mediante medalla y estilo, sin una columna numérica: oro para primera, plata para segunda, bronce para tercera y estrella para las demás.
- Si todos obtienen cero puntos, todos comparten la primera posición y reciben oro.
- Generar la clasificación no modifica las puntuaciones.
- Al terminar, el indicador de tiempo muestra el ganador y sus puntos, los números de los ganadores empatados o cero puntos si nadie acertó.

## Pantallas principales y controles

- Espera: paneles sin ejercicios, puntuaciones a cero y controles disponibles para preparar la partida. El mensaje de espera existe en HTML, pero está oculto por CSS.
- Preparación: capa con mensaje inicial y cuenta regresiva.
- Partida: paneles de jugadores con puntuación, operación, manzanas, respuestas y feedback.
- Resultado: capa con ranking, confeti y botón para jugar de nuevo.
- Barra inferior: música, idioma, reinicio, pantalla completa, selección de 1 a 4 jugadores e inicio; también incluye logos y temporizador.
- Durante la cuenta regresiva se deshabilitan inicio, reinicio y selección de jugadores. Durante la partida se habilita reinicio, pero inicio y selección siguen deshabilitados.
- Jugar de nuevo cierra el resultado y devuelve al estado de espera.

## Interacción táctil

- Las respuestas utilizan `pointerdown` y los controles generales utilizan `click`.
- Hay reglas `touch-action: manipulation`, bloqueo de selección de texto y supresión del menú contextual.
- El código cancela `gesturestart` y el comportamiento predeterminado de `touchstart` cuando hay más de un contacto. Su efecto sobre el uso simultáneo debe verificarse en hardware real.
- Los selectores de jugadores miden 44 × 44 píxeles CSS; los controles generales tienen altura mínima de 44 píxeles y las respuestas varían según el diseño.
- Las respuestas no tienen un manejador `click` para su activación exclusiva con teclado.

## Audio

- Música de fondo local en bucle; la inicialización establece volumen 0.28 e intenta reproducirla tras la primera interacción o al iniciar.
- El botón de música pausa o reanuda únicamente la música de fondo; no silencia los efectos.
- Celebración final local: `sonidos/triunfo.mp3`.
- Efectos externos OGG desde `https://actions.google.com/sounds/v1/cartoon/`: `wood_plank_flicks.ogg` (acierto), `cartoon_whistle.ogg` (inicio), `metal_clang.ogg` (final) y `klaxon.ogg` (error).
- Los fallos de reproducción se capturan y no muestran un aviso. La reproducción efectiva depende del navegador y de la disponibilidad de los archivos.

## Idiomas

- Español inicial e inglés, alternables mediante el control de idioma.
- El diccionario traduce título del documento, controles, etiquetas, mensajes y nombres genéricos de jugadores. El ranking usa el idioma vigente al generarse.
- Las banderas provienen de `https://flagcdn.com/w20/es.png` y `https://flagcdn.com/w20/us.png`.
- El atributo HTML `lang` permanece en `es`; los atributos de accesibilidad estáticos no se traducen mediante `updateLanguage()`.

## Pantalla completa

- El botón solicita pantalla completa para el documento solo si `requestFullscreen` existe como función.
- Si la API no existe, no realiza la solicitud. Si la promesa de entrada se rechaza, el error se captura.
- Si ya está en pantalla completa y existe `exitFullscreen`, solicita salir.
- `fullscreenchange` actualiza el texto del botón según el estado y el idioma.

## Recursos locales

- `img/Recurso 6.png`: marca Suma2; si falla, se muestra el texto alternativo SUMA2.
- `img/AVACOM-LOGO.png`: logo AVACOM; se oculta si falla su carga.
- `img/AsistenteAVACOM.png`: archivo existente sin referencia en `suma2.html`.
- `sonidos/musicafondo.mp3`: música de fondo.
- `sonidos/triunfo.mp3`: celebración final.

## Funcionamiento offline

- El HTML incluye sus estilos y lógica; no necesita descargar un framework ni llamar a un servidor para generar ejercicios o puntuar.
- Las imágenes de marca y los dos MP3 están disponibles localmente.
- Las banderas y cuatro efectos de sonido son dependencias de Internet existentes. No se garantiza su disponibilidad sin conexión ni sin caché previa.
- No se implementa un service worker ni una estrategia explícita de caché offline.
- La ejecución completa sin conexión queda pendiente de prueba real con caché vacía.

## Adaptación responsive y resolución lógica

- Diseño DOM/CSS fluido; no existe un canvas ni una resolución lógica fija de 1920 × 1080 implementada.
- Una columna por defecto. Desde 640 píxeles CSS, los modos de 2 a 4 jugadores usan dos columnas; 3 jugadores pasan a tres desde 1080 y 4 jugadores a cuatro desde 1440.
- Se utilizan Grid, Flexbox, `clamp()`, unidades de viewport y contenedor, media queries y consultas de contenedor desde 560 píxeles de ancho.
- Hay reglas específicas para pantallas de altura máxima de 600 píxeles y para pantallas horizontales desde 1440 píxeles de ancho y 601 de alto.
- El área de juego permite desplazamiento cuando su contenido lo necesita. Los logos de la barra se ocultan hasta 1100 píxeles de ancho.
- La ausencia de recortes y la comodidad táctil en cada resolución no se han certificado mediante esta documentación.

## Tecnologías y compatibilidad

- HTML5, CSS y JavaScript nativo integrados en `suma2.html`; DOM, eventos de puntero, temporizadores, audio HTML y API de pantalla completa.
- Recursos PNG, MP3, OGG y emojis. No se utiliza Phaser ni otro framework, backend o base de datos.
- `AGENTS.md` establece Windows, Chrome, Edge y Android WebView como objetivos de compatibilidad. No especifica versiones mínimas ni acredita pruebas en ellos.

## Restricciones que requieren autorización

Según `AGENTS.md`, conservar estructura, código, estilos, elementos HTML, funcionalidades y recursos existentes. Limitar cada modificación a la parte solicitada.

No cambiar sin solicitud o autorización las reglas, puntuaciones, tiempos, número de jugadores, sonidos, idioma o mecánicas; tampoco eliminar recursos o introducir frameworks, librerías o dependencias externas. Preservar el funcionamiento táctil simultáneo, la adaptación a otras pantallas y la prioridad de recursos locales. No introducir dependencias de Internet para funciones esenciales. No hacer commits, push ni operaciones Git destructivas sin la autorización indicada en `AGENTS.md`.
