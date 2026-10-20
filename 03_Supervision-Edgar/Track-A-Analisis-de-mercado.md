---
tipo: track
track: A
estado: cerrado
fechas: 2026-08-27 → 2026-09-17
corte: 2026-10-20
fuente: reporte de supervisión del 2026-10-09, revisión S4 y revisión de corte S5 del Track A, cierre del Track A (2026-09-18), reporte bimestral 1
---

# Track A · Análisis de mercado (cerrado)

## Pregunta

¿Dónde están en Puebla los contratistas de obra pública que van a necesitar fianzas y que todavía no son clientes? ¿Cuándo se concentra esa demanda y cuánto vale en prima?

## Fuentes públicas que se usaron

- Padrón de contratistas del estado (2025 y 2026).
- DENUE de INEGI, sector construcción.
- Contratos de obra municipal.
- Compras MX.
- Histórico de CompraNet.
- ENEC de INEGI, para la estacionalidad.

## Cómo avanzó

| Momento              | Qué pasó                                                                                                                                                  |
| :------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 27-ago (S2)          | Primer encargo: inventario de fuentes públicas. No entregó nada: el encargo fue abstracto.                                                                |
| 2-sep (S3)           | El encargo se rehace como caso concreto: seguir una obra anunciada hasta el contrato y la empresa ganadora en Compras MX.                                 |
| S3–S4                | Encuentra y limpia el padrón 2026, baja DENUE, ENEC, Compras MX y CompraNet, y arma el primer cruce.                                                      |
| 10-sep (revisión S4) | El cruce tenía 19 % de coincidencias falsas, el padrón 2025 se perdía sin aviso y la documentación no medía lo que afirmaba. Se le dieron 6 correcciones. |
| 13-sep               | Baja el ruido de 18 % a **3 %** con un filtro contra nombres genéricos que pensó él. Se le pide tablero de Power BI para visualización del trabajo.       |
| 17-sep               | Cierre del track con el tablero y las respuestas de negocio.                                                                                              |
| 18-sep               | Cuatro bitácoras técnicas, DENUE ampliado a 3 años y el hallazgo del archivo de enero (ver abajo).                                                        |

## Resultados

| Producto | Detalle |
| :-- | :-- |
| Cruce padrón × DENUE | Python (Google Colab), con similitud de nombres (umbral 95) y respaldo por correo y teléfono |
| Contratistas vinculados | 136. De ellos, 108 coinciden con mi pipeline de referencia |
| Tablero en Power BI | 10 visuales con filtros y tabla de contacto |
| Respuestas de negocio | Dónde están los prospectos, qué variables anticipan la necesidad de fianza, en qué meses se concentra la demanda y cuánto vale en prima |
| Hallazgo | Las listas mensuales de renovación del padrón anticipan quién va a participar en licitaciones |

**El hallazgo más importante:** los archivos mensuales de obra pública no son obra nueva. Son cortes acumulados de las mismas obras, y el archivo de enero pertenece al ejercicio fiscal anterior. Lo comprobó siguiendo un mismo contrato de un mes a otro. Ese error estaba en mi análisis y él lo encontró.

## Semáforo al cierre

| Capacidad | Nivel |
| :-- | :--: |
| Auditar fuentes ajenas | 🔵 |
| Limpieza de una base | 🟢 |
| Documentación de método | 🟢 (falta fechar y versionar) |
| Visualización (Power BI) | 🟢 |
| Vincular bases por llaves | 🟡 alto |
| Verificar su propio resultado | 🔴 |

## Lo que quedó pendiente

- El tablero apunta a la tabla descartada. Hay que reapuntarlo a la versión válida.
- La reconciliación aisló 28 RFC de diferencia, pero no tiene columna de veredicto.

## Mi parte en el track

Pipeline de referencia en Python con estos resultados:

- 546 contratistas únicos del padrón.
- 108 coincidencias de confianza alta o media (20 %).
- Una regla para estimar las fianzas que pide cada contrato (licitación, anticipo, cumplimiento y vicios ocultos) y su prima.
- Geolocalización de obras municipales y mapa de cercanía entre obras y contratistas.

Las cifras de cartera municipal que salían del archivo de enero se corrigieron con el hallazgo del practicante.
