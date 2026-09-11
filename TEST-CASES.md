# Pruebas de Suma2Pantalla

Lista pendiente de ejecución basada en el código actual y en los requisitos de `AGENTS.md`. Ninguna casilla acredita una prueba realizada. Registrar navegador y versión, dispositivo, resolución CSS, número de jugadores, conexión y resultado al ejecutar. Los tamaños propuestos son escenarios de prueba, no compatibilidad ya certificada. No modificar archivos para ejecutar estas pruebas.

## 1 jugador

- [ ] Seleccionar 1: solo aparece Jugador 1; completar la partida y comprobar que el ranking contiene únicamente ese jugador y sus puntos.

## 2 jugadores

- [ ] Seleccionar 2: aparecen únicamente Jugador 1 y Jugador 2; responder en ambos y comprobar puntuaciones independientes con un temporizador común.

## 3 jugadores

- [ ] Seleccionar 3: aparecen tres paneles; completar la partida y comprobar que el cuarto jugador no interviene ni aparece en el ranking.

## 4 jugadores

- [ ] Abrir el juego: hay cuatro jugadores seleccionados; completar una partida respondiendo en los cuatro paneles y comprobar que cada respuesta afecta solo a su jugador.

## Inicio

- [ ] Abrir `suma2.html` directamente en navegador: comprobar estado de espera, 60 segundos, puntuaciones a cero, inicio habilitado y reinicio deshabilitado.
- [ ] Cambiar el número de jugadores antes de iniciar: comprobar paneles visibles, selección activa y puntuaciones a cero.
- [ ] Pulsar Iniciar repetidamente: comprobar que solo se inicia una cuenta regresiva y una partida.

## Cuenta regresiva

- [ ] Iniciar: comprobar secuencia 3, 2, 1 con intervalos previstos de un segundo, seguida de «¡YA!» o «GO!» durante aproximadamente 700 ms.
- [ ] Durante la preparación, comprobar que no se consumen los 60 segundos y que inicio, reinicio y selección de jugadores están deshabilitados.

## Temporizador

- [ ] Mantener la pestaña activa: comprobar descenso desde 60, una unidad por segundo aproximadamente, y finalización al llegar a cero.
- [ ] Comprobar cambio de color en los últimos 10 segundos y animación de pulso en los últimos 5.
- [ ] Intentar responder tras finalizar: comprobar que no se suman puntos.
- [ ] Llevar la pestaña a segundo plano y volver: registrar la duración real frente al contador; el código no compensa retrasos mediante un reloj absoluto.

## Aciertos y generación de ejercicios

- [ ] Resolver correctamente: comprobar incremento exacto de un punto, feedback positivo y nuevo ejercicio tras aproximadamente 260 ms.
- [ ] Pulsar varias veces la respuesta correcta antes del siguiente ejercicio: comprobar que ese botón solo otorga un punto.
- [ ] Revisar varios ejercicios: operandos entre 1 y 9, cuatro opciones distintas entre 2 y 18 y exactamente una respuesta correcta; no exigir ejercicios diferentes consecutivos.
- [ ] Contar las manzanas y comparar las operaciones horizontal y vertical: deben representar los mismos operandos.

## Errores

- [ ] Elegir una opción incorrecta: comprobar feedback negativo, puntuación intacta y permanencia del ejercicio.
- [ ] Fallar y luego acertar: comprobar que se permite reintentar y se obtiene un único punto por el acierto.

## Reinicio

- [ ] Reiniciar durante una partida: comprobar que se detiene el contador, se borran ejercicios y puntos, se restauran 60 segundos y se requiere pulsar Iniciar nuevamente.
- [ ] Acertar y reiniciar antes de 260 ms; esperar más de un segundo: no debe aparecer un nuevo ejercicio ni feedback pendiente. Repetir con respuestas de varios jugadores.
- [ ] Reiniciar tras un error y tras varios aciertos rápidos: comprobar que no quedan tareas visuales pendientes que afecten a la siguiente partida.
- [ ] Pulsar Jugar de Nuevo en el resultado: comprobar cierre del ranking y vuelta a espera conservando jugadores, idioma y estado de música.

## Ranking

- [ ] Completar con puntuaciones distintas: verificar orden descendente, puntos exactos y presencia exclusiva de los jugadores seleccionados.
- [ ] Obtener cuatro puntuaciones distintas: comprobar oro, plata, bronce y estrella, en ese orden.
- [ ] Comparar puntuaciones antes y después de generar el ranking: no deben cambiar.

## Empates

- [ ] Conseguir puntuaciones 2, 2, 1, 0: comprobar posiciones equivalentes a 1, 1, 3, 4 mediante oro, oro, bronce y estrella.
- [ ] Conseguir puntuaciones 2, 1, 1, 0: comprobar posiciones equivalentes a 1, 2, 2, 4 mediante oro, plata, plata y estrella.
- [ ] Terminar con todos a cero: comprobar oro compartido e indicador final de cero puntos; repetir con 2, 3 y 4 jugadores.
- [ ] Empatar en cabeza con puntos positivos: comprobar que el indicador final identifica a todos los ganadores empatados.

