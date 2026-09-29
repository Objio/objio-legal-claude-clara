---
name: redline-documentos-terceros
description: Revisa y corrige documentos de terceros (contratos, acuerdos, políticas, manuales, borradores de colegas o de la contraparte) al estilo de los abogados de fusiones y adquisiciones: corrige directamente el .docx, resalta en amarillo todo lo nuevo o modificado, ancla en el margen un comentario de Word con el porqué jurídico de cada cambio y renombra el archivo con el sufijo «— Rev. OBJIO LEGAL». Los comentarios salen a nombre de la Lic. Clara Alcántara (o del Lic. Gilberto Objío Subero si actúa por él). También responde los comentarios de la contraparte, compara una versión devuelta con la enviada y prepara el correo breve de remisión. Úsala cuando digas «revisa este contrato», «corrige este documento», «haz el redline», «ponle comentarios», «marca los cambios en amarillo», «responde los comentarios», «qué cambió la contraparte», «devolvieron el contrato con observaciones».
---

# Redline de documentos de terceros (estilo fusiones y adquisiciones)

Cuando un documento es de otro (la contraparte, el cliente, un colega, un proveedor), **no se entrega solo un informe de observaciones: se entrega el documento corregido**. El destinatario trabaja sobre el archivo; un comentario anclado al párrafo exacto es accionable, un párrafo de correo no.

## Las cinco piezas del método

1. **Corrección directa** sobre el propio .docx: el texto queda como debe quedar.
2. **Resaltado amarillo** en todo texto nuevo o modificado, para que el destinatario vea de un vistazo qué cambió.
3. **Comentario de Word al margen** en cada cambio, con **el porqué jurídico**: qué riesgo corrige, qué norma lo exige o qué interés del cliente protege. No «se mejora la redacción», sino la razón concreta.
4. **Nombre del archivo** con el sufijo `— Rev. OBJIO LEGAL`: `Contrato de servicios — Rev. OBJIO LEGAL.docx`.
5. **Plagio detectado** (texto copiado de otra organización sin adaptar): no se parchea; se reescribe el documento completo desde cero y se deja una nota al pie que lo explique.

**Autor de los comentarios:** `Lic. Clara Alcántara — OBJIO LEGAL` (iniciales CA). Si Clara indica que actúa por el Lic. Objío o el documento sale a su nombre: `Lic. Gilberto Objío Subero — OBJIO LEGAL` (iniciales GOS).

## Reglas que gobiernan la revisión

- **Producto final cerrado:** lo que se entrega es accionable (el destinatario puede firmar o negociar ya), verificado (cada dato y cada norma citada en un comentario, contra su fuente primaria vigente) y perfecto (ortografía, formato intacto, ningún cambio sin marcar).
- **Nunca te confías:** después de guardar el archivo se comprueba mecánicamente que cada comentario tiene su referencia y que todo lo modificado está resaltado. Leer los pasajes amarillos enseña lo que se marcó, nunca lo que se modificó sin marcar.
- **Lo que se puede adelantar, se adelanta:** si de la revisión salen mejoras, el documento mejorado se entrega en la misma respuesta, junto con el correo de remisión ya redactado. Proponer cambios sin entregar el documento aplicado es trabajo sin terminar.

## Procedimiento

### 1. Leer todo el documento, incluido lo que no se ve
Un .docx es un contenedor: además del cuerpo tiene **comentarios, control de cambios, notas al pie, encabezados, pies y tablas**. En un documento ajeno, ahí está lo que la otra parte piensa. Antes de opinar:
- listar los comentarios existentes (autor y texto);
- detectar si trae control de cambios (inserciones y supresiones sin aceptar); si lo trae, revisarlo como tal, porque la lectura normal muestra la versión con todo aceptado;
- leer tablas, notas y encabezados.

Si un comentario del cliente o de la contraparte ya señala un punto, no se presenta como hallazgo propio: se responde.

### 2. Si es una versión devuelta: comparar el cuerpo antes de leer los comentarios
Comparar el texto con la versión que se envió. Hay tres escenarios distintos:
1. **Contraofertaron redacción** (hay texto nuevo suyo): se negocia cláusula por cláusula.
2. **Objetaron por comentario y dejaron el texto intacto:** no hubo contraoferta; el documento sigue siendo el nuestro. Lo que mueve la negociación es devolver una versión que **incorpore todo lo aceptable de sus objeciones**, para que lo que quede se lea como cierre y no como una ronda nueva.
3. **Suprimieron o cambiaron algo sin comentarlo:** es lo primero que hay que cazar y señalar.

