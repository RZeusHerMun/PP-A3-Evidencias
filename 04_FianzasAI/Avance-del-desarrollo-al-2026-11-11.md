---
tipo: reporte-desarrollo
herramienta: FianzasAI v2
version_en_la_carpeta: 2.0.0-alpha.10
repositorio: RZeusHerMun/PDF_AI-v2 (privado)
corte: 2026-11-11
corte_anterior: 2026-10-23
fuente: docs/SEGUIMIENTO.md, BUGS.md, CAMBIOS.md, DECISIONES.md, SESIONES.md, ALCANCE.md y README.md del repositorio; laboratorio/ocr/README.md; historia de git
revision: ok
actualizado: 2026-11-11
---

# FianzasAI · avance del desarrollo al 11 de noviembre

Parte 1 de 2. Esta nota coteja lo que dicen los registros del desarrollo (seguimiento, bugs, cambios, decisiones y sesiones) y lo compara con el corte anterior de [Estado y versiones](Estado-y-versiones.md) (23-oct). La parte 2 lo cruzará con la bitácora diaria, el trabajo del practicante y las labores de oficina.

## En corto

- **Dónde está:** versión 2.0.0-alpha.10 (11-nov). En 43 días (29-sep a 11-nov) salieron 15 versiones, en 34 sesiones de trabajo documentadas.
- **Qué hace hoy que no hacía el 23-oct:** el explorador del expediente quedó cerrado (alpha.9, 5-nov); el previo ya genera el **texto de la fianza desde un modelo** y **se cierra** con número de fianza, número de autorización y el PDF de la plataforma (alpha.10); hay cotizador con tarifas que edita la oficina; y hay un laboratorio de **OCR** con resultados sobre documentos reales.
- **Pedidos de uso:** de 113 pedidos registrados desde el 27-oct, 68 están cerrados (probados y con visto bueno), 11 hechos en espera de prueba y 34 abiertos.
- **Calidad:** 49 errores corregidos y documentados, 7 problemas conocidos abiertos, 419 pruebas automáticas en verde.
- **Lo que falta para la v1 no es código:** falta que las ejecutivas la prueben en sus laptops con el Drive real y medir el "antes". Las laptops siguen en la versión instalada el 2-oct.

## 1. Cómo creció

| Indicador | Corte 23-oct | Corte 11-nov | Cambio |
| :-- | --: | --: | --: |
| Versión | alpha.8.1 publicada, alpha.9 en curso | alpha.10 | 6 versiones más (9, 9.1, 9.2, 9.3, 9.4 y 10) |
| Decisiones de diseño documentadas | 46 (D-01 a D-46) | 68 (D-01 a D-68) | +22 |
| Errores corregidos y documentados | 30 (B-001 a B-030) | 49 (B-001 a B-049) | +19 |
| Pruebas automáticas unitarias | 277 | 419 | +142 |
| Pedidos de uso con seguimiento | sin tabla | 113 (C-01 a C-113) | tabla nueva desde el 27-oct |
| Sesiones de desarrollo documentadas | 18 | 34 | +16 |

**Pruebas automáticas a lo largo del desarrollo** (de SESIONES.md): 60 el 29-sep · 100 el 6-oct · 177 el 13-oct · 277 el 23-oct · 365 el 29-oct · 393 el 5-nov · 419 el 11-nov. Además hay dos pruebas de punta a punta (previo y explorador) y 18 pruebas propias del laboratorio de OCR.

**Tamaño:** unas 22,600 líneas de código en pantalla, servidor y lógica compartida (con sus pruebas), 37 commits y 16 *pull requests* en GitHub.

**Versiones desde el corte anterior:**

| Versión | Fecha | Qué trajo |
| :-- | :-- | :-- |
| alpha.9 | 2026-11-05 | Explorador del expediente cerrado: cambiar un archivo sin perder la ficha, sumar una carpeta a un fiado que ya tiene expediente, guardar un suelto a un fiado nuevo, Alta en el formato nuevo y Registro que lee `EXPEDIENTE/`. También: texto de la fianza con modelo (27-oct), lista de afianzadoras (28-oct), cotizador y tarifas |
| alpha.9.1 | 2026-11-06 | Comprobante de domicilio válido 6 meses |
| alpha.9.2 | 2026-11-07 | La ficha del fiado junta lo que traen los documentos del expediente (se acepta con Tab); copiar la leyenda de veracidad; agregar una carpeta completa; al guardar se abre el fiado donde quedó |
| alpha.9.3 | 2026-11-09 | El texto de la fianza dice bien la versión que sigue (v2, v3…); manita para mover el PDF; actualizador que ya no se detiene sin motivo |
| alpha.9.4 | 2026-11-11 | Un PDF con texto del escáner en letras «CID» ya no se ve como escaneado |
| alpha.10 (bloque 1) | 2026-11-11 | Cerrar el previo con el PDF de la plataforma; agente y número de autorización en la ficha; guardar solo el .txt; ruta propia de los modelos; la pestaña Revisiones se pinta cuando hay avisos |

