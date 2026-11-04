# Claqueta

> **Estado: beta.** Puede cambiar sin aviso y hay partes sin probar con material real (ver [Limitaciones](#limitaciones)).

**Claqueta** es un catálogo de metadatos de rodaje. Arrastras vídeos, audio o carpetas a la página y **el navegador lee los metadatos del fichero local: el vídeo nunca se sube**. Anotas escena, plano, toma, versión, valoración y comentarios, y exportas al montaje (DaVinci Resolve) o a un parte diario.

**Web:** <https://claqueta.caravana.dev/> · **Descargas:** [Releases](../../releases)

Este repositorio solo contiene las **descargas** y su documentación.

## Web o portátil: cuándo usar cada una

| | **Web** (<https://claqueta.caravana.dev/>) | **Claqueta portátil** (Windows o macOS) |
|---|---|---|
| Úsala cuando… | tienes conexión y quieres **guardar y consultar el catálogo** desde cualquier equipo, o probar sin instalar nada | estás **en el set o sin internet**, o prefieres que nada salga de tu equipo |
| Instalación | ninguna, solo un navegador (probado con Chrome) | descomprimir y abrir `Claqueta.bat` |
| Cuenta | **No hace falta para importar** y rellenar. Sí para **guardar** y ver el catálogo | no hace falta |
| Dónde se guarda | en el servidor, por cuenta (100 MB cada una) | en la carpeta `datos` de tu equipo |
| Vídeo | se lee en tu navegador y **no se sube** | se lee en tu equipo |

**Flujo típico:** en el set, con la portátil, catalogas las tarjetas sin conexión. Al volver, entras en la web y usas «Subir al servidor» para pasar lo hecho a tu cuenta, sin duplicar clips. Desde ahí exportas a Resolve o imprimes el parte diario.

### Cómo usar la web

1. Abre <https://claqueta.caravana.dev/>.
2. **Importar:** arrastra ficheros o una carpeta (una carpeta de `.dng` cuenta como una secuencia). El navegador lee los metadatos.
3. Rellena escena, plano, toma, versión, valoración y comentarios. Para guardar la ruta real del fichero, copia las rutas con *Ctrl+Mayús+C* en el Explorador de Windows y pégalas en la página.
4. **Guardar:** al pulsarlo pide entrar con correo y contraseña, o crear una cuenta. Sin cuenta puedes seguir trabajando, pero no se guarda.
5. **Catálogo, parte diario y exportación** (CSV, CSV y script para Resolve) están en la misma web, ya con tu cuenta.

**Cuentas:** en «Entrar» hay una pestaña **«Crear cuenta»** (nombre, correo y contraseña). Te registras tú mismo, sin esperar a nadie, y entras en el acto con 100 MB de espacio. Cada cuenta ve solo sus proyectos. No se verifica el correo (Claqueta no envía correo), y el administrador puede cerrar el registro. Los **administradores** pueden proteger su cuenta con verificación en dos pasos (Google Authenticator, con códigos de recuperación).

**Privacidad:** el vídeo nunca se sube. Al servidor solo van los metadatos y el texto que escribes, más una miniatura del fotograma central. En ProRes, DNxHD, MXF y CinemaDNG esa miniatura la hace el servidor, así que **ese único fotograma** (o el DNG central) se envía para convertirlo y se borra al terminar.

## Qué se descarga

| Fichero | Para qué | Tamaño |
|---|---|---|
| `Claqueta-portatil-windows.zip` | **Claqueta portátil Windows**: Claqueta completa para **Windows 10/11**, autónoma: lleva PHP, ffmpeg y LibRaw. Sin internet, sin instalación y sin cuenta. | ~125 MB |
| `Claqueta-portatil-macos-apple-silicon.zip` | **Claqueta portátil macOS** para Macs con chip Apple (M1, M2, M3, M4…): lleva PHP y ffmpeg. | ~40 MB |
| `Claqueta-portatil-macos-intel.zip` | **Claqueta portátil macOS** para Macs con **procesador Intel**. | ~45 MB |
| `Claqueta.lua` | Script para **DaVinci Resolve** (también la versión gratuita, sin Python) que importa el material catalogado con sus metadatos. | ~20 KB |

## A quién va dirigido

- **Equipos de rodaje pequeños** (cortos, documental, publicidad, eventos) que graban en formatos pesados —Blackmagic RAW, ProRes RAW, CinemaDNG— y quieren saber qué hay en cada tarjeta sin copiarla.
- **Script, data wrangler o DIT** que anota la jornada sobre la marcha.
- **Montadores con DaVinci Resolve** que quieren recibir escena, plano y toma ya rellenados.

No es un gestor de activos ni un programa de copia y verificación de tarjetas.

## Cómo se usa la portátil

### Windows

1. Descarga `Claqueta-portatil-windows.zip` de la última Release y descomprímelo donde quieras.
2. Abre `Claqueta.bat`. Se abre el navegador en `http://127.0.0.1:8099/`. Deja abierta la ventana negra mientras trabajas.
3. Arrastra tarjetas o carpetas, rellena escena, plano y toma.
4. Exporta desde «Exportar»: CSV, parte diario o script de Resolve.

Todo queda en la carpeta `datos` junto al `.bat`. Para actualizar, descomprime la versión nueva y copia en ella tu carpeta `datos`.

La primera vez Windows puede pedir permiso para instalar el runtime de Visual C++ (viene incluido). Claqueta solo atiende a tu propio equipo (127.0.0.1), no a la red.

### macOS

> **Sin probar en un Mac real.** Está montada con binarios ya compilados (PHP de static-php-cli y ffmpeg de osxexperts.net) y la aplicación se ha comprobado en Linux con el mismo contenido del ZIP, pero no en macOS. Si algo falla, abre un *issue*.

1. Elige tu versión: menú Apple › *Acerca de este Mac*. Con «Chip: Apple…» es `apple-silicon`; si pone Intel, `intel`.
2. Descomprime el ZIP.
3. **Primera vez:** macOS bloquea lo descargado. Abre la Terminal, escribe `xattr -dr com.apple.quarantine ` (con un espacio al final), arrastra la carpeta `Claqueta` a la ventana y pulsa Intro. Si prefieres, clic derecho en `Claqueta.command` › *Abrir*, y *Ajustes del Sistema › Privacidad y seguridad › Permitir de todos modos* si lo pide.
4. Abre `Claqueta.command`. Se abre el navegador en `http://127.0.0.1:8099/`. Deja abierta la ventana de Terminal mientras trabajas.

Todo queda en la carpeta `datos`. **Diferencia con Windows:** LibRaw no se puede incluir en macOS, así que los CinemaDNG se catalogan igual pero **sin miniatura**, salvo que instales LibRaw con Homebrew (`brew install libraw`), que Claqueta detecta solo.

## Cómo se usa el script de Resolve

1. Copia `Claqueta.lua` en `%APPDATA%\Blackmagic Design\DaVinci Resolve\Support\Fusion\Scripts\Utility\`.
2. En Resolve: *Workspace › Scripts › Claqueta*.
3. El script lee de un servidor Claqueta (dirección y clave de cuenta). Esta descarga **no lleva ninguna dirección ni clave**: pon las tuyas dentro del fichero o en la ventana del script. Si tienes tu propio servidor Claqueta, lo más cómodo es descargar el script desde él, que ya las incluye.

## Qué lee

| Formato | Qué sale |
|---|---|
| Blackmagic RAW | códec, compresión, resolución, fps, TC, cámara y la **claqueta de la cámara** (escena, toma, carrete…) |
| ProRes y ProRes RAW | perfil, TC, audio |
| MXF, MP4, MOV, MKV… | lo anterior, y GPS y fecha en los de móvil |
| CinemaDNG | una carpeta de `.dng` forma una secuencia: fotogramas, fps, TC, cámara, ISO, obturador… |
| WAV, BWF | se catalogan como sonido directo |

Además: reconocimiento y emparejado de **proxies**, miniatura del fotograma central y sonido directo emparejado por timecode.

## Limitaciones

- **ProRes RAW** sin probar con un fichero real.
- **BRAW sin miniatura** a propósito (el SDK de Blackmagic exige registro).
- El script de **Resolve** solo se ha verificado con un simulador y una primera pasada real; puede necesitar ajustes de campos.
- La portátil de **Windows** es la probada (y la que también se descarga desde la web, ya con la dirección del servidor puesta); la de **macOS** no se ha probado en un Mac real y no hace miniaturas de CinemaDNG sin Homebrew. Probado con Chrome.
- «Subir al servidor» desde la portátil pide la dirección del servidor, tu correo y tu contraseña (y el código de dos pasos si la cuenta lo tiene). En la portátil no hay registro: la cuenta se crea antes en la web.

## Componentes de terceros

El ZIP incluye PHP 8.4 (php.net), ffmpeg 8.1 (BtbN, GPL), LibRaw 0.21 (LGPL), [mediainfo.js](https://mediainfo.js.org/) (BSD-2) y el runtime de Visual C++ de Microsoft. Las licencias de ffmpeg y LibRaw están en `herramientas\` dentro del ZIP. El código fuente de ffmpeg está disponible en el proyecto de BtbN y en <https://ffmpeg.org>.

## Licencia

Claqueta se distribuye tal cual, sin garantía, para uso propio. No se concede licencia para redistribuirla ni modificarla; las piezas de terceros mantienen las suyas.
