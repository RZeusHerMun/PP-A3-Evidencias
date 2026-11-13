---
tipo: desarrollo
herramienta: FianzasAI v2
version_publicada: 2.0.0-alpha.10.1
version_en_curso: 2.0.0-alpha.10 (bloque 2) y OCR etapa 2
repositorio: RZeusHerMun/PDF_AI-v2 (privado)
corte: 2026-11-12
fuente: README, docs/CAMBIOS.md, docs/DECISIONES.md, docs/BUGS.md y docs/SESIONES.md del repositorio, bitácora privada y reunión de seguimiento del 2026-11-12
revision: ok
actualizado: 2026-11-12
---

# FianzasAI · estado y versiones

## Qué es

Una herramienta local para las ejecutivas que tiene dos partes:

- **Previo:** el contrato (o convenio, fallo o pedido) se abre a la izquierda y la ficha del previo a la derecha. Cada dato se captura seleccionando el texto en el PDF, así que queda con su página y su cita como evidencia. La herramienta calcula sola lo que se puede calcular (montos, anticipo, monto con letra) y revisa errores comunes: RFC, vigencias retroactivas, beneficiario no textual y palabras indebidas.
- **Alta / Expediente:** lee la constancia de situación fiscal (CSF) del fiado sin IA, arma la ficha del fiado con los campos que piden Berkley y MAPFRE, y controla vigencias. Desde la alpha.9 tiene el explorador del expediente: revisa lo que mandó el fiado, sugiere nombres, muestra lo que falta y lo guarda en su carpeta del Drive.
- **Texto de la fianza y cierre del previo:** el texto sale del modelo de la oficina con los datos de la ficha (v1, v2… con su motivo). El previo se cierra con el número de autorización y el PDF de la plataforma (alpha.10).
- **OCR (alpha.10.1):** una página escaneada se lee sola al llegar a ella y se captura igual que un PDF con texto. La cita queda marcada "leída por OCR" para cotejarla contra la imagen. La INE y la cédula se capturan a mano.

Corre en cada laptop. Solo escucha en la misma computadora.

Lo que la herramienta **no** hace:

- No borra ni mueve nada en el Drive. El 12-nov Dirección pidió poder borrar documentos desde el explorador, con confirmación: está por hacerse.
- No inventa datos: si un dato no está en el documento, se queda vacío.
- La IA es opcional y solo sugiere. Hoy funciona en modo manual.

## Por qué se hizo así

| Decisión | Motivo |
| :-- | :-- |
| Proyecto nuevo en vez de seguir el prototipo de AI Studio (D-01) | El prototipo automatizaba sin dejar revisión humana y dependía de un solo proveedor |
| Instalada en la laptop de cada ejecutiva y distribuida desde GitHub (D-02) | No necesita servidor y los documentos no salen de la oficina |
| La ejecutiva captura y la IA solo sugiere (D-03) | La responsabilidad del dato es de quien emite |
| Drive para escritorio con la estructura de carpetas que ya usa la oficina (D-19) | No cambia la forma de trabajar |
| Registro general en Excel que se reconstruye desde las fichas (D-20, D-24) | Una vista para consultar sin capturar dos veces y fácil de migrar a un CRM |

## Versiones

| Versión           | Fecha      | Qué trajo                                                                                                                   |
| :---------------- | :--------- | :-------------------------------------------------------------------------------------------------------------------------- |
| alpha.1 – alpha.2 | 2026-09-29 | Arranque de la v2: visor del PDF, ficha del previo, captura con evidencia, montos calculados y varias fianzas por documento |
| alpha.3           | 2026-10-02 | Ajustes de la primera prueba con contratos reales: catálogo de ramo y subramo, beneficiario textual, deshacer por captura   |
| alpha.4           | 2026-10-02 | Fianza de anticipo. **Instalada en las laptops de las ejecutivas**                                                          |
| alpha.5           | 2026-10-06 | Anticipo en monto, catálogo completo, fianzas por proveedores y póliza de RC                                                |
| alpha.6           | 2026-10-08 | **Guardar en Drive** con la estructura de la oficina y **Registro general** en Excel                                        |
| alpha.7           | 2026-10-13 | Monto afianzado editable, carpeta de archivos de la app en cada contrato y ajustes de la primera prueba con Drive           |
| alpha.8           | 2026-10-13 | **Módulo Altas:** alta rápida con la CSF                                                                                    |
| alpha.8.1         | 2026-10-15 | Actualizador nuevo para instalaciones y copias de desarrollo                                                                |
| alpha.9           | 2026-11-05 | **Explorador del expediente** cerrado, copiar faltantes para el chat, cotización rápida, acta como poderes, tarifas que edita la oficina y **texto de la fianza con modelo** ([S10](../02_Bitacora/S10.md), [S11](../02_Bitacora/S11.md), [S12](../02_Bitacora/S12.md)) |
| alpha.9.1         | 2026-11-06 | Comprobante de domicilio válido 6 meses |
| alpha.9.2         | 2026-11-07 | La ficha del fiado junta lo que traen los documentos del expediente; copiar la leyenda de veracidad; carpeta completa al fiado |
| alpha.9.3         | 2026-11-09 | El texto de la fianza dice bien la versión que sigue; manita para mover el PDF; actualizador que no se detiene sin motivo |
| alpha.9.4         | 2026-11-11 | Un PDF con texto raro del escáner ya no se ve como escaneado |
| alpha.10          | 2026-11-11 | **Cierre del previo** con número de autorización y PDF de la plataforma; agente junto a la afianzadora; guardar solo el .txt; ruta propia de los modelos |
| alpha.10.1        | 2026-11-12 | **OCR dentro de la herramienta**, etapa 1 ([S13](../02_Bitacora/S13.md)) |

