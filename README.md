# Claqueta — descargas

> **Estado: beta.** Puede cambiar sin aviso y hay partes sin probar con material real (ver [Limitaciones](#limitaciones)).

**Claqueta** es un catálogo de metadatos de rodaje. Arrastras vídeos, audio o carpetas a la página y **el navegador lee los metadatos del fichero local: el vídeo nunca se sube**. Anotas escena, plano, toma, versión, valoración y comentarios, y exportas al montaje (DaVinci Resolve) o a un parte diario.

Este repositorio solo contiene las **descargas** y su documentación. Los ficheros están en [**Releases**](../../releases/latest).

## Qué se descarga

| Fichero | Para qué | Tamaño |
|---|---|---|
| `Claqueta-portatil.zip` | Claqueta completa para **Windows 10/11**, autónoma: lleva PHP, ffmpeg y LibRaw. Sin internet, sin instalación y sin cuenta. | ~125 MB |
| `Claqueta.lua` | Script para **DaVinci Resolve** (también la versión gratuita, sin Python) que importa el material catalogado con sus metadatos. | ~20 KB |

## A quién va dirigido

- **Equipos de rodaje pequeños** (cortos, documental, publicidad, eventos) que graban en formatos pesados —Blackmagic RAW, ProRes RAW, CinemaDNG— y quieren saber qué hay en cada tarjeta sin copiarla.
- **Script, data wrangler o DIT** que anota la jornada sobre la marcha.
- **Montadores con DaVinci Resolve** que quieren recibir escena, plano y toma ya rellenados.

No es un gestor de activos ni un programa de copia y verificación de tarjetas.

## Cómo se usa (portátil)

1. Descarga `Claqueta-portatil.zip` de la última Release y descomprímelo donde quieras.
2. Abre `Claqueta.bat`. Se abre el navegador en `http://127.0.0.1:8099/`. Deja abierta la ventana negra mientras trabajas.
3. Arrastra tarjetas o carpetas, rellena escena, plano y toma.
4. Exporta desde «Exportar»: CSV, parte diario o script de Resolve.

Todo queda en la carpeta `datos` junto al `.bat`. Para actualizar, descomprime la versión nueva y copia en ella tu carpeta `datos`.

La primera vez Windows puede pedir permiso para instalar el runtime de Visual C++ (viene incluido). Claqueta solo atiende a tu propio equipo (127.0.0.1), no a la red.

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
- Solo Windows para la versión portátil. Probado con Chrome.
- «Subir al servidor» requiere un servidor Claqueta propio; no se ofrece ninguno público.

## Componentes de terceros

El ZIP incluye PHP 8.4 (php.net), ffmpeg 8.1 (BtbN, GPL), LibRaw 0.21 (LGPL), [mediainfo.js](https://mediainfo.js.org/) (BSD-2) y el runtime de Visual C++ de Microsoft. Las licencias de ffmpeg y LibRaw están en `herramientas\` dentro del ZIP. El código fuente de ffmpeg está disponible en el proyecto de BtbN y en <https://ffmpeg.org>.

## Licencia

Claqueta se distribuye tal cual, sin garantía, para uso propio. No se concede licencia para redistribuirla ni modificarla; las piezas de terceros mantienen las suyas.