Cada objeción se clasifica en **acogida** (tienen razón), **cedible** (decisión de negocio legítima, se cambia por otra cosa) o **innegociable** (orden público o riesgo nuclear del cliente). Para cada innegociable se lleva una fórmula intermedia, no un «no». Si la contraparte propuso un mecanismo útil, se usa su propia fórmula donde se resistía.

La segunda ronda se marca con **otro color** (verde sobre el amarillo anterior) para que se distinga qué es nuevo.

### 3. Revisar el fondo
Por cada cláusula o sección: ¿protege al cliente?, ¿es exigible?, ¿cumple la norma aplicable leída en bloque y vigente?, ¿falta algo? Para contratos, usar el estándar de calidad de la skill `documentos-objio-legal` (`tipos_de_documento.md`): partes completas, objeto con exclusiones, precio con ITBIS, terminación, confidencialidad, limitación de responsabilidad, controversias, coletilla y legalización de firmas.

### 4. Aplicar el redline
Con ejecución de código: usar `codigo_redline.md` (python-docx). Cada cambio lleva texto nuevo resaltado y su comentario. Las observaciones que no cambian texto (decisiones de negocio del cliente, preguntas) van como comentario sin resaltado. Las respuestas a comentarios de la contraparte se anclan en el mismo párrafo, empezando por «En respuesta a [autor]: …».

Reglas técnicas que evitan dañar el documento ajeno:
- Trabajar sobre una copia; el original no se toca.
- No reconstruir párrafos enteros: al sustituir texto se conservan los comentarios, notas y marcas que ya había (incluidos los de la contraparte).
- Conservar el formato del documento (su fuente, sus estilos, su numeración). El redline no le impone la marca de OBJIO LEGAL a un documento ajeno.

### 5. Verificar antes de entregar
- Prueba mecánica: `verificar(original, revisado)` debe devolver una lista vacía (todo comentario con su referencia; todo párrafo nuevo o modificado con resaltado).
- Volver a listar los comentarios del archivo final: deben estar los propios y los ajenos.
- Pasar el documento por la skill `verificacion-antes-de-enviar`: cada norma, dato y cifra de los comentarios se verifica contra su fuente.

### 6. Entregar
En una sola respuesta:
1. **El documento redline** (`… — Rev. OBJIO LEGAL.docx`; y PDF si se va a remitir así).
2. **Un resumen breve** para Clara: veredicto general, la observación de fondo que decide, y los puntos que requieren una decisión suya o del cliente.
3. **El correo de remisión** ya redactado, **corto** (de 3 a 6 líneas): qué se revisó, el veredicto, la observación que decide, remisión a los comentarios del documento para el resto y la conclusión operativa («con esos ajustes, el contrato puede firmarse»). Nada de repetir en el correo lo que ya dicen los comentarios.

## Alternativa manual (sin ejecución de código)

Si en la conversación no hay herramienta de ejecución de código, entregar una **tabla de redline** que Clara aplica en Word en pocos minutos:

| # | Ubicación (cláusula y primeras palabras) | Texto actual | Texto propuesto | Comentario para el margen (el porqué) |
|---|---|---|---|---|

Y las instrucciones en Word: sustituir el texto; seleccionarlo y aplicar «Color de resaltado del texto > Amarillo»; con el texto seleccionado, «Revisar > Nuevo comentario» y pegar el comentario; para responder a un comentario existente, «Responder» en el propio comentario. Antes de empezar, en «Archivo > Opciones > General», poner como nombre de usuario `Lic. Clara Alcántara — OBJIO LEGAL` para que los comentarios salgan con su autoría. Guardar con el sufijo `— Rev. OBJIO LEGAL`.

## Errores que esta skill no permite

- Entregar un informe de observaciones sin el documento corregido.
- Cambiar texto sin resaltarlo, o resaltar sin comentar el porqué.
- Comentarios vagos («mejorar», «revisar redacción») sin la razón jurídica.
- Borrar o perder los comentarios de la contraparte al editar.
- Opinar sobre un .docx sin haber leído sus comentarios y su control de cambios.
- Rebatir punto por punto una versión que volvió con el texto intacto, en lugar de incorporar lo aceptable.
- Correos largos que duplican lo que ya está en los comentarios.
- Imponer la marca del despacho a un documento ajeno.