## Pantalla completa

- [ ] En un navegador que permita la API, entrar y salir con el botón: comprobar cambio de estado y texto sin reiniciar la partida.
- [ ] Salir con el mecanismo del navegador: comprobar que el botón refleja el estado actualizado.
- [ ] En un entorno sin `requestFullscreen`, pulsar el botón: comprobar que no produce un error JavaScript ni interrumpe el juego.
- [ ] En un entorno que rechace la solicitud, comprobar que su promesa rechazada no produce un error sin capturar.

## Audio

- [ ] Tras la primera interacción, comprobar reproducción de música local en bucle y coherencia del indicador; registrar si el navegador bloquea la reproducción.
- [ ] Después de inicializar el audio, apagar y encender la música: comprobar pausa y reanudación sin afectar tiempo ni puntos.
- [ ] Con conexión y recursos disponibles, comprobar efectos de inicio, acierto, error, final y celebración local.
- [ ] Con música apagada, comprobar que los efectos siguen habilitados: el control no es un silencio global.
- [ ] Bloquear la reproducción de audio desde el entorno de prueba: comprobar que el juego continúa y no aparecen excepciones de reproducción sin capturar.

## Cambio de idioma

- [ ] Alternar español e inglés en espera: comprobar título del documento, etiquetas, controles y nombres de jugadores.
- [ ] Cambiar idioma durante la partida: comprobar conservación de puntos, ejercicios y tiempo, y actualización del feedback textual.
- [ ] Iniciar y terminar una partida en cada idioma: comprobar mensajes de preparación y ranking en el idioma seleccionado.

## Pantalla táctil

- [ ] Completar una partida usando únicamente toques, incluidos selección, inicio, respuestas y reinicio.
- [ ] Con 2, 3 y 4 jugadores, tocar respuestas simultáneamente en paneles distintos: comprobar registros independientes y ausencia de bloqueos o dobles puntuaciones.
- [ ] Probar toques rápidos, pulsación prolongada y varios contactos: registrar el efecto del bloqueo global de gestos sin asumir que garantiza multitáctil.
- [ ] Comprobar que las áreas de toque son cómodas y que desplazar el área de juego permite alcanzar todos los paneles sin respuestas accidentales.

## Diferentes resoluciones

- [ ] Probar 360 × 640, 640 × 360, 768 × 1024, 1024 × 768, 1366 × 768 y 1920 × 1080 píxeles CSS con 1 a 4 jugadores: comprobar legibilidad, controles accesibles y ausencia de recortes o desplazamiento horizontal.
- [ ] Probar justo antes y en los anchos 640, 1080 y 1440: comprobar cambios de columnas previstos para cada número de jugadores.
- [ ] Probar alturas 600 y 601 con ancho desde 640, y paneles alrededor de 560 de ancho: comprobar disposición de opciones, manzanas y operación vertical.
- [ ] Girar o redimensionar durante la partida: comprobar conservación de puntuaciones y continuidad del temporizador.
- [ ] Revisar cuenta regresiva y ranking en pantallas pequeñas: comprobar acceso al botón final y desplazamiento vertical cuando sea necesario.

## Recursos locales

- [ ] Comprobar existencia y carga de `img/Recurso 6.png` y `img/AVACOM-LOGO.png` respetando nombres y rutas.
- [ ] Comprobar existencia y reproducción de `sonidos/musicafondo.mp3` y `sonidos/triunfo.mp3`.
- [ ] Confirmar que `img/AsistenteAVACOM.png` sigue existiendo aunque no tenga referencia en el HTML.
- [ ] Simular fallos de carga de los logos mediante herramientas del navegador, sin eliminar archivos: comprobar texto SUMA2 alternativo y ocultación del logo AVACOM fallido.

## Funcionamiento offline

- [ ] Con caché vacía y sin conexión, abrir el archivo local y completar una partida: comprobar ejercicios, puntuación, temporizador, ranking y reinicio.
- [ ] Sin conexión, comprobar imágenes y MP3 locales; registrar fallos de banderas y efectos externos como dependencias existentes.
- [ ] Confirmar que los fallos de recursos externos no bloquean las funciones esenciales ni generan excepciones JavaScript sin capturar; distinguirlos de errores de red.

## Compatibilidad con navegador

- [ ] En Chrome sobre Windows, ejecutar el flujo completo y registrar versión, audio, pantalla completa y diseño.
- [ ] En Edge sobre Windows, ejecutar el flujo completo y registrar versión, audio, pantalla completa y diseño.
- [ ] En Android WebView real, ejecutar el flujo completo y registrar versión, aplicación contenedora, audio, API de pantalla completa, diseño e interacción multitáctil.

## Errores de JavaScript

- [ ] Validar la sintaxis del bloque JavaScript de `suma2.html` sin modificar el archivo.
- [ ] Mantener la consola abierta durante inicio, respuestas, reinicio, cambio de idioma y final: comprobar ausencia de excepciones sin capturar.
- [ ] Repetir varias partidas cambiando entre 1 y 4 jugadores: comprobar que no se acumulan intervalos, no se acelera el contador y no se duplican puntos.