## 2. Qué se construyó, por parte

### Lógica y servidor (lo que no se ve)

| Pieza | Qué hace | Desde |
| :-- | :-- | :-- |
| Ficha del previo con evidencia | Cada dato guarda página y cita; montos en centavos, anticipo, monto con letra, varias fianzas por documento, póliza de RC | alpha.1 a alpha.5 |
| Revisiones | RFC, vigencia retroactiva, monto con letra, plazo contra fechas, beneficiario no textual, palabras indebidas | alpha.1 en adelante |
| Drive y Registro | Guarda en la estructura de la oficina (Agente › Fiado › `CTO. {número}`), nunca borra ni reemplaza; `REGISTRO FIANZASAI.xlsx` con 5 hojas que se reconstruye desde las fichas | alpha.6 y alpha.7 |
| Lector de la CSF | Con reglas, sin IA; calibrado con CSF reales sin que los datos salieran de la laptop | alpha.8 |
| Expediente del fiado | Catálogo de documentos, vigencias y días de aviso por tipo, checklist hay · falta · vence, cotejos (domicilio, acta como poderes con la INE), nombres de archivo de la oficina | alpha.9 |
| Tarifas y cotizador | `TARIFAS FIANZASAI.xlsx` en el Drive (tarifas, afianzadoras y agentes); tarifa preferencial por fiado; cotización con el monto afianzado | alpha.9 |
| Texto de la fianza | Motor que llena los modelos Word con `{{campo}}`, marca «FALTA» lo que no hay, guarda v1, v2… con el motivo de cada versión | alpha.9 (27-oct) |
| Cierre del previo | Lee el número de fianza del nombre del PDF de la plataforma, lo compara con el escrito y deja la fianza EN REVISIÓN en la ficha y en el Registro | alpha.10 |
| Actualizador | Las instalaciones se actualizan con doble clic desde GitHub; las copias de desarrollo tienen el suyo | alpha.8.1 y ajustes hasta el 9-nov |

### Pantalla (lo que usan las ejecutivas)

| Pantalla | Qué tiene hoy |
| :-- | :-- |
| Inicio | Previo, Alta, Expediente del fiado y cotización rápida |
| Previo | Contrato a la izquierda y ficha a la derecha; captura seleccionando el texto; pestaña Revisiones que se pinta; Ctrl+Z propio; guardar en Drive; ventana de Texto (modelo, recuadro editable, Word opcional, cierre del previo) |
| Alta | Alta rápida con la CSF, campos para Berkley y MAPFRE, "Para la plataforma" para copiar |
| Expediente del fiado | Tarjetas con miniatura, tipo, vigencia y datos clave; vista en grande con flechas; ficha del fiado editable; pestañas de Revisión y Notas; copiar faltantes para WhatsApp; buscador en todos los agentes |
| Detalles de uso | Montos con comas que se copian sin comas, aviso antes de salir sin guardar, panel angosto, barra y ficha que se esconden, manita para mover el PDF |

### De idea a decisión

Las 68 decisiones están en DECISIONES.md con su contexto y lo que se descartó. Las que más pesan en el rumbo:

| Decisión | Qué fijó |
| :-- | :-- |
| D-03 y D-09 | La ejecutiva captura y decide; la IA solo sugiere; nada se inventa |
| D-19 a D-21 | Se trabaja sobre el Drive y la estructura que ya usa la oficina; nunca se borra |
| D-36 | Qué es la v1 y dónde termina la herramienta y empieza el CRM |
| D-47, D-57 y D-58 | Biblioteca de modelos de texto y texto de la fianza desde la ficha |
| D-60 y D-68 | El previo se cierra en la herramienta; los demás estados de la fianza los lleva el CRM |
| D-66 y D-67 | OCR por página, sin tocar el PDF original; motor Tesseract; la INE y la cédula se capturan a mano; el OCR se adelanta |

