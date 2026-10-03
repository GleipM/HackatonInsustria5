# Fuentes y estado de los datos

Criterio: `[V]` significa que la fuente oficial o académica respalda la cifra o el método; `[S]` es un valor de ejemplo del MVP; `[P]` requiere validación local o no pudo comprobarse en este entorno. Las cifras del simulador nunca deben presentarse como medición del valle.

| Dato o parámetro | Estado | Fuente, año y ubicación | Cómo se revisó |
|---|---|---|---|
| 1,397 ha de jitomate en Morelos | [V] reportado por el equipo; [P] verificación directa en esta sesión | INEGI, Censo Agropecuario 2022, ficha estatal Morelos: https://inegi.org.mx/contenidos/programas/ca/2022/doc/ca2022_rdMOR.pdf | El PDF oficial no pudo extraerse en el lector web de este entorno; se conserva la cifra proporcionada y queda pendiente revisar la tabla exacta del PDF. |
| 67,618 t de jitomate en Morelos | [V] reportado por el equipo; [P] verificación directa en esta sesión | INEGI, Censo Agropecuario 2022, ficha estatal Morelos: https://inegi.org.mx/contenidos/programas/ca/2022/doc/ca2022_rdMOR.pdf | Misma limitación de extracción del PDF. No se presenta como cálculo propio. |
| 40,380 t y 59.7% en agricultura protegida | [V] reportado por el equipo; [P] verificación directa en esta sesión | INEGI, Censo Agropecuario 2022, ficha estatal Morelos: https://inegi.org.mx/contenidos/programas/ca/2022/doc/ca2022_rdMOR.pdf | El porcentaje coincide aritméticamente con 40,380 / 67,618 = 59.7%, pero la tabla de origen debe confirmarse en el PDF. |
| 2,410 ha y 201,721 t atribuidas a SIAP 2023 | [P] | Portal oficial de Datos Abiertos Agrícolas SIAP: https://nube.agricultura.gob.mx/datosAbiertos/Agricola.php | El portal respondió con desafío anti-bot. No fue posible descargar el archivo ni filtrar Morelos, jitomate, año 2023, modalidad y variable. No se afirma que las cifras sean comparables. |
| Diferencia INEGI vs SIAP | [P] | SIAP Datos Abiertos, SIACON y metodología: https://www.gob.mx/agricultura/dgsiap/documentos/siacon-ng-161430 ; https://www.gob.mx/agricultura/dgsiap/documentos/notas-metodologicas-de-los-reportes-indicadores-del-sector-primario?state=published | Hipótesis a comprobar, no conclusión: pueden diferir el año/ciclo, unidad estadística, superficie sembrada vs cosechada, modalidad, agricultura protegida y cobertura censal/administrativa. Reconciliar solo después de descargar, filtrar y comparar definiciones. |
| ETo con Hargreaves-Samani | [V] como método; [P] calibración local | FAO-56 (1998), capítulo 4 y sección de alternativa con datos faltantes: https://www.fao.org/4/x0490e/x0490e08.htm | Se verificó que FAO-56 documenta procedimientos de ETo y datos faltantes. El MVP usa temperaturas sintéticas si no se carga CSV. |
| ETc = ETo x Kc | [V] como método | FAO-56 (1998), capítulo 6, ecuación 58: https://www.fao.org/4/x0490e/x0490e0b.htm | La página oficial muestra explícitamente la ecuación y el procedimiento de curva Kc. |
| Kc inicial 0.60, medio 1.15, final 0.70-0.90 para tomate | [V] valor de referencia FAO; [P] ajuste local | FAO-56 (1998), Tabla 12, tomate, sección "Tabulated Kc values": https://www.fao.org/4/x0490e/x0490e0b.htm | La tabla oficial muestra tomate en Solanaceae con 0.60, 1.15 y 0.70-0.90. En v3 se usa Kc final 0.80 como punto medio explícito de ejemplo, no como validación local. |
| Duraciones 30/40/40/25 días, total 135 | [V] ejemplo FAO para clima árido; [P] para Morelos y variedad | FAO-56 (1998), Tabla 11, fila Tomato (siembra de enero, clima árido), página/tabla digital "TABLE 11": https://www.fao.org/4/x0490e/x0490e0b.htm | Verificado de nuevo leyendo la página oficial directamente: 30 inicial, 40 desarrollo, **40** media, **25** final, total 135. Esta revisión encontró que el código de `index.html` tenía 45/30 (total 145) en vez de 40/25 — no coincidía ni con esta misma tabla de fuentes.md ni con el texto que la app ya mostraba en "Supuestos". Se corrigió el código para que coincida con la tabla oficial. |
| Agotamiento permisible p = 0.40 | [V] para tomate según FAO-56 | FAO-56 (1998), capítulo 8, Tabla 22 (profundidad radicular y fracción de agotamiento por cultivo): https://www.fao.org/4/x0490e/x0490e0e.htm | Verificado leyendo la página oficial: la Tabla 22 sí lista tomate con profundidad radicular 0.7-1.5 m y **p = 0.40** explícitamente (la revisión anterior no la había encontrado). FAO aclara que ese valor es para ETc ≈ 5 mm/día y da una fórmula de ajuste (p = p_tabla + 0.04×(5−ETc)); v3 usa 0.40 fijo y no aplica ese ajuste, lo cual sigue siendo una simplificación declarada. |
| Ky = 1.05 | [V] por fuentes secundarias convergentes; tabla primaria no verificada directamente | FAO Irrigation and Drainage Paper 33, Doorenbos & Kassam (1979), "Yield response to water" | La tabla original de FAO 33 no se pudo extraer en este entorno (el PDF no se deja leer como texto). Dos fuentes académicas independientes que citan esa tabla (un estudio de tomate en Afaka, Nigeria, y un artículo sobre validación de CROPWAT para tomate) coinciden en Ky = 1.05 para el ciclo completo. Se sube de [P] a [V] por esa convergencia, pero sigue sin confirmarse contra la tabla original página por página. |
| INIFAP para Kc, etapas, p y Ky locales | [P] | Portal institucional INIFAP: https://www.gob.mx/inifap | No se localizó en la carpeta ni se pudo abrir aquí una ficha técnica específica de jitomate Morelos que sustituya FAO-56. Antes del pitch, un técnico debe aportar publicación, tabla y página INIFAP si existe. |
| Latitud 18.8 N para radiación | [S] | Punto aproximado de la zona Cuautla-Ayala-Yautepec; no se descargó una ficha geográfica oficial | Valor de demostración editable. No debe confundirse con coordenada exacta de parcela. |
| Clima de tres escenarios | [S] | Generado dentro de `index.html` | Se revisó el código: los escenarios son sintéticos, no observaciones. La pantalla los marca como ejemplo. |
| CSV de clima | [V] formato del MVP; [P] calidad del dato | Instrucciones del propio `index.html`; fuente meteorológica oficial pendiente SMN/CONAGUA | El CSV exige fecha, tmax, tmin y lluvia; `hr` es opcional. Se puede cargar sin servidor. |
| Calendario 14 mm cada 3 días | [S] | Supuesto declarado por el equipo en el prototipo | Es la línea base editable; cualquier ahorro depende de este supuesto. |
| Eficiencia de riego: goteo 85%, aspersión 75%, surco 60% | [V] aspersión y surco coinciden con el valor indicativo de FAO; [S] goteo | FAO, "Irrigation Water Management: Training Manual No. 4", Tabla 8 "Indicative values of the field application efficiency (ea)": https://www.fao.org/4/t7202e/t7202e08.htm | Verificado leyendo la página oficial: FAO da 60% para riego de superficie/surco, 75% para aspersión y 90% para goteo. Aspersión (75%) y surco (60%) coinciden exactamente. Goteo en v3 usa 85%, un valor conservador por debajo del 90% indicativo de FAO (razonable para un sistema real sin mantenimiento perfecto, pero no es el número de la tabla). No reemplaza una medición de caudal, presión y uniformidad en campo. |
| TAW por tipo de suelo: arenoso 50 mm, franco 80 mm, arcilloso 110 mm | [P] | FAO-56 (1998), capítulo 8, Tabla 19 (agua disponible total por textura de suelo): https://www.fao.org/4/x0490e/x0490e0e.htm | Se intentó verificar de nuevo esta sesión: la página de FAO-56 menciona la Tabla 19 en el texto pero su contenido numérico no se pudo extraer en este entorno (ni directamente ni por fuentes secundarias confiables). Los valores de v3 no se modificaron porque no hay una fuente verificada con la que compararlos todavía; un técnico con acceso al PDF original de FAO-56 debe confirmarlos antes del pitch. |
| Sensor de humedad | [S] dato capturado manualmente en v3 | No hay sensor físico conectado | La pantalla acepta porcentaje de agua disponible y lo marca como medición capturada; si se escribe un dato simulado debe etiquetarse como ejemplo. |
| Índices de tizón tardío, mosquita blanca y palomilla | [S] | Reglas heurísticas del prototipo | No sustituyen diagnóstico ni conteo. Solo disparan monitoreo; no recomiendan agroquímicos. |
| Precisión y cobertura de alertas | [P] hasta capturar conteos | Conteos manuales de trampas en v3 | Son métricas exploratorias: positivo = conteo mayor que cero; alerta = índice >= umbral. Requieren diseño de muestreo y validación fitopatológica. |
| Agua, ahorro, estrés y alertas del resumen | [S]/[P] | Calculados por el modelo v3 | Son resultados de ejemplo dependientes de clima, suelo, parámetros y línea base; no son impactos medidos. |

