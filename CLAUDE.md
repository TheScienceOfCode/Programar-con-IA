# Programar con IA

## Voz de la narración

Todas las lecciones usan la misma voz: Kokoro con el speaker `em_alex`. El valor por defecto de la CLI es `ef_dora`, que **no** es la del curso.

Siempre que produzcas audio, indica la voz explícitamente:

```bash
.autotorial/autotorial produce session-N --voice kokoro --speaker em_alex
```

- Nunca ejecutes `produce` sin `--voice kokoro --speaker em_alex`.
- La voz es parte de la clave de caché: si la sesión 1 muestra `0 generated, N cached` con estos parámetros, la voz es la correcta. Si genera audio nuevo para la sesión 1, la voz está mal.
- No modifiques ni regeneres las sesiones ya publicadas salvo que se pida.

## Duración de las lecciones

En `lessons/INDEX.md` el título de cada lección ya renderizada lleva su duración, redondeada a minutos según la longitud del MP4 (`- N minutos`). Después de renderizar (`render session-N --format mp4`), actualízala con `ffprobe -v error -show_entries format=duration -of csv=p=0 bin/autotorial/video/session-N.mp4`. No agregues columnas a la tabla: la página de inicio usa la segunda celda como título y el resto como descripción.
