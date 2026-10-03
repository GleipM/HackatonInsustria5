# Plan: detección de plagas por foto (lo que falta)

Este documento es para quien continúe esta función. Resume qué ya quedó armado, qué se decidió, qué sigue abierto y en qué orden conviene atacarlo. Todo vive en `index.html` (archivo único, sin build, sin servidor — ver "Restricciones" abajo antes de cambiar la arquitectura).

## Contexto: qué problema resuelve

En la vista Técnico, pestaña "Plagas", ya existía un bloque para capturar manualmente el conteo de trampas del día (`tiz`/`mos`/`tuta`). La idea es que, además de escribir el número a mano, el técnico pueda tomar o subir una foto de la trampa y que una IA de visión sugiera qué plaga hay y cuántos individuos — como ayuda, no como fuente de verdad (la recomendación sigue "pendiente de validar", igual que el resto de la app).

## Qué ya está hecho (funcional, probado)

Todo dentro de `index.html`:

- **Captura de foto real**: botón "Tomar foto de la trampa" abre la cámara (`getUserMedia`) en un modal (`#camModal`, líneas ~883-892), con botón "Capturar" que toma el frame a un `<canvas>` oculto y lo guarda como `dataURL` JPEG. Botón "Cancelar" y tecla Escape cierran el modal y detienen el stream de la cámara (`openCamera()` / `closeCamera()`, líneas 1178-1196).
- **Subida de foto alternativa**: input de archivo (`#trapPhotoFile`) para cuando no hay cámara o el navegador no da permiso (líneas 1207-1214).
- **La foto se guarda por día del ciclo**, en `S.trapPhotos[S.day]` (igual que `S.traps[S.day]` ya guarda los conteos numéricos). Se resetea al entrar a un lote nuevo (línea 1582) y al cambiar de día se muestra la foto de ese día o el estado vacío (`renderTrapPhoto()`, líneas 1171-1177, enganchada en `renderTrapInputs()`).
- **Vista previa + quitar foto**: miniatura de 140×140, botón "Quitar foto".
- **Botón "Analizar con IA (próximamente)"**: existe y es clickeable, pero es un *stub* honesto — solo muestra el mensaje "La detección automática todavía no está conectada a un proveedor de visión. Por ahora, registra el conteo a mano abajo." (línea 1216-1217). **Esto es lo que falta conectar de verdad.**
- Responsive y modo oscuro probados (360px–1920px). Sin errores de consola.

IDs/funciones clave para quien siga:
| Elemento | Qué es |
|---|---|
| `#trapPhotoBox`, `#trapPhotoEmpty`, `#trapPhotoPreview`, `#trapPhotoImg` | Contenedor de la foto del día |
| `#trapCamBtn`, `#camModal`, `#camVideo`, `#camShoot`, `#camCancel`, `#camCanvas` | Flujo de cámara |
| `#trapPhotoFile` | Subida alterna por archivo |
| `#trapPhotoAnalyze`, `#trapPhotoMsg` | Botón de análisis (stub) y su mensaje de estado |
| `S.trapPhotos` | `{ [díaDelCiclo]: dataURL }` |
| `renderTrapPhoto()` | Repinta la foto del día actual |

## Decisiones ya tomadas (no las reabras sin volver a hablarlo con el equipo)

1. **Sin backend.** Seguimos en GitHub Pages, un solo archivo HTML, sin servidor propio.
2. **Proveedor de visión en la nube**, no un modelo entrenado a mano (se descartó Teachable Machine / COCO-SSD por ahora).
3. **Para resolver la tensión "API en la nube" + "sin servidor"**: cada quien pega **su propia API key**, que se guarda solo en su navegador (`localStorage`), igual que ya hace la cuenta local. La app llama directo desde el navegador a la API del proveedor. Esto se debe anunciar en pantalla tan explícitamente como el aviso de "cuenta local, sin servidor ni cifrado" que ya existe en el login — **nunca** ocultar que la clave es visible ahí.
4. **Se integra con lo existente**, no reemplaza el simulador: vive dentro de "Conteo de trampas del día" en la vista Técnico, no es una pantalla nueva aparte.