## 3. Seguimiento de pedidos

Desde el 27-oct cada cosa que se pide en las notas del día entra a una tabla (SEGUIMIENTO.md) con qué se hizo, su estado y la revisión de quien lo pidió.

| Estado | Pedidos | % |
| :-- | --: | --: |
| Cerrados (hechos, probados y con visto bueno) | 68 | 60 % |
| Hechos, falta la prueba | 11 | 10 % |
| Abiertos | 34 | 30 % |
| **Total** | **113** | |

**Los 34 abiertos:** 22 por hacer, 4 a medias, 7 esperan un dato o una decisión y 1 es un bug confirmado (K-15).

| Grupo de abiertos | Pedidos | Ejemplos |
| :-- | --: | :-- |
| Explorador, ficha del fiado y Alta | 6 | Arrastrar documentos al expediente, notas en Revisiones, carpeta que no guarda todo (K-15) |
| Previos con plantillas (alpha.10) | 7 | Oficio de retroactividad desde la alerta, modelos por beneficiario, carta cotización en PDF, moneda en dólares |
| Vista | 6 | Ctrl+S en todos lados, miniaturas al ancho, atajos de teclado, rediseño de las fichas |
| Después | 9 | Validación SAT contra EF, calculadora de EF de Berkley, módulo de correcciones de previos, checklist de obligados solidarios |
| De la oficina | 2 | Vicios ocultos 116.05 contra 80.50; ¿316 o 312 en la BUAP?; datos de Aserta, Insurgentes y Dorama |
| Por aclarar | 4 | Preguntas que esperan respuesta |

**De dónde salieron los pedidos:** 39 de la prueba con un fiado real (nota R30.5), 43 de las notas de las sesiones D31 a D36, 29 de revisiones y cambios chicos en la conversación de desarrollo y 2 del trabajo de campo del practicante. Es decir: casi todo lo que se construyó desde el 23-oct salió de usar la herramienta con casos de la oficina.

## 4. Errores

**49 corregidos** (B-001 a B-049). Cada uno tiene síntoma, causa, corrección y la prueba que lo cubre.

| Cómo se detectó | Errores |
| :-- | --: |
| Probando con casos reales y en Windows (Rafa) | 22 |
| Trabajo de campo del practicante | 1 |
| Pruebas automáticas, calibración con documentos reales y revisión, antes de llegar a la oficina | 26 |

Por mes: 8 en septiembre, 33 en octubre y 8 en lo que va de noviembre.

**7 problemas conocidos abiertos:**

| Clave | Qué es | Estado |
| :-- | :-- | :-- |
| K-01 | Los PDF escaneados no se pueden capturar | En curso: es lo que resuelve el OCR |
| K-06 | Una CSF escaneada no se lee sola | Igual, depende del OCR |
| K-15 | Al guardar una carpeta, un documento sin datos para renombrarlo no se guarda | Reproducido el 11-nov; arreglo por aprobar |
| K-02 | Falta probar en las laptops de la oficina con casos reales | Lo probado en Windows es en la laptop de Rafa y la HP |
| K-03 | IVA fijo al 16 % | Sin fecha |
| K-05 | "Otras de crédito" sin obligaciones ni clave | Sin fecha |
| K-07 | Después de un `git pull` a mano, el actualizador no reinstala dependencias | Sin fecha |

## 5. Cómo ha impactado, por categoría

| Categoría | Qué cambió | Evidencia |
| :-- | :-- | :-- |
| **Errores de transcripción** (problema n.º 1 de la oficina) | El dato se captura una vez, con su página y cita, y de ahí salen la ficha, el Registro y el texto de la fianza. El texto ya no se vuelve a teclear | Texto con modelo (D-57), «FALTA» en rojo, revisiones automáticas |
| **Expediente del fiado** | Se sabe qué hay, qué falta y qué vence al abrir la carpeta; la lista de faltantes sale lista para mandarla | Explorador (alpha.9), 13 pedidos cerrados con la columna VERIFICADO el 6-nov |
| **No saber cuál previo es el último** | Cada texto queda como v1, v2… con su motivo; el previo cerrado guarda el PDF de la plataforma y el número de autorización | D-59, D-68 |
| **Cotización** | Cotización rápida con el tarifario de la oficina y la tarifa preferencial del fiado | D-40, D-46, C-91 |
| **Trazabilidad del desarrollo** | Cada pedido, error y decisión tiene número y se puede seguir | 113 pedidos, 49 errores, 68 decisiones |
| **Preparación para el CRM** | El Registro ya trae las llaves (RFC, número de contrato, número de fianza) y, desde la alpha.10, el estado y el número de autorización de cada fianza | ALCANCE § 3, hoja Fianzas del Registro |

