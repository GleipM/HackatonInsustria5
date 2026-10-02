# Manual de usuario: Mi lote de jitomate

Guía de uso de `simulador-v3.html`, el simulador de riego y riesgo de plagas para jitomate del valle Cuautla–Ayala–Yautepec, Morelos.

> **Antes de empezar:** esta es una demostración. El clima, algunos conteos y la humedad pueden ser datos de ejemplo. Ningún número de esta pantalla es una medición real de tu parcela hasta que lo confirmes con datos propios. La herramienta nunca recomienda un agroquímico: cuando hay una alerta, solo dice que hay que revisar el cultivo.

## Cómo abrir el simulador

No necesita instalación ni internet para funcionar (solo la primera vez, para cargar la letra). Pasos:

1. Busca el archivo `simulador-v3.html` en la carpeta del proyecto.
2. Haz doble clic sobre él, o ábrelo arrastrándolo a una ventana del navegador (Chrome, Edge o Safari).
3. Se abre directamente en la vista **Soy productor**. Arriba a la derecha puedes cambiar a **Soy técnico** y viceversa, las veces que quieras.

Funciona igual en celular y en computadora. En celular, las tarjetas se acomodan en una sola columna.

---

## Parte 1: Vista "Soy productor"

Pensada para revisarse en el celular, en el campo, en un vistazo. Todo lo que ves aquí ya pasó (o está por pasar) por la revisión del técnico.

### 1. Mi lote

Tarjeta plegable (toca "Cambiar" para abrirla). Aquí defines los datos de tu parcela:

| Campo | Qué preguntar | Qué hace |
|---|---|---|
| ¿Cuándo trasplantaste? | Fecha de trasplante | Marca el día 1 del ciclo; todo se calcula a partir de ahí |
| ¿Dónde siembras? | Campo abierto o Invernadero | En invernadero no entra la lluvia al cultivo y baja la demanda de agua |
| ¿Cómo es tu suelo? | Arenoso, Franco o Arcilloso | Cambia cuánta agua puede guardar tu suelo (arenoso guarda menos, arcilloso guarda más) |
| ¿Cómo riegas? | Goteo, Aspersión o Surco | Cambia la eficiencia de riego usada en los cálculos |
| ¿Cada cuántos días riegas normalmente? | Número de días | Es tu calendario actual; sirve de comparación para calcular el ahorro |
| ¿Cuánta agua echas cada vez? | Litros por m² | Lo mismo: parte de tu calendario actual |
| ¿Cuánto te cuesta el agua? | $ por m³ (opcional) | Si lo llenas, la sección de ahorro te dice cuánto dinero te ahorras |
| Clima para esta demostración | Ciclo normal / seco y caluroso / lluvioso y fresco | Cambia el ejemplo de clima que usa toda la pantalla |

**Importante:** "litros por m²" es lo mismo que "milímetros de riego". 1 litro por m² = 10 m³ de agua por hectárea.

### 2. Navegar los días del ciclo

Debajo de "Mi lote" hay una barra con:

- Botones **Antes** / **Después** para moverte un día a la vez.
- Una barra deslizable para saltar a cualquier día del ciclo completo (normalmente entre 130 y 145 días, desde el trasplante hasta la cosecha).
- La fecha y la etapa del cultivo (Recién trasplantado, Creciendo, Floración y frutos, Maduración y cosecha) se actualizan solas.

### 3. ¿Hoy toca regar?

Es la tarjeta principal, la respuesta corta:

- **"Sí, hoy toca regar"** (fondo azul-verdoso): muestra cuántos litros por m² aplicar, su equivalente en m³ por hectárea y en "pipas" de 10,000 litros, para que te des una idea del tamaño.
- **"Hoy no riegues"** (fondo claro): te dice en cuántos días sería el próximo riego, con fecha incluida.

Debajo siempre aparece:

- **Agua en el suelo:** una barra de color que va de "Falta agua" (rojo) a "Bien" (verde), con el porcentaje actual.
- Un aviso de lluvia si llovió ese día y el cultivo está a cielo abierto.
- Un estado de validación:
  - **"Falta que tu técnico la confirme"** (ámbar): todavía nadie revisó la recomendación de ese día.
  - **"Confirmada por tu técnico"** (verde): el técnico ya la validó, puedes seguirla.
  - **"Tu técnico la cambió: pregúntale qué hacer"** (rojo): el técnico rechazó la recomendación automática; no la sigas sin hablar con él o ella primero.

### 4. Plagas y enfermedades

Un aviso para saber cuándo revisar el cultivo, **no un diagnóstico**. Muestra:

- Un resumen general ("Todo tranquilo", "Riesgo medio" o "Cuidado: riesgo alto de...").
- Una tarjeta por cada plaga vigilada (tizón tardío, mosquita blanca, palomilla del tomate) con su nivel (Bajo / Medio / Alto) y un texto explicando qué es y qué buscar en la planta si tocas "Qué revisar en tus plantas".
- Si el nivel es alto, el mensaje siempre termina en: avisa a tu técnico antes de aplicar cualquier producto.

