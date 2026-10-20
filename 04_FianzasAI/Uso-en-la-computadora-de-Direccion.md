---
tipo: guia-uso
herramienta: FianzasAI v2
corte: 2026-10-20
---

# FianzasAI en la computadora de Dirección

La instalación la hacemos juntos, una sola vez. Esta nota explica qué queda en su computadora y cómo se usa.

## Qué queda instalado

- Una carpeta **FianzasAI** en *Documentos*, conectada al repositorio de la herramienta.
- Dos accesos:
  - **`Iniciar FianzasAI.bat`** abre la herramienta en el navegador. La ventana negra tiene que quedarse abierta mientras se usa.
  - **`Actualizar FianzasAI.bat`** baja la versión más nueva. Cuando le avise de una versión nueva, se cierra FianzasAI y se le da doble clic.
- La computadora descarga con un **acceso de solo lectura**: desde ahí no se puede cambiar el código.

## Cómo se usa

- **Previo:** se arrastra el contrato en PDF. Se da clic en un campo, se selecciona el texto en el PDF y se presiona Enter. El botón **p.N** de cada campo muestra de dónde salió el dato.
- **Alta / Expediente:** se arrastra la CSF del fiado. La herramienta llena la ficha sola y marca en verde de dónde tomó cada dato.
- **Registro:** si la computadora tiene configurado el Drive, el botón **Registro** arma `REGISTRO FIANZASAI.xlsx` con todas las fichas guardadas por todas las laptops. Sirve para consultar: se abre, se revisa y se cierra.

## Dónde ver el desarrollo

- **Código y documentación:** en GitHub, repositorio `PDF_AI-v2`. La carpeta `docs/` tiene cuatro registros:
  - `CAMBIOS.md`: qué trae cada versión.
  - `DECISIONES.md`: por qué se hizo cada cosa.
  - `BUGS.md`: errores encontrados y corregidos.
  - `SESIONES.md`: bitácora del desarrollo.
- **Resumen:** [Estado y versiones](Estado-y-versiones.md), en este mismo repositorio.

## Si algo falla

Una foto de la ventana negra y me la manda. No hace falta borrar ni reinstalar nada.