De los 15 incidentes del flujo que salieron en el Track B, la herramienta ataca de frente 2 (error en captura y expediente equivocado), detecta antes 5 (documento fuente incompleto, documentación vencida, retroactividad, palabras indebidas y cambios del previo), 4 son sobre todo del CRM, 2 quedan para después de la v1 y 2 están fuera de ambos (ALCANCE § 4).

## 6. Avance contra los objetivos

### La v1 (D-36): previos con plantilla y altas probados por las ejecutivas en sus laptops

| Parte | Corte 23-oct | Corte 11-nov | Falta |
| :-- | :-- | :-- | :-- |
| Previo: captura | Funcional, probado por Rafa | Igual, más agente, afianzadora y tarifa en la ficha | Que las ejecutivas capturen 3 a 5 contratos reales con la unidad compartida |
| Previo: texto con plantilla | Sin empezar en la app | Texto con modelo, versiones con motivo y cierre del previo. La biblioteca tiene 33 modelos; 20 pasan la revisión mecánica del 12-nov | Corregir los 13 modelos que fallan y aprobar el contenido con las ejecutivas; oficio de retroactividad; modelos por beneficiario; probar el cierre con un PDF real de la plataforma |
| Altas (expediente del fiado) | Alta rápida hecha; explorador en prueba | Explorador cerrado; Alta y Registro en el formato nuevo | Que las ejecutivas hagan altas y actualizaciones reales |
| Instalación | HP lista; laptops con la alpha.4 | HP 14 actualizada; laptops igual | Versión estable y actualizar las 2 laptops (acuerdo del 28-oct) |
| Medir el "antes" | Sin empezar | Sin empezar. El motivo de cada versión ya se registra solo | Muestra de 10 a 15 emisiones terminadas |

### Los objetivos de cierre del proyecto

| Objetivo | Dónde va | Qué lo detiene |
| :-- | :-- | :-- |
| **Que las ejecutivas usen y prueben la herramienta** | No ha empezado. Todo lo probado con casos reales lo hizo Rafa | Una versión estable en sus laptops y una fecha de prueba con un caso real |
| **IA en la herramienta** | El conector está hecho (dos proveedores) y la IA solo recibe un recorte del contrato. Hoy se trabaja en modo manual. Dirección aceptó pruebas por API para cotizar el consumo | Contratar la API de prueba y medir primero en manual para poder comparar |
| **Conexión con un CRM para ver todo el proceso** | La herramienta ya deja los datos y sus llaves, y el estado EN REVISIÓN de cada fianza. El flujo completo está dibujado (v3), con la etapa de la fianza viva por auditar | Cerrar los estados del flujo con las ejecutivas, elegir el CRM y probar el acomodo importando el Registro, antes de cualquier API |

## 7. OCR: qué se midió y qué implica

**Por qué importa:** según las ejecutivas, casi 4 de cada 5 contratos llegan escaneados. En la muestra del laboratorio, 3 de cada 4 páginas son escaneadas. Sin OCR esos documentos no se pueden capturar seleccionando el texto.

**Qué se midió** (laboratorio aislado, con documentos reales que no salieron de la laptop):

| Medida | Resultado |
| :-- | :-- |
| Tiempo por página | 6.0 s en la HP 14 y 7.6 s en la Acer (mediana) |
| Memoria | Unos 550 MB de pico; cabe en el equipo más justo de la oficina |
| Aciertos fuera de INE y cédula | 65 de 76 datos, contra lo capturado a mano como referencia |
| INE y cédula | 4 de 17 datos: no sirve, ni con más resolución |

**Decidido (D-67):** motor Tesseract, que se instala junto con la herramienta; la INE y la cédula se capturan a mano; el OCR se adelanta a la herramienta en vez de esperar al final.

**Lo que implica en el uso:**