## Verificación del cálculo de riego contra fuentes oficiales (2026-10-02)

Se releyeron directamente las páginas oficiales de FAO-56 y del manual de riego de FAO (no solo se repitió lo ya escrito en este archivo). Resultado:

- **Corregido un error real**: el código usaba 45/30 días para las etapas media/final del tomate (total 145); la Tabla 11 de FAO-56 dice 40/25 (total 135), y eso ya era lo que decían tanto este archivo como el texto de "Supuestos" en la propia app. Se corrigió el código para que los tres coincidan.
- **p = 0.40 para tomate sí está en una tabla oficial** (Tabla 22 de FAO-56): se sube de `[P]` a `[V]`.
- **Ky = 1.05** se sube de `[P]` a `[V]` por convergencia de dos fuentes académicas independientes que citan FAO 33, aunque la tabla original no se pudo leer directamente en este entorno.
- **Eficiencias de riego**: aspersión (75%) y surco (60%) coinciden exactamente con la Tabla 8 del manual de riego de FAO; goteo (85%) es un valor conservador frente al 90% indicativo de FAO.
- **TAW por textura de suelo** (50/80/110 mm) sigue sin poder verificarse: la Tabla 19 de FAO-56 no se pudo extraer en este entorno ni por la página oficial ni por fuentes secundarias. Se queda `[P]`, sin inventar un número de reemplazo.
- La fórmula de Hargreaves-Samani y la curva de Kc (interpolación lineal entre etapas) ya estaban implementadas tal como las documenta FAO-56; se revisó línea por línea contra las ecuaciones 21-25 (radiación extraterrestre) y no se encontraron errores.

