---
tipo: desarrollo
herramienta: FianzasAI v2
version_publicada: 2.0.0-alpha.8.1
version_en_curso: 2.0.0-alpha.9
repositorio: RZeusHerMun/PDF_AI-v2 (privado)
corte: 2026-10-23
fuente: README, docs/CAMBIOS.md, docs/DECISIONES.md, docs/BUGS.md y docs/SESIONES.md del repositorio, y bitácora privada
revision: ok
actualizado: 2026-10-23
---

# FianzasAI · estado y versiones

## Qué es

Una herramienta local para las ejecutivas que tiene dos partes:

- **Previo:** el contrato (o convenio, fallo o pedido) se abre a la izquierda y la ficha del previo a la derecha. Cada dato se captura seleccionando el texto en el PDF, así que queda con su página y su cita como evidencia. La herramienta calcula sola lo que se puede calcular (montos, anticipo, monto con letra) y revisa errores comunes: RFC, vigencias retroactivas, beneficiario no textual y palabras indebidas.
- **Alta / Expediente:** lee la constancia de situación fiscal (CSF) del fiado sin IA, arma la ficha del fiado con los campos que piden Berkley y MAPFRE, y controla vigencias. En la alpha.9 se agrega el explorador del expediente: revisa lo que mandó el fiado, sugiere nombres, muestra lo que falta y lo guarda en su carpeta del Drive.

Corre en cada laptop. Solo escucha en la misma computadora.

Lo que la herramienta **no** hace:

- No borra ni mueve nada en el Drive.
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
| alpha.9           | en curso   | Explorador del expediente del fiado, copiar faltantes para el chat, cotización rápida, acta como poderes y tarifas que edita la oficina (ver [S10](../02_Bitacora/S10.md))                                                      |

Registro técnico: 30 errores corregidos y documentados (B-001 a B-030) y 46 decisiones de diseño (D-01 a D-46). Al 23-oct, la alpha.9 tenía 294 pruebas automáticas en verde. Lo del 23-oct está en una rama aparte y falta probarlo en Windows.

## Dónde está instalada

| Computadora                 | Versión               | Nota                                                             |
| :-------------------------- | :-------------------- | :--------------------------------------------------------------- |
| HP de la oficina            | alpha.8.1             | Actualizada el 2026-10-15                                        |
| Laptops de las ejecutivas   | anterior a la 8.1     | Instaladas el 2026-10-02 con la alpha.4. Falta pasarlas a la 8.1 |
| Computadora del practicante | alpha.8.1             | Copia de desarrollo. El `.env` ya lee (2026-10-21)           |
| Mi laptop                   | alpha.9 en desarrollo | —                                                                |

## Medición

- **Referencia actual:** unos 5 minutos de revisión manual por contrato.
- **Primera prueba (2026-10-02):** 6 minutos de extracción en un contrato real. El tiempo de captura no se midió.
- **Pendiente:** medir tiempo **y** errores de captura con las ejecutivas, contrato por contrato.

## Lo que sigue

1. Probar en Windows lo del 23-oct e integrarlo. Cerrar la alpha.9: ficha del fiado editable, que no se pierda lo capturado al cambiar de documento, alta guardando en `EXPEDIENTE/` y Registro.
2. Extracción por tipo de documento y **OCR para escaneados**. En una muestra real, 8 de 23 PDF son escaneados. La prueba de OCR sube de puesto (D-37): Tesseract y, si no alcanza, PaddleOCR. Falta decidir qué se recorre. En el trabajo de campo, los 4 contratos que vio el practicante llegaron escaneados.
3. Cotejo de documentos, y unir y dividir PDF.
4. Biblioteca de modelos de texto por subramo y beneficiario para generar previos. Desde el 22-oct hay un machote de campos para el oficio de retroactividad.
5. Conexión con ClickUp o con el CRM que se elija.
6. Pasar las instalaciones a una rama "estable" con acceso de solo lectura.

## Riesgos abiertos

- **Acceso al repositorio:** mientras duran las pruebas, las computadoras de la oficina usan mi sesión de GitHub. Antes de la versión estable se cambia por un token de solo lectura en cada laptop.
- **Uso de IA con contratos:** falta que la Dirección decida si se pueden mandar contratos a una API de IA empresarial (ver [Pendientes](../06_Pendientes-y-por-decidir.md)).
- **Datos de prueba:** el nombre que parecía de un fiado real se cambió por uno ficticio el 2026-10-22. Sigue en la historia de git del repositorio.