1. Un contrato escaneado se podrá capturar igual que uno con texto: se lee la página que se está viendo y el texto queda encima para seleccionarlo.
2. La primera vez que se abre una página escaneada hay que esperar unos segundos; lo leído se guarda y no se repite.
3. Lo que lee el OCR puede traer errores de un carácter y el motor no siempre avisa (en la prueba un RFC salió con una letra cambiada, sin marca de duda). Por eso la cita queda marcada como leída por OCR y **se coteja contra la imagen**. La regla de que la ejecutiva captura y decide no cambia.
4. El PDF original no se modifica.
5. La INE y la cédula siguen a mano.
6. Abre la puerta a lo que estaba detenido por los escaneados: extracción por tipo de documento (actas, poderes) y la CSF escaneada.

**Sin decidir:** si el OCR pasa a ser requisito para cerrar la v1 (D-36 lo dejaba fuera).

## 8. Qué representa

**Para la oficina.** Un solo lugar donde nace el dato: del contrato y del expediente a la ficha, al Registro y al texto de la fianza, sin teclearlo dos veces y con la evidencia a un clic. No cambia la forma de trabajar: usa el Drive, las carpetas y los nombres de archivo de la oficina, y cada regla que tiene adentro salió de cómo trabajan las ejecutivas. No sustituye al CRM: le prepara datos correctos para que el CRM organice el trabajo.

**Como cierre del proyecto de prácticas.** Es el entregable de automatización del programa: una herramienta que funciona, con su manual, su documentación técnica completa y una forma de trabajo que otra persona puede retomar (procedimiento para empezar y cerrar cada sesión, pruebas automáticas y registro de decisiones). Lo que la vuelve un resultado y no un prototipo es la parte que falta: uso real por las ejecutivas y una medición de antes y después.

## 9. Riesgos y decisiones abiertas

| Tema | Riesgo | Qué se necesita |
| :-- | :-- | :-- |
| Uso por las ejecutivas | Quedan 5 semanas de programa después de esta y coinciden con la temporada alta | Fecha para instalar la versión estable y probar un previo y un alta reales |
| Medición | Sin el "antes" no se puede decir cuánto ahorra | Quién arma la muestra de emisiones terminadas |
| OCR | Confiar en un dato mal leído | Regla de cotejo contra la imagen y decidir si entra a la v1 |
| IA | Los contratos saldrían de la oficina hacia un proveedor | Aprobar la prueba por API y revisar el aviso de privacidad |
| Modelos de texto | 13 de 33 fallan la revisión mecánica y el contenido de casi todos tiene dudas abiertas | Quién los corrige y quién aprueba el contenido en la oficina |
| Acceso al repositorio | Las computadoras de la oficina usan la sesión de GitHub de Rafa | Token de solo lectura antes de la versión estable |

## Notas del cotejo

Diferencias que encontré entre los registros. Ninguna cambia las conclusiones.

- El corte del 23-oct de *Estado y versiones* dice 294 pruebas automáticas; SESIONES.md registra 277 ese día. Aquí uso la serie de SESIONES.
- El README de `docs/` todavía dice que faltan las laptops de las ejecutivas y la copia del practicante; SEGUIMIENTO tiene cerrados C-44 y C-50. Lo vigente es el acuerdo del 28-oct: las laptops se actualizan con la versión estable.
- ALCANCE.md sigue marcado como borrador del 20-oct y deja el OCR fuera de la v1; D-67 lo adelantó. Su tabla de la v1 no refleja el cierre de la alpha.9.
- K-02 sigue redactado como "sin probar en Windows ni con contratos reales", aunque ya se probó en la laptop de Rafa y en la HP. Lo que falta son las laptops de las ejecutivas.
- Los documentos del 11-nov dicen que el diseño de la primera etapa del OCR en la herramienta está por aprobarse. Si el 12-nov ya funciona en la herramienta, hay que registrarlo en CAMBIOS, SESIONES y SEGUIMIENTO (C-46).
- Todo lo de la alpha.9.4 y la alpha.10 está probado en Linux con datos ficticios; falta verlo en Windows.
- SEGUIMIENTO (C-48, C-63) habla de 10 modelos de texto, 3 validados. La biblioteca creció a 33 y la revisión del 12-nov (bitácora S13) encontró que 20 pasan lo mecánico. Aquí uso la cifra de la revisión.
