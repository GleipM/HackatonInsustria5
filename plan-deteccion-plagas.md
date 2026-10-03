# Plan: detección de plagas por foto

Este documento es para quien continúe esta función. Resume qué ya quedó armado, qué se decidió, qué sigue abierto y en qué orden conviene atacarlo. Todo vive en `index.html` (archivo único, sin build, sin servidor — ver "Restricciones" abajo antes de cambiar la arquitectura).

## Contexto: qué problema resuelve

En la vista Técnico, pestaña "Plagas", ya existía un bloque para capturar manualmente el conteo de trampas del día (`tiz`/`mos`/`tuta`). La idea es que, además de escribir el número a mano, el técnico pueda tomar o subir una foto de la trampa y que una IA de visión sugiera qué plaga hay y cuántos individuos — como ayuda, no como fuente de verdad (la recomendación sigue "pendiente de validar", igual que el resto de la app).

## Qué ya está hecho (funcional, probado)

Todo dentro de `index.html`:

- **Captura de foto real**: botón "Tomar foto de la trampa" abre la cámara (`getUserMedia`) en un modal (`#camModal`, líneas ~883-892), con botón "Capturar" que toma el frame a un `<canvas>` oculto y lo guarda como `dataURL` JPEG. Botón "Cancelar" y tecla Escape cierran el modal y detienen el stream de la cámara (`openCamera()` / `closeCamera()`, líneas 1178-1196).
- **Subida de foto alternativa**: input de archivo (`#trapPhotoFile`) para cuando no hay cámara o el navegador no da permiso (líneas 1207-1214).
- **La foto se guarda por día del ciclo**, en `S.trapPhotos[S.day]` (igual que `S.traps[S.day]` ya guarda los conteos numéricos). Se resetea al entrar a un lote nuevo (línea 1582) y al cambiar de día se muestra la foto de ese día o el estado vacío (`renderTrapPhoto()`, líneas 1171-1177, enganchada en `renderTrapInputs()`).
- **Vista previa + quitar foto**: miniatura de 140×140, botón "Quitar foto".
- **Botón "Analizar con IA"**: originalmente un *stub* honesto; ya está conectado a Gemini (ver "Estado al 2026-10-02" abajo).
- Responsive y modo oscuro probados (360px–1920px). Sin errores de consola.

IDs/funciones clave para quien siga:
| Elemento | Qué es |
|---|---|
| `#trapPhotoBox`, `#trapPhotoEmpty`, `#trapPhotoPreview`, `#trapPhotoImg` | Contenedor de la foto del día |
| `#trapCamBtn`, `#camModal`, `#camVideo`, `#camShoot`, `#camCancel`, `#camCanvas` | Flujo de cámara |
| `#trapPhotoFile` | Subida alterna por archivo |
| `#trapPhotoAnalyze`, `#trapPhotoMsg` | Botón de análisis y su mensaje de estado/sugerencia |
| `#aiKeyBox`, `#aiKeyInput`, `#aiKeyToggle`, `#aiKeySave`, `#aiKeyClear` | Panel de la API key de Gemini |
| `analyzeTrapPhoto()`, `AI_PROMPT`, `AI_SCHEMA`, `AI_MODEL` | Llamada a Gemini, prompt y esquema JSON |
| `S.trapPhotos` | `{ [díaDelCiclo]: dataURL }` |
| `renderTrapPhoto()` | Repinta la foto del día actual |

## Decisiones ya tomadas (no las reabras sin volver a hablarlo con el equipo)

1. **Sin backend.** Seguimos en GitHub Pages, un solo archivo HTML, sin servidor propio.
2. **Proveedor de visión en la nube**, no un modelo entrenado a mano (se descartó Teachable Machine / COCO-SSD por ahora).
3. **Para resolver la tensión "API en la nube" + "sin servidor"**: cada quien pega **su propia API key**, que se guarda solo en su navegador (`localStorage`), igual que ya hace la cuenta local. La app llama directo desde el navegador a la API del proveedor. Esto se debe anunciar en pantalla tan explícitamente como el aviso de "cuenta local, sin servidor ni cifrado" que ya existe en el login — **nunca** ocultar que la clave es visible ahí.
4. **Se integra con lo existente**, no reemplaza el simulador: vive dentro de "Conteo de trampas del día" en la vista Técnico, no es una pantalla nueva aparte.

## Estado al 2026-10-02: conectado a Gemini

**Proveedor elegido: Google Gemini**, modelo `gemini-3.8-flash` (Flash estable con nivel gratuito, para que el jurado pueda probar con su propia key de AI Studio). Llamada REST directa a `models/gemini-3.8-flash:generateContent` con la key en el header `x-goog-api-key` (no en la URL, para que no quede en historial/logs) y salida JSON forzada con `responseSchema`.

Lo hecho, todo en `index.html`:

- **Prueba de CORS (paso 1)**: preflight desde un origen `https://gleipm.github.io` contra Gemini y Anthropic → ambos responden `Access-Control-Allow-Origin` y los errores (clave inválida) también llegan legibles al navegador.
- **Campo de API key (paso 2)**: `<details id="aiKeyBox">` bajo la foto, input password con botón ojo (`#aiKeyInput`, `#aiKeyToggle`), "Guardar clave"/"Borrar clave". Se guarda en `localStorage["visionApiKey"]`, separado de cuentas y lotes. Aviso `.authnote` explícito: clave local, visible, sin cifrado; la foto se envía a Google y en el nivel gratuito puede usarse para mejorar sus productos.
- **Llamada real (paso 3)**: `analyzeTrapPhoto()` reduce la foto a máx. 1600 px JPEG (`shrinkPhoto()`), manda `AI_PROMPT` + `AI_SCHEMA`. El prompt se limita a mosquita blanca y palomilla del tomate; otras especies solo se marcan como `otros_insectos` sin nombrarlas; prohíbe recomendar productos.
- **Resultado como sugerencia (paso 4)**: texto en `#trapPhotoMsg` ("La IA sugiere (confianza …): Mosquita blanca: ~6 …", más la nota de la IA y el recordatorio "pendiente de validar"). **Nunca** escribe en `.trapInput` ni en `S.traps`. Si la respuesta llega después de cambiar de día o de foto, se descarta.
- **Errores honestos (paso 5)**: sin clave (abre el panel de clave), clave inválida (400), sin permiso (401/403), cuota (429), sin red, respuesta bloqueada, sin texto o JSON ilegible: cada uno con su mensaje, nunca un resultado inventado.
- **Docs (paso 6)**: `README.md`, `preguntas-jurado.md` (pregunta 13) y `manual-usuario.md` actualizados.
- **Probado** con Playwright + Edge: flujo sin clave, clave inválida contra la API real de Gemini, y respuestas simuladas (éxito, "no es trampa", sin red, 429, cambio de día a mitad del análisis). 360 px en oscuro sin scroll horizontal, sin errores de JS.

### Lo que sigue pendiente

- **Probar con una key real y fotos reales de trampas.** Todavía no se ha hecho una llamada exitosa real (no había key disponible al implementar); el camino de éxito solo se probó con respuesta simulada. Hacerlo antes de la demo: si `gemini-3.8-flash` rechazara el `responseSchema` o el nombre del modelo, el error se mostraría en pantalla tal cual.
- **Regenerar `manual-usuario.pdf`** a partir del `.md` actualizado.
- **Medir el error de la sugerencia** contra conteos manuales antes de decir cualquier número de precisión.

## Decisión de proveedor (histórico)

Comparación que se hizo antes de elegir Gemini:

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