## Lo que falta decidir

**Proveedor de visión** — quedó pendiente de investigar, no elegido:

| Opción | A favor | En contra |
|---|---|---|
| Claude (Anthropic) vision | Buena calidad describiendo imágenes; el SDK tiene un modo explícito `dangerouslyAllowBrowser` pensado para llamadas directas desde el navegador en prototipos | Hay que revisar límites de uso/CORS reales al momento de implementar, no solo de memoria |
| Google Gemini vision | Nivel gratuito generoso; la API REST (`generativelanguage.googleapis.com`) acepta la key como query param y normalmente se usa así desde el navegador en demos | Verificar también política de CORS y cuotas vigentes |

Antes de escribir código de integración, confirmar con una prueba mínima (una sola llamada `fetch` desde el navegador, sin librería) que el proveedor elegido responde sin bloqueo de CORS. Si bloquea, la alternativa sin backend se cae y hay que volver a decidir (aceptar un backend chiquito, o cambiar de proveedor).

## Lo que falta construir, en orden sugerido

1. **Prueba de humo del proveedor**: un `fetch` suelto desde la consola del navegador (no hace falta que esté en la app todavía) confirmando que la API responde a una imagen de prueba sin CORS ni backend.
2. **Campo para la API key**: un input (tipo password, con botón mostrar/ocultar como el de la contraseña del login) donde el técnico la pega. Guardarla en `localStorage` bajo una clave propia (ej. `"visionApiKey"`), **nunca** mezclada con la cuenta/lote. Mostrar el mismo tipo de aviso que ya existe en el login (`.authnote`, línea ~56) sobre que es local y visible.
3. **Reemplazar el stub de `$("trapPhotoAnalyze").onclick`** (línea 1216) por la llamada real: tomar el `dataURL` de `S.trapPhotos[S.day]`, mandarlo a la API con un prompt acotado a identificar **solo** las plagas que ya modela la app (mosquita blanca, palomilla del tomate) o "no identificado" — no pedirle que invente especies fuera de ese catálogo.
4. **Mostrar el resultado como sugerencia, no como dato final**: igual que el resto de la app, nunca autocompletar `S.traps[S.day]` sin que el técnico confirme. Por ejemplo: mostrar "La IA sugiere: mosquita blanca, ~6 individuos — revisa y escribe el conteo arriba" en `#trapPhotoMsg`, pero dejar que el técnico siga siendo quien escribe el número final en los inputs `.trapInput`.
5. **Manejo de errores honesto**: sin clave configurada → mensaje claro con el paso 2; clave inválida o error de red → mensaje claro, nunca fallar en silencio ni inventar un resultado.
6. **Actualizar la documentación del proyecto** una vez esté conectado de verdad (no antes, para no prometer algo que no existe):
   - `README.md`: agregar la función a "Qué hace".
   - `preguntas-jurado.md`: agregar una pregunta honesta tipo "¿la detección por foto es confiable?" (siguiendo el formato de las preguntas 11 y 12 ya existentes).
   - `manual-usuario.md` / `.pdf`: cómo usar la cámara y de dónde sacar/pegar la API key.

## Restricciones del proyecto (no romperlas)

- Nunca inventar datos ni fingir que una función funciona si no está conectada de verdad (por eso el botón de análisis hoy es un mensaje honesto, no un resultado falso).
- Nunca recomendar un agroquímico específico, con o sin IA de por medio.
- Toda detección queda "pendiente de validar" por el técnico, igual que las recomendaciones de riego.
- Mantener el patrón de un solo archivo `index.html`, sin servidor, deploy directo a GitHub Pages.
- Si se prueba con Playwright, usar Chrome real con cámara simulada: `chromium.launch({channel:'chrome', args:['--use-fake-device-for-media-stream','--use-fake-ui-for-media-stream']})` — así se probó este primer tramo.
