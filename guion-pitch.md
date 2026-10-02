# Guion de pitch: 3 minutos

## 0:00-0:25 | Problema
En el valle Cuautla-Ayala-Yautepec, un productor de jitomate toma decisiones de riego con información incompleta y las plagas se detectan tarde. El reto no es solo producir más: es anticipar, perder menos agua y reducir pérdidas logísticas sin quitarle la decisión a la persona que trabaja la parcela.

## 0:25-0:50 | Evidencia y alcance
El equipo parte de la cifra reportada por INEGI para Morelos en el Censo Agropecuario 2022: 1,397 hectáreas y 67,618 toneladas de jitomate; 59.7% de la producción, 40,380 toneladas, corresponde a agricultura protegida. La cifra de SIAP 2023 que circula no se presenta como comparable: está pendiente descargar y filtrar el archivo oficial.

## 0:50-1:25 | Solución
Presentamos un simulador sencillo para celular. Calcula demanda de agua con temperatura, etapa del cultivo y balance diario. Compara el calendario del productor, el balance hídrico, el riego deficitario y goteo con aplicaciones pequeñas y frecuentes. También estima un riesgo de monitoreo para tizón tardío, mosquita blanca y palomilla del tomate.

## 1:25-1:55 | Industria 5.0 y personas
La recomendación no llega sola al productor: queda pendiente de validación de un técnico agrónomo. El productor puede registrar cuánto aplicó. El técnico puede cargar clima por CSV, capturar humedad medida por sensor o tensiómetro y añadir conteos de trampas. Así, la tecnología aprende de la parcela y mantiene supervisión humana.

## 1:55-2:25 | Demo e impacto medible
En la demo elegimos uno de tres climas de ejemplo, avanzamos al día actual y vemos una respuesta directa: hoy toca regar o hoy no riegues. En la vista técnica vemos agua usada, ahorro frente al calendario, días de estrés y alertas. Con conteos, aparecen precisión y cobertura exploratorias. Son indicadores del piloto, no resultados ya comprobados.

## 2:25-2:50 | Viabilidad
El MVP funciona sin servidor y acepta CSV. El siguiente paso es una prueba de pocas parcelas con datos de estación oficial, caudal real, humedad, conteos y cosecha. La solución escala por parámetros versionados por zona y cultivo, con validación agronómica antes de emitir recomendaciones.

## 2:50-3:00 | Cierre
No prometemos una receta automática. Prometemos una decisión mejor informada, medible y validada por personas: anticipar el riesgo, usar el agua necesaria y aprender del lote real.

## Nota para la demo
Decir explícitamente que el clima, el sensor si se simula y los conteos si se capturan como ejemplo están marcados en pantalla. No presentar ahorro, rendimiento relativo, precisión o cobertura como resultado real.
