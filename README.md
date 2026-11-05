# Monitor de HS80

Monitor independiente de batería para **Corsair HS80 RGB Wireless** en Windows. La aplicación se llama **HS80 Battery** y muestra el porcentaje junto al reloj, con estimaciones de autonomía y carga al pasar el ratón por su icono.

**Versión disponible: 1.2.1.** Proyecto no oficial, sin afiliación con Corsair.

## Descargar e instalar

[**Descargar el instalador para Windows**](https://github.com/minysito/monitor-hs80/releases/latest)

1. En la última release, descarga `Monitor-HS80-Setup-v1.2.1.exe`. No necesitas los archivos “Source code”.
2. Si ya tienes la app abierta, pulsa su icono junto al reloj y elige **Salir**. La X solo oculta la ventana.
3. Ejecuta el instalador y pulsa **Instalar y abrir**.
4. Elige si quieres **Iniciar con Windows**. También puedes cambiar esta opción desde la app.

La instalación es para tu usuario, sin administrador y sin instalar Python. Incluye acceso desde Inicio, una guía `LEEME.txt` y desinstalación desde Aplicaciones de Windows.

El instalador no está firmado digitalmente. Comprueba su procedencia y el archivo `SHA256SUMS.txt` de la release.

## Qué hace

- Consulta batería y estado de carga **cada 60 segundos**, también minimizada.
- Muestra porcentaje redondeado en la bandeja y un rayo cuando carga. La ventana y el tooltip conservan la décima que comunica el firmware.
- Al pasar el ratón por el icono, muestra porcentaje y **tiempo estimado hasta 0 %**, o **hasta 100 % cuando carga**. El tiempo solo aparece en el tooltip.
- Aprende de tu consumo y conserva un **historial local**, separado para carga y descarga.
- Interfaz gamer oscura, con animaciones distintas de carga y descarga. La animación se pausa al minimizar.

| Estado | Color |
| --- | --- |
| Descarga, desde 40 % | Verde |
| Descarga, desde 20 % hasta menos de 40 % | Naranja |
| Descarga, por debajo de 20 % | Rojo |
| Cargando | Azul |

No configura RGB, ecualizador, sidetone, micrófono ni servicios de Corsair. La consulta no necesita iCUE abierto y no incluye sus servicios ni su APO. No sustituye los controladores de Windows que requiere el dispositivo.

## Bandeja, cierre e inicio con Windows

- **X o Minimizar:** oculta la ventana y mantiene las consultas.
- **Doble clic en el icono:** abre la ventana.
- **Actualizar ahora:** fuerza una lectura sin esperar al siguiente minuto.
- **Icono → Salir:** termina la aplicación.
- **Iniciar con Windows:** arranca oculta en la bandeja al iniciar sesión con tu usuario. Espera quince segundos para permitir que cargue el escritorio; si Windows rechaza el icono, reintenta cada cinco segundos.

Windows puede colocar el icono dentro de la flecha de iconos ocultos. Puedes arrastrarlo a la zona visible.

## Cómo se estima el tiempo

Al principio muestra **«calculando»** hasta observar al menos cinco minutos y dos puntos porcentuales de cambio. Si ya existe historial, puede usar el ritmo aprendido desde la primera lectura válida.

Combina la tendencia de hasta dos horas de observaciones continuas con el historial. Da más peso al ritmo reciente y va reduciendo la influencia del antiguo. Guarda hasta 256 ventanas válidas de consumo, como máximo cada quince minutos después de la primera.

Carga y descarga se aprenden por separado. Una desconexión, suspensión prolongada, cambio de modo o salto anómalo reinicia la observación continua, conservando lo aprendido. Si falta una lectura actual o no se conoce el estado de carga, no presenta una estimación antigua como actual.

**Es una aproximación:** el porcentaje procede del firmware, el consumo cambia con el uso y la carga puede ralentizarse cerca del 100 %. Los tiempos se redondean a cinco minutos; por debajo se muestra «< 5 min». No se ha contrastado la precisión con un ciclo físico completo hasta 0 % o 100 %.

## Compatibilidad y límites comprobados

- Probado en **Windows 11 x64** con HS80 RGB Wireless por dongle y por cable USB de datos.
- Windows 10, HS80 MAX y otros modelos no están verificados.
- El auricular debe estar encendido. Si detecta conexión USB directa, consulta esa ruta; en caso contrario utiliza el dongle.
- iCUE u otros controladores HID/RGB pueden interferir con la lectura. Si hay problemas, cierra esas aplicaciones y vuelve a consultar.
- La versión 1.2.1 pasó 28 pruebas automáticas y pruebas del ejecutable: inicio oculto desde System32, cierre con X hacia la bandeja, lectura en segundo plano y restauración.
- El arranque automático después de un reinicio real sigue pendiente de confirmación; el registro de errores permite investigarlo.

## Datos locales y privacidad

La app no envía las mediciones a un servidor. No se publica tu historial con esta descarga.

| Elemento | Ubicación |
| --- | --- |
| Instalación | `%LOCALAPPDATA%\Programs\HS80Battery` |
| Historial de consumo y carga | `%LOCALAPPDATA%\HS80Battery\battery-history.json` |
| Registro de arranque y errores | `%LOCALAPPDATA%\HS80Battery\app.log` |

El historial contiene ritmo, duración, variación del porcentaje, modo y fecha. Se conserva al actualizar y al desinstalar. El log tiene tamaño limitado. El inicio automático utiliza una entrada de tu usuario en Windows.

## Resolución de problemas

**No veo el icono al iniciar sesión:** espera al menos quince segundos, revisa los iconos ocultos y comprueba que Windows no haya deshabilitado HS80 Battery en Aplicaciones de inicio. Abre la app desde Inicio y vuelve a activar su casilla si procede. Si continúa fallando, revisa `app.log`.

**Aparece «sin lectura»:** enciende el auricular, revisa el dongle o el cable de datos, cierra otras apps que accedan al HS80 y pulsa Actualizar ahora. La app reintenta cada minuto.

**Sigue en «calculando»:** necesita un cambio medible de porcentaje en el modo actual. No genera horas ficticias a partir de una batería que aún no ha variado.

**El instalador no puede reemplazar archivos:** usa icono → Salir; pulsar X no termina el proceso. Vuelve a ejecutar el instalador.

## Información de esta publicación

Este repositorio distribuye el instalador y la documentación de uso. No contiene las capturas de investigación, configuraciones personales ni el historial de batería del desarrollador. Las dependencias y sus avisos se describen en [THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md).

Para comunicar un fallo, abre una [incidencia](https://github.com/minysito/monitor-hs80/issues) indicando versión, Windows, modelo, cable/dongle y pasos para reproducirlo. Revisa cualquier log antes de compartirlo.
