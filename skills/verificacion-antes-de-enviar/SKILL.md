---
name: verificacion-antes-de-enviar
description: Contraexamen adversarial de todo documento que va a salir de OBJIO LEGAL hacia un cliente, una contraparte, un tribunal o una autoridad (escrito, contrato, opinión, informe, correo o acto). Extrae cada dato verificable —nombres, cédulas, RNC, montos, fechas, plazos, números de expediente, artículos de ley, sentencias— y lo contrasta con la fuente primaria (el expediente adjunto, Gaceta Oficial, Consultoría Jurídica del Poder Ejecutivo, Poder Judicial, Tribunal Constitucional, DGII), corrige el documento y repite hasta cero hallazgos. Entrega la tabla de hallazgos y la versión corregida. Úsala cuando digas «verifica antes de enviar», «revísalo antes de mandarlo», «doble chequeo», «contraexamen», «pair review», «verifica las cifras», «revisa las citas», «¿está listo para enviar?», o al terminar cualquier documento final dirigido a un tercero. No aplica a borradores internos de trabajo.
---

# Verificación antes de enviar (contraexamen adversarial)

Todo documento que sale de OBJIO LEGAL se somete a contraexamen antes del envío. La pregunta fija es:

> **«Si el cliente molesto, el juez o la contraparte leen esto buscando un error, ¿qué encuentran?»**

El objetivo es **cero defectos al destinatario**. No se revisa «por encima»: se extrae cada afirmación verificable y se contrasta, una por una, con su fuente primaria.

## Tres reglas que gobiernan esta skill

1. **Producto final cerrado.** El documento solo está listo cuando es a la vez:
   - **Accionable:** el destinatario puede actuar ya, sin pedir nada más; cero campos en blanco ni corchetes pendientes.
   - **Verificado:** cada dato, monto, RNC, cédula, fecha, plazo y cita está validado contra su fuente primaria.
   - **Perfecto:** cero defectos visibles (tildes, caracteres corruptos, montos que no cuadran, anexos mencionados y no adjuntos, firma, formato).

   Prueba final: *si el Lic. Objío o la cliente reabren este documento dentro de tres semanas, con alguien al teléfono, ¿sigue siendo perfecto sin tocarlo?*

2. **Nunca te confías.** Nada se da por cierto porque «ya estaba en la versión anterior», porque lo redactó Claude, porque viene de una plantilla o porque «siempre ha sido así». La pregunta ante cada dato es: *¿cómo sé que esto es verdad ahora?* Si no hay respuesta verificable, no se afirma. Una verificación que no se hizo en esta conversación no cuenta como verificación.

3. **Lo que se puede adelantar, se adelanta.** La revisión no termina en una lista de observaciones: entrega también el documento corregido. Si del contraexamen salen mejoras de redacción o de fondo, se aplican al documento (en un documento de un tercero, con el método de la skill `redline-documentos-terceros`). Lo único que queda para Clara es lo que solo ella puede decidir o hacer.

## Cuándo se usa

| Situación | ¿Aplicar? |
|---|---|
| Clara lo pide («verifica antes de enviar», «doble chequeo», «contraexamen») | Siempre |
| Termina un documento final para cliente, contraparte, tribunal o autoridad | Sí, antes de entregarlo |
| Correo a un tercero con cifras, fechas o compromisos | Sí |
| Contrato para firma, opinión jurídica, informe ejecutivo, escrito para depósito, acto de alguacil | Sí |
| Borrador interno de trabajo o nota para uso propio | No |

## Fuentes que se usan (de mayor a menor autoridad)

| Nivel | Fuente | Qué se verifica ahí |
|---|---|---|
| 1 | **Expediente que Clara adjunta** en la conversación (contratos, actas, sentencias, correspondencia, cédulas, certificaciones) | Hechos del caso, nombres, identificaciones, montos, fechas, números de expediente |
| 1 | **Gaceta Oficial** (texto publicado de leyes y decretos) | Número, fecha y texto literal de la norma |
| 2 | **Consultoría Jurídica del Poder Ejecutivo** — consultoria.gov.do | Texto de leyes, decretos y reglamentos; modificaciones y derogaciones |
| 2 | **Poder Judicial** — poderjudicial.gob.do | Sentencias de la Suprema Corte de Justicia y de tribunales; datos de expedientes publicados |
| 2 | **Tribunal Constitucional** — tribunalconstitucional.gob.do | Sentencias TC/NNNN/AA, su fecha y su ratio |
| 2 | **DGII** — dgii.gov.do, consulta de RNC y cédula | Razón social, nombre comercial, RNC y estado del contribuyente |
| 3 | **Búsqueda web** dirigida a sitios oficiales | Localizar el documento primario cuando no se tiene a mano |
| 4 | Doctrina, prensa o conocimiento general | Nunca basta por sí sola para un dato que sale al tercero |

Reglas sobre las fuentes:
- Una cita se verifica **leyendo el texto de la norma o de la sentencia**, no un resumen ni un blog. Nunca un artículo aislado: se lee el bloque (el artículo, sus párrafos y los artículos vecinos que lo modulan).
- Toda norma citada se comprueba **vigente** y en su **redacción actual** (buscar modificaciones y derogaciones posteriores).
- Si la búsqueda web no está disponible en la conversación o la fuente no se puede abrir, el dato queda como **NO VERIFICADO**, no como correcto. Se le dice a Clara qué documento hace falta para cerrarlo.
- No se usan fuentes de memoria («creo que el artículo dice…»). Si no se abrió la fuente, no se verificó.