## Procedimiento para cerrar la discrepancia SIAP/INEGI

1. Descargar el archivo de Datos Abiertos Agrícolas del SIAP para el año o ciclo que corresponda.
2. Filtrar entidad Morelos, cultivo jitomate/tomate rojo, año 2023 y separar superficie sembrada, superficie cosechada y producción.
3. Revisar si la serie es anual, ciclo agrícola, avance o cierre; separar riego/secano y agricultura protegida si están disponibles.
4. Comparar las definiciones con el Censo Agropecuario 2022 de INEGI, que es otra operación estadística y otro periodo.
5. Guardar el archivo original, fecha de descarga y filtros; solo entonces decidir si las cifras son comparables o explicar la diferencia como periodo, metodología o cobertura.

## Fuentes no disponibles en esta revisión

El PDF de INEGI no pudo ser extraído por el lector web y el portal SIAP bloqueó la descarga con un desafío anti-bot. No se inventan páginas ni cifras para cubrir esas dos limitaciones.

### Segundo intento de verificación (misma sesión, revisión posterior)

Se intentó de nuevo por tres rutas adicionales, todas sin éxito, para no dejar la discrepancia SIAP/INEGI sin un intento más de cierre:

1. Un PDF de la Secretaría del Campo del Estado de México que replica cierres agrícolas por estado (`secampo.edomex.gob.mx/.../56Morelos2023.pdf`) se descargó, pero su contenido es un flujo comprimido que el lector de PDF de este entorno no pudo decodificar (no hay `pdftotext`/`poppler` disponible en esta máquina).
2. El mirror histórico de Datos Abiertos en `datamx.io` solo tiene un recurso de cierre agrícola 2007-2008 (dominio `sagarpa.gob.mx` ya dado de baja); no sirve para 2023 y no se usó.
3. El dominio alterno `nube.siap.gob.mx/cierreagricola/` no resuelve (DNS inexistente).

Conclusión: sigue sin ser posible, desde este entorno, descargar el archivo oficial de Datos Abiertos del SIAP para 2023. La cifra de 2,410 ha y 201,721 t atribuida a SIAP 2023 se mantiene como `[P]` pendiente; un técnico con acceso sin restricciones a `nube.agricultura.gob.mx/datosAbiertos/Agricola.php` debe descargar el archivo, filtrar Morelos/jitomate/2023 y aplicar el procedimiento de la sección anterior antes del pitch.
