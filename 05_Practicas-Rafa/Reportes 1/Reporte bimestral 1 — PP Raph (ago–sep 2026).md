---
tipo: reporte-bimestral-buap
fecha: 2026-10-09
exportado: 2026-10-14
practicante: Rafael Hernández Muñoz
periodo: agosto – septiembre 2026
fuente: https://claude.ai/artifact/NBLRoAEzUT3yr5NMSLxYec
privado: true
tags:
  - pp-invierno26
  - reporte
---
# Reporte bimestral 1 — Prácticas Profesionales (agosto–septiembre 2026)

> [!note] Copia del doc publicado el 2026-10-09 en Claude ([original](https://claude.ai/artifact/NBLRoAEzUT3yr5NMSLxYec)), exportada al vault el 2026-10-14.
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
| Periodo que cubre | Agosto – septiembre de 2026 |
| Horas acumuladas en el periodo | [por completar] |

## Resumen de actividades

En este bimestre puse en marcha el programa de prácticas de la oficina el 17 de agosto, coordiné la incorporación de un practicante de Física y desarrollé el análisis de mercado de fianzas para Puebla (Track A), que se dio por cerrado el 17 de septiembre.

El trabajo se dividió en tres frentes: operación de la oficina (emisión de previos y carga de expedientes en los sistemas de las afianzadoras), análisis de datos públicos para identificar contratistas de obra pública con potencial de afianzamiento, y la organización del registro de trabajo del programa (bitácoras, control de versiones y método de evaluación).

El resultado principal fue una base depurada de 546 contratistas del padrón estatal, vinculada con el directorio de INEGI y con los contratos públicos 2025–2026, junto con una regla para estimar las fianzas que cada contrato requiere.

## Actividades desarrolladas

### 1. Arranque y coordinación del programa de prácticas

- Definí el cronograma agosto–diciembre: tres sesiones por semana de 4.5 h (lunes, miércoles y jueves), con fases de inducción (semanas 1–2), operación (semanas 3–8) y proyectos (semanas 9–17).
- Reprogramé el cierre a diciembre al recalcular las horas necesarias para cumplir la meta de 250 h con 13.5 h semanales y los días inhábiles.
- Diseñé un método de seguimiento con bitácora diaria y semanal, un semáforo de dominio (expuesto, reconoce, produce, explica) y verificaciones orales a libro cerrado.
- Aplicé la evaluación de cierre de la fase de inducción el 27 de agosto, mediante un mini-test de preguntas abiertas.

### 2. Operación de fianzas

- Acompañé la emisión de previos y la carga de expedientes y estados financieros en los sistemas de cuatro afianzadoras (MAPFRE, AVLA, Berkley y Tokio).
- Preparé sesiones de caso completo (un contrato con todos sus documentos) para cubrir cancelaciones, bases de cálculo y contragarantías.

### 3. Análisis de mercado (Track A)

- Integré y limpié las fuentes públicas: padrón de contratistas del estado (2025 y 2026), DENUE de INEGI para el sector construcción, contratos de obra municipal, Compras MX 2026 y el histórico de CompraNet 2010–2023.
- Programé en Python un cruce difuso padrón × DENUE con normalización de texto, reparación de codificación, similitud de nombres y un puntaje de confianza basado en evidencias (correo, teléfono, código postal, colonia).
- Definí una regla para estimar las fianzas implícitas de cada contrato (licitación, anticipo, cumplimiento y vicios ocultos) y la prima asociada.
- Geolocalicé obras municipales de la ciudad de Puebla ajustando la retícula de calles numeradas con regresión de Theil–Sen, y construí un mapa de cercanía entre obras y contratistas.
- Revisé el entregable del practicante en este track y le di retroalimentación sobre la verificación de resultados.

### 4. Infraestructura de trabajo

- Organicé el registro del programa en un vault de Obsidian con plantillas automatizadas de bitácora.
- Configuré dos repositorios Git (uno privado y uno compartido con el practicante) y establecí reglas de sincronización para evitar conflictos.

## Resultados y productos

El cruce de bases pasó de 59 coincidencias con 11 falsos positivos en su primera versión a 108 coincidencias de confianza alta o media sobre 546 contratistas únicos (20 %).

| Producto | Descripción | Fecha |
| --- | --- | --- |
| Cronograma del programa | Plan de fases y horas agosto–diciembre, con cálculo de reposiciones | Agosto 2026 |
| Método de seguimiento y plantillas | Bitácora diaria y semanal, semáforo de dominio, evaluación de fase | 26 ago 2026 |
| Pipeline padrón × DENUE v2 | Script y notebook reproducibles en Python, con niveles de confianza A/B/C | 10 sep 2026 |
| Script de fianza implícita v2 | Estimación de fianzas y prima por contrato, geolocalización de obras y mapa | 11 sep 2026 |
| Base de prospectos depurada | Contratistas con RFC, teléfono y correo, segmentados por actividad en obra pública | Septiembre 2026 |
| Documentación del Track A | Notas técnicas del método, decisiones y hallazgos | Septiembre 2026 |

Otros hallazgos del análisis: 211 contratistas aparecen en ambos padrones y 318 solo en el de 2025 (renovación pendiente); 53 de las 59 empresas con obra municipal están en el padrón; y 25 contratistas concentran el 80 % de la prima estimada.

## Aprendizajes y competencias

- **Manejo de datos reales:** limpiar bases públicas con errores de codificación y campos incompletos, y vincular registros sin una llave común.
- **Rigor en la verificación:** medir tasas de coincidencia y revisar falsos positivos antes de usar un resultado para decisiones comerciales.
- **Modelado aplicado:** traducir una regla de negocio (porcentajes de fianza sobre el monto del contrato) a parámetros de un script.
- **Coordinación y enseñanza:** comprobé que una explicación rápida y abstracta no genera comprensión; funciona mejor un caso concreto con pasos numerados y el esquema “primero observa, luego lo hace acompañado”.
- **Conocimiento del sector:** tipos de fianza en obra pública, operación con afianzadoras y fuentes de contratación gubernamental.

## Dificultades y cómo se atendieron

| Dificultad | Atención |
| --- | --- |
| Horario del practicante menor al previsto (13.5 h/semana en lugar de ~20) | Se recalculó el cronograma y se movió el cierre al 18 de diciembre |
| Choque del viernes con clases del practicante | Las sesiones del viernes pasaron al jueves desde la semana 1 |
| Sin evidencia de comprensión en las primeras sesiones | Se exigió un entregable por sesión y verificaciones orales a libro cerrado |
| Encargo del Track A demasiado abstracto | Se reformuló como un caso trazable: seguir una obra pública anunciada hasta su contrato y empresa ganadora |
| Bases con errores de codificación y archivos de cientos de MB | Funciones de reparación de texto y procesamiento por bloques |
| Conflictos al sincronizar los repositorios compartidos | Regla de actualizar antes de trabajar y antes de subir cambios, y exclusión de archivos de configuración |

## Plan para el siguiente bimestre

1. Mapear el flujo operativo real de la oficina y usarlo como base para evaluar herramientas de CRM (Track B).
2. Evaluar ClickUp con una matriz cuantitativa de criterios.
3. Iniciar el desarrollo de una herramienta para extraer datos de los contratos y apoyar la redacción de los textos de fianza.
4. Consolidar la fase de operación del practicante y avanzar hacia los siguientes tracks del programa.