## Procedimiento

### Paso 1 · Leer el documento completo
Leer el documento entero, no un resumen. En un .docx incluye lo que no está en el cuerpo: encabezados, pies, notas al pie, tablas, comentarios y control de cambios. Identificar tipo (correo, escrito, contrato, opinión, informe, acto), destinatario y propósito.

### Paso 2 · Extraer todas las afirmaciones verificables
Hacer la lista completa, por categorías:

| Categoría | Ejemplos |
|---|---|
| Identidad | Nombres de personas y empresas, cédulas, RNC, registro mercantil, domicilios, calidades («en su calidad de…») |
| Cifras y fechas | Montos (en letras y en números, que deben coincidir), fechas, plazos, porcentajes, números de expediente, de acto o de sentencia |
| Citas jurídicas | «Art. X de la Ley Y», decretos, resoluciones, sentencias SCJ y TC, con su fecha |
| Hechos | Secuencia de lo ocurrido, quién hizo qué y cuándo, partes que intervienen |
| Compromisos | Plazos prometidos, próximos pasos, entregables, condiciones |
| Forma | Ortografía y tildes, caracteres corruptos, concordancia, anexos mencionados, firma, fecha del documento, numeración de páginas |

### Paso 3 · Verificar cada afirmación
Cada una recibe un estado y su prueba:

- **OK** — confirmada; se anota la fuente exacta (documento del expediente y página, o URL oficial).
- **ERROR** — la fuente dice otra cosa; se anota lo que dice el documento y lo que dice la fuente.
- **NO VERIFICADO** — no hay fuente disponible en la conversación; se anota qué haría falta.

Prohibido marcar OK sin fuente concreta. «Debe ser correcto porque viene de la plantilla» no es una fuente.

### Paso 4 · Doble guarda reputacional
- **Hacia dentro:** ¿cómo lo leería un cliente molesto, un juez, la DGII o la contraparte? ¿Hay algo que pueda usarse contra el despacho o contra el cliente (una admisión, un plazo mal contado, una promesa imprudente, un tono inadecuado)?
- **Hacia fuera:** ¿hay algo que dañe injustamente a un tercero de buena fe (un dato personal innecesario, una afirmación sin prueba)?

### Paso 5 · Tabla de hallazgos
Presentar a Clara, en este formato:

```
VERIFICACIÓN ANTES DE ENVIAR · [nombre del documento] · [fecha]
Documento: [tipo] · Destinatario: [quién] · Ciclo: N de 5
Afirmaciones revisadas: X  (OK: a · ERROR: b · NO VERIFICADO: c)
```

| # | Gravedad | Dato | El documento dice | La fuente dice | Fuente consultada | Acción |
|---|---|---|---|---|---|---|
| 1 | P0 | RNC de la demandada | 1-01-XXXXX-X | 1-01-YYYYY-Y | DGII, consulta RNC | Corregido |
| 2 | P1 | Art. citado | Art. 44 | Art. 45 (el 44 regula otra cosa) | consultoria.gov.do | Corregido |
| 3 | P2 | Tilde | «dias» | «días» | Ortografía | Corregido |

Gravedad:
- **P0** — error que cambia el efecto jurídico o expone al despacho: identidad, monto, plazo, norma, sentencia, fecha, parte equivocada.
- **P1** — error de precisión o de fundamento: cita imprecisa, dato incompleto, afirmación sin soporte.
- **P2** — forma: ortografía, formato, estilo.

### Paso 6 · Corregir el documento
Aplicar todas las correcciones directamente sobre el documento, conservando su formato, membrete y firma. Si es un .docx o .pdf, generar el archivo corregido con la herramienta de creación de archivos o de ejecución de código de Claude (ver skill `documentos-objio-legal`). Si es un correo, entregar el texto corregido listo para copiar.

### Paso 7 · Repetir hasta cero hallazgos
Volver al Paso 2 sobre el documento **ya corregido**: una corrección puede introducir un error nuevo. El ciclo termina cuando no queda ningún ERROR y ningún NO VERIFICADO sin explicar. Máximo cinco ciclos; si no converge, se detiene y se presenta a Clara exactamente qué dato bloquea y qué documento o decisión lo resolvería.

### Paso 8 · Cierre
Entregar en una sola respuesta:
1. El documento corregido (archivo o texto).
2. La tabla de hallazgos del ciclo final y el resumen de ciclos: «Convergió en N ciclos · X afirmaciones verificadas · listo para enviar».
3. Solo lo irreductible para Clara: los datos que únicamente ella puede aportar (con el mejor dato disponible ya propuesto) y las decisiones que le corresponden. Nada de «próximos pasos» que Claude podía hacer.

## Errores que esta skill no permite

- Verificar solo lo evidente (montos grandes) y dejar pasar tildes, fechas o anexos.
- Marcar OK sin fuente concreta.
- Corregir sin volver a verificar el documento corregido.
- Cerrar con datos NO VERIFICADOS sin decírselo expresamente a Clara.
- Citar un artículo sin haber leído su texto vigente, o leerlo aislado de su bloque.
- Dar por buena una cifra que no coincide en letras y en números.
- Entregar la lista de observaciones sin el documento corregido.
- Revisar solo el cuerpo de un .docx e ignorar comentarios, control de cambios, encabezados y notas.

## Relación con otras skills

- `documentos-objio-legal`: al terminar un documento final, se pasa por esta verificación antes de entregarlo.
- `redline-documentos-terceros`: si el documento revisado es de un tercero, las correcciones se aplican con redline (amarillo más comentario al margen).
