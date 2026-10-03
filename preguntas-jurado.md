# Preguntas difíciles del jurado

1. **¿Los 2,410 ha y 201,721 t de SIAP contradicen a INEGI?**
   Respuesta honesta: todavía no se pueden reconciliar con rigor. INEGI 2022 y la cifra atribuida a SIAP 2023 no necesariamente miden el mismo año, universo, modalidad o variable. El portal SIAP bloqueó la descarga en esta sesión. Antes de presentar, descargaremos el archivo oficial y compararemos filtros y definiciones.

2. **¿El ahorro de agua ya está demostrado en Morelos?**
   No. Es una simulación dependiente del clima sintético, el suelo y el calendario supuesto de 14 mm cada 3 días. El piloto debe medir volumen aplicado por hectárea y producción comercial en parcelas comparables.

3. **¿Por qué usan Hargreaves-Samani y no FAO Penman-Monteith?**
   Porque el MVP necesita operar con temperatura máxima y mínima cuando faltan radiación, humedad y viento. FAO-56 reconoce alternativas con datos faltantes. Con una estación confiable y datos completos, se debe contrastar o migrar a Penman-Monteith.

4. **¿Los Kc y las etapas están validados para jitomate de Morelos?**
   No. v3 usa la referencia FAO-56 para tomate y la marca como referencia, no como calibración local. Un técnico debe contrastar variedad, fecha de trasplante, cubierta y observaciones fenológicas; INIFAP debe aportar una fuente local si existe.

5. **¿El sensor es real?**
   En este MVP la captura es manual y puede provenir de sensor o tensiómetro; no hay hardware conectado. La pantalla obliga a distinguir dato capturado de dato de ejemplo. El siguiente piloto conectaría un sensor calibrado y registraría timestamp, unidad y ubicación.

6. **¿Una alerta alta significa que hay plaga?**
   No. Es una regla heurística de temperatura y lluvia para priorizar monitoreo. La confirmación requiere conteo de trampas, revisión de plantas y diagnóstico de un técnico o fitopatólogo. La herramienta nunca receta agroquímicos.

7. **¿Qué significan precisión y cobertura con pocos conteos?**
   Son métricas exploratorias, no una validación científica. En v3 precisión y cobertura se calculan solo sobre los conteos guardados; con pocos días pueden ser engañosas. El piloto debe definir muestreo, umbral de presencia y periodo de evaluación antes de reportarlas.

8. **¿El goteo representa un sistema real?**
   Todavía no completamente. v3 divide la reposición en eventos pequeños y frecuentes, pero no modela caudal, presión, uniformidad, pulsos ni sectorización. La recomendación debe ser revisada con la ficha hidráulica del lote.

9. **¿Cómo llega la recomendación al productor sin quitarle autonomía?**
   El productor recibe una respuesta sencilla, pero la recomendación permanece pendiente hasta que un técnico la valida o rechaza. La bitácora conserva la decisión y el productor puede registrar lo que realmente aplicó.

10. **¿Cómo escalan el MVP?**
    Primero se valida con pocas parcelas y técnicos: clima oficial, humedad medida, riego aplicado, fenología, conteos y cosecha. Después se versionan los parámetros por zona y cultivo, se agrega almacenamiento seguro y se evalúa el modelo por temporada. No se debe escalar una regla sin calibración.

11. **¿El login y la cuenta son seguros?**
    No, y lo decimos explícitamente en la propia pantalla. Es una cuenta local de la demo: correo y contraseña se guardan en texto plano en el navegador del dispositivo, sin servidor. Sirve para mostrar el concepto — iniciar sesión, administrar varios lotes, ver un resumen diario — no para proteger datos reales. Un piloto real necesita autenticación en servidor, contraseñas con hash y cumplimiento de protección de datos personales.

12. **¿Por qué el selector de cultivo incluye nopal, caña y maíz si solo simulan jitomate?**
    Para mostrar, sin inventar nada, que la arquitectura ya está lista para más cultivos de Morelos: esas opciones aparecen deshabilitadas ("próximamente") y no se pueden crear lotes con ellas. Activar cada cultivo de verdad implica trabajar con un agrónomo especialista en su fenología, sus coeficientes de riego y sus plagas propias — no reutilizar los del jitomate.
