---
tipo: reporte-bimestral-buap
fecha: 2026-10-09
exportado: 2026-10-14
practicante: Rafael Hernández Muñoz
periodo: septiembre – octubre 2026 (corte 9-oct)
fuente: https://claude.ai/artifact/UEcSEQzssRk6ajnzibQvDD
privado: true
tags:
  - pp-invierno26
  - reporte
---
# Reporte bimestral 2 — Prácticas Profesionales (septiembre–octubre 2026)

> [!note] Copia del doc publicado el 2026-10-09 en Claude ([original](https://claude.ai/artifact/UEcSEQzssRk6ajnzibQvDD)), exportada al vault el 2026-10-14.
> Se guarda tal cual se entregó. Lo que cambió después está en [[Contexto PP - plan vs real (2026-10-14)]].

`2026-10-09` · Raph Hernández

## Datos generales

| Campo | Dato |
| --- | --- |
| Practicante | Rafael Hernández Muñoz |
| Licenciatura | Física, FCFM-BUAP |
| Matrícula | [por completar] |
| Unidad receptora | Oficina de fianzas A3, Puebla |
| Área | Análisis cuantitativo y automatización de procesos |
| Responsable en la unidad receptora | [por completar] |
| Periodo que cubre | Septiembre – octubre de 2026 (corte al 9 de octubre) |
| Horas acumuladas en el periodo | [por completar] |

## Resumen de actividades

En este bimestre cerré el análisis de mercado (17 de septiembre), evalué opciones de CRM para la oficina y definí el alcance de una herramienta propia de extracción de datos de contratos, cuya versión 2 inicié el 29 de septiembre.

El trabajo se movió del análisis de datos hacia la automatización de procesos internos. La evaluación de ClickUp mostró que antes de elegir una herramienta había que mapear el flujo operativo real; ese mapeo orientó también el diseño de la herramienta.

Al corte del 9 de octubre, la herramienta tiene definidos sus módulos, su forma de instalación y distribución, y su integración con la estructura de carpetas de Google Drive que ya usa la oficina.

## Actividades desarrolladas

### 1. Cierre del análisis de mercado (Track A)

- Revisé la versión final del cruce de bases del practicante, la comparé con mi pipeline y documenté qué tabla era la válida y qué faltaba corregir.
- Cerré el track dentro del programa el 17 de septiembre, con la integración de sus prospectos en una tabla maestra.

### 2. Evaluación de CRM (Track B)

- Probé ClickUp como CRM con el practicante: qué información se puede cargar, cómo representar el flujo de la oficina y qué limitaciones tiene.
- Al ver que la prueba se reducía a cargar datos, replanteé el enfoque: primero mapear el flujo operativo real (elementos, variables y dependencias) y usarlo como criterio para evaluar CRMs comerciales.
- Coordiné el llenado de una matriz cuantitativa de evaluación de CRM para ClickUp.
- Comparé rentar un CRM (ClickUp o de código abierto) contra desarrollar uno propio, manteniendo Google Drive como almacén de archivos.

### 3. Herramienta de extracción de datos de contratos

- Analicé un prototipo previo hecho en Google AI Studio: automatizaba la extracción pero no dejaba espacio para la revisión humana.
- Definí el alcance en tres módulos: (1) extracción de datos con vista previa del PDF y sugerencias de IA que la ejecutiva acepta o corrige; (2) edición de PDF (dividir, unir, renombrar, insertar firmas); (3) generación de previos a partir de plantillas por tipo de fianza y beneficiario.
- Inicié la versión 2 el 29 de septiembre, conservando del prototipo la segmentación de contratos para optimizar el uso de tokens.
- Dejé el conector de IA compatible con Anthropic y con APIs tipo OpenAI, y decidí instalar la herramienta en la laptop de cada ejecutiva, distribuida desde un repositorio de GitHub.
- Diseñé la integración con Google Drive siguiendo la convención de la oficina (agente › fiado › contrato), con un Excel general de solo lectura con hojas de contratos, fianzas, pólizas de RC, fiados y documentos del expediente.
- El 7 de octubre definí un segundo módulo de Altas: explorar los documentos de alta de un fiado, extraer sus datos a partir de la constancia de situación fiscal y controlar vigencias.
- Mantengo una bitácora de desarrollo con los cambios realizados y los errores encontrados y corregidos.

### 4. Coordinación del programa

- Continué la supervisión del practicante con bitácoras de sesión y verificaciones semanales.
- Retomé los temas pendientes de la fase de operación antes de pasar a los tracks siguientes.

## Resultados, decisiones y productos

La referencia para medir el beneficio de la herramienta es el tiempo actual de revisión manual: unos 5 minutos por contrato para una ejecutiva.

| Fecha | Resultado o decisión |
| --- | --- |
| 8 oct 2026 | Diseño del registro general en Excel a partir de las fichas guardadas en Drive |
| 7 oct 2026 | Definición del módulo de Altas como segunda función principal |
| Octubre 2026 | Repositorio de GitHub como canal de distribución e instalación |
| 29 sep 2026 | Inicio de la versión 2; primera entrega = módulo de extracción; instalación local por ejecutiva |
| Finales sep 2026 | Alcance de la herramienta en tres módulos y preferencia por rentar una API de IA empresarial sobre comprar hardware |
| Septiembre 2026 | Matriz cuantitativa de evaluación de CRM (ClickUp) y decisión de mapear primero el flujo operativo |
| 17 sep 2026 | Cierre del Track A dentro del programa |

## Aprendizajes y competencias

- **Evaluar herramientas por valor, no por funciones:** una plataforma con muchas opciones puede desviar la prueba; el criterio debe salir del proceso real de la oficina.
- **Diseño centrado en el usuario:** la IA sugiere y la ejecutiva valida; la revisión humana es parte del flujo, no un paso opcional.
- **Confidencialidad y costos:** comparar modelos locales, APIs empresariales y hardware propio según privacidad de la información y costo.
- **Ingeniería de software:** control de versiones, distribución por repositorio y bitácora de cambios y errores.
- **Modelado de información:** definir llaves (RFC del fiado, número de contrato) y una estructura de carpetas y hojas que pueda conectarse después con un CRM.

## Dificultades y cómo se atendieron

| Dificultad | Atención |
| --- | --- |
| La prueba de ClickUp se convirtió en carga de datos sin objetivo claro | Se regresó al inicio del track para mapear el flujo y evaluar con una matriz |
| El prototipo de AI Studio no permitía revisión humana y dependía de un proveedor | Nueva versión con validación de la ejecutiva y conector de IA intercambiable |
| Riesgo de compartir datos de clientes con terceros | Evaluación de modelos locales frente a APIs empresariales con condiciones de privacidad |
| Compatibilidad con un CRM que aún no se elige | Registro en Drive y Excel con llaves estables, fácil de migrar después |

## Pendientes y plan de cierre

1. Terminar y entregar el módulo de extracción para pruebas con las ejecutivas.
2. Desarrollar el módulo de Altas y el registro general en Excel.
3. Decidir entre rentar o desarrollar el CRM y cómo conectarlo con la herramienta.
4. Elegir el nombre definitivo de la herramienta.
5. Llevar el programa de prácticas a su cierre el 18 de diciembre.
