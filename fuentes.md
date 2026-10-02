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
| Duraciones 30/40/40/25 días, total 135 | [V] ejemplo FAO para clima árido; [P] para Morelos y variedad | FAO-56 (1998), Tabla 11, fila Tomato, clima árido, página/tabla digital "TABLE 11": https://www.fao.org/4/x0490e/x0490e0b.htm | La tabla oficial muestra 30 inicial, 40 desarrollo, 40 media, 25 final y total 135. FAO indica que son longitudes generales y deben sustituirse por observaciones locales. |
| Agotamiento permisible p = 0.40 | [V] como valor de arranque del ejemplo; [P] para tomate/localidad | FAO-56 (1998), capítulo 8, secciones "Soil water availability", TAW y RAW: https://www.fao.org/4/x0490e/x0490e0e.htm | FAO define RAW = p x TAW y señala que p depende de cultivo, clima, suelo y manejo. No se encontró una tabla oficial que valide 0.40 específicamente para este lote; v3 lo etiqueta como por confirmar. |
| Ky = 1.05 | [P] | FAO-56, capítulo 8 y relación rendimiento-agua; https://www.fao.org/4/x0490e/x0490e0e.htm | El número 1.05 proviene del prototipo y no quedó localizado en una tabla verificable para jitomate Morelos durante esta revisión. Se mantiene como parámetro editable y no como resultado productivo. |
| INIFAP para Kc, etapas, p y Ky locales | [P] | Portal institucional INIFAP: https://www.gob.mx/inifap | No se localizó en la carpeta ni se pudo abrir aquí una ficha técnica específica de jitomate Morelos que sustituya FAO-56. Antes del pitch, un técnico debe aportar publicación, tabla y página INIFAP si existe. |
| Latitud 18.8 N para radiación | [S] | Punto aproximado de la zona Cuautla-Ayala-Yautepec; no se descargó una ficha geográfica oficial | Valor de demostración editable. No debe confundirse con coordenada exacta de parcela. |
| Clima de tres escenarios | [S] | Generado dentro de `simulador-v3.html` | Se revisó el código: los escenarios son sintéticos, no observaciones. La pantalla los marca como ejemplo. |
| CSV de clima | [V] formato del MVP; [P] calidad del dato | Instrucciones del propio `simulador-v3.html`; fuente meteorológica oficial pendiente SMN/CONAGUA | El CSV exige fecha, tmax, tmin y lluvia; `hr` es opcional. Se puede cargar sin servidor. |
| Calendario 14 mm cada 3 días | [S] | Supuesto declarado por el equipo en el prototipo | Es la línea base editable; cualquier ahorro depende de este supuesto. |
| Eficiencia de goteo 85% | [S] | Valor de ejemplo del prototipo | No se presentó una medición de parcela; debe medirse con caudal, presión y uniformidad. |
| Sensor de humedad | [S] dato capturado manualmente en v3 | No hay sensor físico conectado | La pantalla acepta porcentaje de agua disponible y lo marca como medición capturada; si se escribe un dato simulado debe etiquetarse como ejemplo. |
| Índices de tizón tardío, mosquita blanca y palomilla | [S] | Reglas heurísticas del prototipo | No sustituyen diagnóstico ni conteo. Solo disparan monitoreo; no recomiendan agroquímicos. |
| Precisión y cobertura de alertas | [P] hasta capturar conteos | Conteos manuales de trampas en v3 | Son métricas exploratorias: positivo = conteo mayor que cero; alerta = índice >= umbral. Requieren diseño de muestreo y validación fitopatológica. |
| Agua, ahorro, estrés y alertas del resumen | [S]/[P] | Calculados por el modelo v3 | Son resultados de ejemplo dependientes de clima, suelo, parámetros y línea base; no son impactos medidos. |

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