### 5. Los próximos 7 días

Una fila de botones, uno por día, con tres posibles iconos: gota de agua (toca regar ese día), lluvia (se espera lluvia) y un signo de alerta (riesgo alto de plagas). Toca cualquier día para saltar directo a él.

### 6. ¿Cuánta agua te ahorras?

Compara, en todo el ciclo:

- Lo que gastarías con tu calendario actual (el que llenaste en "Mi lote").
- Lo que gastarías siguiendo la recomendación del simulador.

Te dice el ahorro en m³ por hectárea, en porcentaje, en "pipas" y, si llenaste el costo del agua, también en pesos. Si tu calendario ya es eficiente, el mensaje lo dice igual ("gastan casi lo mismo").

### 7. Mi riego de hoy

Aquí anotas cuánto regaste realmente ese día (en litros por m²) y presionas **Guardar**. Esta nota la ve tu técnico en su bitácora. Si no regaste, deja el número en 0.

> La demostración no guarda nada al cerrar la página. Cada vez que la abras, empieza de cero.

### 8. ¿Cómo leo estos números?

Un acordeón al final de la pantalla con las mismas explicaciones de arriba, para consultarlo rápido sin tener que preguntar.

---

## Parte 2: Vista "Soy técnico"

Pensada para computadora o tablet, con más detalle y controles. Aquí se cargan los datos reales, se comparan estrategias de riego y se valida (o rechaza) la recomendación antes de que el productor la vea confirmada.

### Panel izquierdo: Ciclo de cultivo

| Control | Para qué sirve |
|---|---|
| **Clima del ciclo** | Igual que en la vista productor: tres climas de ejemplo o "Mi CSV de clima" |
| **CSV de clima** (si eliges esa opción) | Pega el texto del CSV o súbelo con el botón de archivo, y presiona "Usar este CSV". Formato: una fila por día, con columnas `fecha` (aaaa-mm-dd o dd/mm/aaaa), `tmax` y `tmin` en °C, `lluvia` en mm y, opcional, `hr` (humedad relativa en %). Acepta coma, punto y coma o tabulador como separador |
| **Humedad medida (opcional)** | Si tienes un sensor o tensiómetro, anota aquí el % de agua disponible que midió ese día y presiona "Guardar medición". El modelo corrige su estimación con ese dato para ese día en adelante |
| **Modo de riego** | Goteo (riegos pequeños y frecuentes) o Balance hídrico (riegos grandes y espaciados) — define qué estrategia usa la vista "Validar recomendación" y el resumen del ciclo |
| **Fecha de trasplante** | El día 1 del ciclo |
| **Sistema de producción** | Campo abierto o Invernadero |
| **Agua disponible en el suelo (mm)** | Es la TAW: cuánta agua puede guardar el suelo en la zona de raíces. Se llena sola según el suelo elegido en la vista productor, pero puedes ajustarla a mano |
| **Eficiencia de riego (%)** | Qué porcentaje del agua que bombeas realmente llega a la planta (goteo ~85%, aspersión ~75%, surco ~60%, como referencia) |
| **Calendario del productor** | "Cada (días)" y "Lámina (mm)": el supuesto de riego actual contra el que se mide el ahorro. Cámbialo por lo que el productor realmente declare |

### Panel derecho: cuatro pestañas

Usa la barra deslizable de arriba ("Día del ciclo") para moverte por las fechas; las cuatro pestañas muestran el mismo día desde distintos ángulos.

#### Pestaña "Riego"

- Una tabla que compara **cuatro estrategias**: Calendario del productor, Balance hídrico, Goteo frecuente y Riego deficitario. Para cada una ves agua bombeada (m³/ha), ahorro frente al calendario, número de riegos, días con estrés hídrico, rendimiento relativo estimado y percolación (agua que se va más allá de la raíz, o sea desperdiciada).
- Una gráfica de "Agotamiento de agua en la zona de raíces": una línea por estrategia a lo largo de todo el ciclo, con una línea punteada que marca el límite antes de que el cultivo empiece a sufrir estrés.

#### Pestaña "Plagas"

- Una gráfica con los tres índices de riesgo (tizón tardío, mosquita blanca, palomilla del tomate) de 0 a 100 a lo largo del ciclo, con bandas de color (bajo/medio/alto) y la línea de alerta.
- **Conteo de trampas del día:** anota aquí lo que de verdad se contó en campo (plantas con síntomas de tizón, individuos de mosquita por trampa, capturas de palomilla por trampa) y presiona "Guardar conteos". En cuanto haya conteos guardados, aparece una **precisión** y **cobertura** exploratorias por plaga: qué tan seguido una alerta del modelo coincidió con un conteo positivo. No reemplaza una validación fitopatológica, pero ayuda a ver si el modelo va por buen camino.
- **Alertas del ciclo:** una tabla con cada episodio de riesgo alto (de cuándo a cuándo, cuántos días, índice máximo) y la acción sugerida, que siempre es "monitorear", nunca un producto.

