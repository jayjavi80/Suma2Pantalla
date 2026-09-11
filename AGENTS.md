# Instrucciones del proyecto — Juegos educativos HTML de AVACOM

Estas instrucciones se aplican a este proyecto y pueden reutilizarse en futuros juegos educativos HTML de AVACOM incorporando este archivo a la raíz de cada proyecto.

## Regla principal

Si una solicitud puede cumplirse modificando una parte específica del código, modificar solamente esa parte y conservar todo lo demás.

## Preservar el código

- No eliminar código, funciones, estilos, elementos HTML o recursos existentes salvo que el usuario lo solicite expresamente.
- No eliminar funcionalidades existentes sin autorización explícita.
- No reescribir el proyecto completo cuando solo se solicite una modificación puntual.
- Mantener la estructura general del proyecto y el código organizado.
- No modificar archivos que no sean necesarios para la solicitud.

## Juegos educativos AVACOM y tecnología

- Los proyectos deben funcionar directamente en navegador.
- Priorizar HTML5, CSS3 y JavaScript nativos cuando sea posible.
- Evitar dependencias innecesarias.
- No agregar frameworks, librerías o dependencias externas sin autorización.
- Utilizar Phaser cuando sea necesario; si no está incorporado al proyecto, solicitar autorización antes de agregarlo.
- Mantener los recursos locales existentes.

## Pantallas táctiles

- Los juegos deben ser compatibles con interacción táctil.
- No introducir cambios que dificulten el uso simultáneo por varios jugadores.
- Los botones y elementos interactivos deben tener un área táctil adecuada.
- Evitar depender exclusivamente del teclado o del mouse.

## Diseño responsive

- Los juegos deben adaptarse a diferentes tamaños, resoluciones y relaciones de aspecto.
- No asumir una resolución física específica.
- No utilizar dimensiones fijas que provoquen desbordamientos.
- Evitar desplazamientos horizontales y elementos cortados.
- Cuando se solicite una resolución virtual, mantener la lógica visual proporcional sin romper otras pantallas.
- Mantener una resolución lógica de 1920x1080 cuando sea apropiado para el proyecto o se solicite, sin imponer esa resolución física a la pantalla.

## Compatibilidad

- Mantener compatibilidad con Windows, Chrome, Edge y Android WebView.
- Comprobar la disponibilidad de las API del navegador antes de utilizarlas cuando puedan no estar disponibles en los entornos compatibles.

## Compatibilidad offline

- Priorizar recursos locales.
- No introducir dependencias de Internet para funciones esenciales del juego.
- Si un recurso externo ya existe, no eliminarlo sin autorización, pero señalarlo como dependencia.

## Funcionalidad

- No cambiar reglas del juego, puntuaciones, tiempos, número de jugadores, sonidos, idioma o mecánicas salvo que el usuario lo solicite.
- Mantener compatibilidad con las funcionalidades existentes.

## Modificaciones

- Antes de realizar cambios importantes, explicar qué archivos y funciones se modificarán.
- Realizar cambios pequeños y controlados, limitados a lo solicitado.
- Después de modificar, revisar errores de sintaxis y referencias a recursos.
- Informar claramente qué se cambió y qué comprobaciones se realizaron.

## Git

- Antes de cambios importantes, comprobar `git status` y preservar los cambios existentes del usuario.
- No ejecutar `git reset`, `git clean`, `git checkout` destructivo, `git push --force` ni comandos que puedan eliminar trabajo sin autorización explícita.
- No crear commits automáticamente salvo que el usuario lo solicite.
- No hacer push automáticamente a GitHub salvo que el usuario lo solicite.

## Antes de terminar

- Revisar errores de sintaxis JavaScript cuando se modifique código JavaScript.
- Para cambios que afecten al juego, revisar la consola, comprobar la adaptación a diferentes resoluciones y comprobar el funcionamiento táctil, incluido el uso simultáneo por varios jugadores cuando corresponda.
- Revisar que los recursos utilizados existan y que sus referencias sean correctas cuando se modifique el juego o sus recursos.
- Si alguna comprobación no se puede realizar, indicarlo claramente sin presentarla como realizada.
