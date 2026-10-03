# Simulador de riego y riesgo de plagas para jitomate (Morelos)

Demo del hackatón Industria 5.0. La versión entregable es `index.html`: se abre en el navegador, sin servidor ni instalación, y es el mismo archivo que sirve GitHub Pages en la URL raíz del repo. Tiene botón para cambiar entre modo claro y oscuro.

**Demo en vivo:** https://gleipm.github.io/HackatonInsustria5/

Zona de ejemplo: valle de Cuautla–Ayala–Yautepec, Morelos. Cultivo: jitomate.

## Qué hace

- **Cuenta y lotes:** landing page → inicio de sesión con correo y contraseña (cuenta local del navegador, sin servidor) → pestaña **Resumen** (los lotes que más necesitan atención hoy: riego o riesgo de plagas) y pestaña **Mis lotes** (alta, edición y baja de lotes con sus propios datos). El selector de cultivo ya incluye nopal, caña y maíz, deshabilitados, para mostrar que el sistema puede crecer; solo jitomate tiene simulación activa.
- **Vista Productor:** responde en lenguaje sencillo si hoy toca regar y cuánta agua aplicar, muestra el agua que queda en el suelo, el nivel de riesgo de plagas, los próximos 7 días y cuánta agua se ahorra frente al calendario del productor.
- **Vista Técnico:** compara calendario, balance hídrico, riego deficitario y goteo frecuente; acepta CSV de clima, captura humedad medida y conteos de trampas (con foto de la trampa por cámara o archivo y, opcionalmente, una sugerencia de conteo de mosquita blanca y palomilla del tomate hecha por IA de visión con Gemini, usando la API key propia del técnico guardada solo en su navegador; la sugerencia nunca se guarda sola), muestra precisión/cobertura exploratorias y resume agua, ahorro, estrés y alertas.
- **Revisión humana:** toda recomendación queda como "pendiente de validación" hasta que el técnico la valide. La herramienta nunca recomienda un agroquímico.

## Cómo funciona

- ETo con el método de Hargreaves–Samani y demanda del cultivo ETc = ETo × Kc por etapa.
- Balance de agua diario en la zona de raíces.
- Rendimiento relativo con la relación de Doorenbos y Kassam (solo para comparar estrategias, no para predecir cosecha).
- Índices de riesgo de 0 a 100 para tizón tardío, mosquita blanca y palomilla del tomate, con temperatura y lluvia de los últimos días.

## Estado de los datos (léelo antes de presentar)

- **El clima es sintético** (tres ciclos de ejemplo) o el CSV que cargues. Formato: `fecha,tmax,tmin,lluvia` y, opcional, `hr`. No se pudo confirmar una descarga de estación SMN/CONAGUA en esta sesión.
- **Kc y duración de etapas** ahora usan la referencia FAO-56, Tablas 11 y 12; siguen pendientes de calibración en Morelos. `p` y `Ky` siguen siendo editables y pendientes.
- **Los umbrales de plagas son reglas simples**; las métricas de trampas solo son exploratorias con los conteos que se capturen.
- **El calendario del productor (14 mm cada 3 días) es un supuesto**; el ahorro mostrado depende de él.
- No se ha probado con productores ni con datos de campo.

La pestaña "Supuestos" de la vista Técnico etiqueta cada parámetro como método, ejemplo o por confirmar. El detalle de fuentes está en `fuentes.md`.

## Entregables

- `index.html`: MVP funcional sin servidor.
- `fuentes.md`: cifras, parámetros, etiquetas `[V]`, `[S]` y `[P]`, y procedimiento para SIAP/INEGI.
- `manual-usuario.md` / `manual-usuario.pdf`: guía de uso para productor y técnico.
- `pitch-jitomate-atento.pptx`: 8 láminas ordenadas para la rúbrica.
- `guion-pitch.md`: guion de 3 minutos.
- `preguntas-jurado.md`: preguntas difíciles y respuestas honestas.
- `plan-despliegue.md`: arquitectura PWA, consultas de IA por foto, capacidad para 50-200 usuarios, seguridad, fases y pruebas.