#### Pestaña "Validar recomendación"

Es el corazón de la supervisión humana:

- Muestra la misma recomendación que ve el productor ese día (riego y plagas), con el detalle técnico completo: demanda del cultivo (ETo × Kc), temperatura, lluvia y el valor de cada índice de plaga.
- Dos botones: **Validar recomendación** o **Rechazar**. Hasta que elijas uno, la recomendación aparece como "Pendiente" tanto aquí como en la vista productor.
- Debajo, la **bitácora**: un historial de cada día con la recomendación, el estado de plagas, tu decisión y lo que el productor anotó haber aplicado.
- Un **resumen del ciclo** con agua usada, ahorro frente al calendario, días con estrés y número de alertas emitidas — útil para explicarle el ciclo completo a alguien más en una sola mirada.

#### Pestaña "Supuestos"

La pestaña de la transparencia. Muestra:

- Una tabla de qué tan sólido es cada componente del modelo, con tres etiquetas: **Método** (técnica estándar de la literatura), **Ejemplo** (valor puesto por el equipo, no medido) o **Por confirmar** (falta validarlo localmente).
- **Parámetros editables:** todos los números que alimentan el modelo (latitud, duración de cada etapa del cultivo, coeficientes Kc, agotamiento permisible, sensibilidad al estrés Ky, umbrales de plagas, etc.), cada uno con su etiqueta y una nota explicando de dónde sale. Puedes cambiarlos aquí mismo para probar otros escenarios.
- **Qué no modela esta demo:** una lista honesta de las limitaciones (no hay salinidad, ni riego por zonas, ni pronóstico de lluvia, ni conteos reales comparados a fondo).

---

## Preguntas frecuentes

**¿Necesito internet?** Solo para que cargue la tipografía la primera vez. El cálculo funciona sin conexión.

**¿Se guardan mis datos si cierro la pestaña?** No. Esta es una demostración: cada vez que abres el archivo, empieza de cero. Para un uso real habría que agregar guardado de datos.

**¿Puedo usar mis propios datos de clima?** Sí, con un archivo CSV desde la vista técnico (ver la tabla del panel izquierdo arriba). Si no tienes uno, usa los climas de ejemplo, pero recuerda que no son mediciones reales.

**¿La app me dice qué agroquímico aplicar?** Nunca. Solo avisa cuándo conviene revisar el cultivo. La decisión de aplicar algo es siempre de una persona, no de la herramienta.

**¿Por qué el productor ve "pendiente de validación"?** Porque ninguna recomendación llega al productor como definitiva sin que un técnico la revise primero en la pestaña "Validar recomendación".

**¿Qué pasa si cambio un parámetro en "Supuestos"?** El simulador recalcula todo el ciclo al momento con el nuevo valor. Es útil para probar "¿y si el suelo guarda más agua?" o "¿y si el umbral de alerta fuera más alto?", pero no cambia que los parámetros de referencia (FAO-56, en su mayoría) sigan pendientes de calibrarse con datos de Morelos — ver `fuentes.md`.

## Glosario rápido

| Término | Qué significa |
|---|---|
| **ETo** | Evapotranspiración de referencia: cuánta agua pierde un pasto de referencia por día, según el clima |
| **ETc** | Demanda de agua del cultivo: ETo multiplicada por el Kc de la etapa actual |
| **Kc** | Coeficiente de cultivo: qué tanta más o menos agua necesita el jitomate frente al pasto de referencia, según la etapa |
| **TAW** | Agua total disponible en el suelo para las raíces (mm) |
| **RAW** | Agua fácilmente disponible: la parte del TAW que se puede usar antes de que el cultivo empiece a sufrir estrés |
| **Agotamiento (Dr)** | Cuánta agua le falta al suelo en ese momento, comparado con estar lleno |
| **p** | Fracción de agotamiento permisible: qué tanto se deja secar el suelo antes de que se considere que ya urge regar |
| **Ky** | Qué tan sensible es el rendimiento del cultivo al estrés por falta de agua |
| **Percolación** | Agua que se va más allá de donde llegan las raíces; agua desperdiciada |
| **Rendimiento relativo** | Una estimación de cosecha comparada entre estrategias, no una predicción de toneladas reales |
| **Lámina (mm)** | Otra forma de decir litros por m²; 1 mm = 1 litro por m² = 10 m³ por hectárea |

---

## Nota sobre `index.html`

`index.html` tiene exactamente el mismo contenido que `simulador-v3.html`: es la copia que GitHub Pages sirve en la URL pública del repositorio (https://gleipm.github.io/HackatonInsustria5/), para que el enlace raíz muestre el MVP completo sin tener que apuntar a un archivo específico. Puedes usar cualquiera de los dos indistintamente.