Registro técnico al 12-nov: 49 errores corregidos y documentados (B-001 a B-049), 69 decisiones de diseño (D-01 a D-69) y 428 pruebas automáticas en verde. De la alpha.9.2 en adelante está probado en Linux con datos ficticios y falta probarlo en Windows. El detalle del periodo está en [Avance del desarrollo al 11-nov](Avance-del-desarrollo-al-2026-11-11.md).

## Dónde está instalada

| Computadora                 | Versión               | Nota                                                             |
| :-------------------------- | :-------------------- | :--------------------------------------------------------------- |
| HP de la oficina            | sigue la versión principal | Se actualiza con doble clic. Versión exacta al 12-nov: sin registro |
| Laptops de las ejecutivas   | alpha.4               | Instaladas el 2026-10-02. Su actualizador viejo se detiene; hay que meterles el nuevo una vez a mano (12-nov). Se acordó actualizarlas con una versión estable (28-oct) |
| Computadora del practicante | sin registro          | Copia de desarrollo |
| Mi laptop                   | alpha.10.1 en desarrollo | —                                                             |

## Medición

- **Referencia actual:** unos 5 minutos de revisión manual por contrato.
- **Primera prueba (2026-10-02):** 6 minutos de extracción en un contrato real. El tiempo de captura no se midió.
- **OCR (laboratorio, 10 y 11-nov):** 6.0 s por página en la HP 14 y 7.6 s en la Acer, unos 550 MB de memoria. Contra lo capturado a mano: 65 de 76 datos fuera de INE y cédula; en INE y cédula, 4 de 17.
- **Pendiente:** medir tiempo **y** errores de captura con las ejecutivas, contrato por contrato. No se midió en la reunión del 12-nov.

## Lo que sigue

1. Probar en Windows de la alpha.9.2 a la 10.1, con contratos escaneados reales. Actualizar a mano las laptops de las ejecutivas.
2. Lo que pidió la reunión del 12-nov ([RS02](../07_Reuniones/RS02_2026-11-12.md)): borrar documentos con confirmación, selección del OCR menos sensible, subcarpetas de fichas y versiones viejas, domicilio fiscal de la CSF, gastos variables en la cotización y cálculo de fianzas compuestas.
3. OCR, etapa 2: el resto del documento en segundo plano, la CSF escaneada y la IA sobre lo leído. O el bloque 2 de la alpha.10 (está por decidir cuál va primero).
4. Biblioteca de modelos de texto: corregir los 13 que fallan y que las ejecutivas aprueben el contenido.
5. Reglas de agentes (9-nov): agentes distintos por afianzadora y asignación entre dos agentes.
6. Conexión con el CRM que se elija, empezando por importar el Registro.
7. Pasar las instalaciones a una rama "estable" con acceso de solo lectura.

## Riesgos abiertos

- **Acceso al repositorio:** mientras duran las pruebas, las computadoras de la oficina usan mi sesión de GitHub. Antes de la versión estable se cambia por un token de solo lectura en cada laptop.
- **Uso de IA con contratos:** falta que la Dirección decida si se pueden mandar contratos a una API de IA empresarial (ver [Pendientes](../06_Pendientes-y-por-decidir.md)).
- **OCR:** un dato mal leído puede pasar sin aviso (en la prueba, una letra de un RFC ficticio salió cambiada). Por eso la cita se marca y se coteja contra la imagen.
- **Datos de prueba:** el nombre que parecía de un fiado real se cambió por uno ficticio el 2026-10-22. Sigue en la historia de git del repositorio.
