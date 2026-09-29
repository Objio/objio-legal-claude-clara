---
name: documentos-objio-legal
description: Produce documentos jurídicos de OBJIO LEGAL en Word (.docx) y PDF con la marca de la casa —demandas, escritos, contratos, opiniones jurídicas, poderes, actos de alguacil, cartas, informes y propuestas ejecutivas— con la tipografía, los márgenes, los colores, el encabezado y la firma canónicos. Elige la marca según el contexto (OBJIO LEGAL | MEDICAL LAW, OBJIO LEGAL u OSM LEGAL), pone la firma de la Lic. Clara Alcántara o la del Lic. Gilberto Objío Subero según a nombre de quién salga, y entrega siempre las dos versiones, DOCX y PDF. Incluye el informe ejecutivo premium (propuesta corporativa, briefing normativo, memorando). Úsala cuando digas «hazlo en Word», «genera el PDF», «redacta la demanda», «prepara el contrato», «opinión jurídica», «carta al cliente», «acto de alguacil», «informe ejecutivo», «propuesta de servicios», «ponle el membrete», «pásalo al formato de la casa».
---

# Documentos OBJIO LEGAL (Word y PDF con la marca de la casa)

Esta skill convierte el contenido jurídico en un documento terminado, listo para firmar, depositar o remitir. **Claude redacta; el código solo da formato.** El contenido se escribe primero, completo y verificado; después se genera el archivo.

## Reglas que no se negocian

1. **Doble formato siempre:** se entregan el .docx (editable) y el .pdf (para remitir o depositar).
2. **Producto final cerrado:** el documento sale accionable (sin corchetes, sin «[completar]», sin campos en blanco que Claude podía llenar con un dato del expediente), verificado (cada dato contra su fuente) y perfecto (ortografía, tildes, formato, firma, anexos).
3. **Nunca te confías:** después de generar el archivo, se abre y se comprueba (texto, tildes, número de páginas, encabezado, firma). Que el código no diera error no significa que el documento esté bien.
4. **Lo que se puede adelantar, se adelanta:** si el documento va a remitirse, se entrega también el correo de remisión redactado; si lleva anexos, se lista cada anexo con su nombre exacto. A Clara solo le queda lo que únicamente ella puede hacer (firmar, decidir, enviar).
5. **Verificación antes de enviar:** todo documento final dirigido a un tercero pasa por la skill `verificacion-antes-de-enviar` antes de entregarse.
6. **Cero invenciones:** ningún número de ley, artículo, sentencia, cifra, cliente o persona que no conste en el expediente o en una fuente primaria consultada. Si falta un dato que solo Clara tiene, se pregunta una sola vez, agrupando todas las preguntas.
7. **Sin emojis ni iconos** en ningún documento.

## Marca según el contexto

| Contexto del asunto | Encabezado |
|---|---|
| Derecho médico, responsabilidad sanitaria, clínicas, hospitales, profesionales de la salud | **OBJIO LEGAL \| MEDICAL LAW** (entidad: MDCLAW EIRL) |
| Corporativo o general | **OBJIO LEGAL** |
| Asuntos llevados por OSM LEGAL | **OSM LEGAL** |
| Contrato entre terceros (el cliente con su proveedor, socio, etc.) | **Formato neutro:** sin membrete ni logo del despacho; solo las partes. Si se desea, «Preparado por OBJIO LEGAL» al final, nunca en el encabezado. |

## Formato de Word (especificación exacta)

| Elemento | Valor |
|---|---|
| Papel | Carta (8,5 × 11 pulgadas), salvo que el tribunal o el cliente pidan otro |
| Márgenes | Izquierdo 3 cm · superior, inferior y derecho 2,5 cm |
| Fuente | Times New Roman 12 pt en todo el cuerpo |
| Interlineado | 1,5 |
| Alineación | Justificada en el cuerpo; firma alineada a la izquierda |
| Título del documento | Times New Roman 14 pt, negrita, centrado, color navy `#1B365D` |
| Títulos de sección | Times New Roman 12–13 pt, negrita, navy `#1B365D` |
| Encabezado | La marca del contexto, Times New Roman 10 pt, negrita, navy, alineada a la derecha, con **filete dorado de 2 pt** (`#C9A962`) debajo |
| Pie de página | «Página X de Y» centrado, 9 pt, gris `#546879`; si procede, «CONFIDENCIAL» en `#8B0000` |
| Tablas | Cabecera con fondo navy `#1B365D` y texto blanco en negrita; filas alternas en `#EEF2F7`; texto 10 pt |
| Montos | En letras y en números, y deben coincidir: «CIEN MIL PESOS DOMINICANOS CON 00/100 (RD$100,000.00)» |

### Colores de la marca
Azul, blanco y gris. **El dorado es solo un detalle.**

| Uso | Valor |
|---|---|
| Navy profundo · titulares, fondos de cabecera | `#1B365D` |
| Azul medio · bandas, segundo plano, acento sobre fondo claro | `#2F5FB0` |
| Acento sobre fondo oscuro · rótulos y filetes | `#8FB4E3` |
| Grises · texto secundario y filetes | `#546879` → `#798CA0` → `#D3DDEA` |
| Papel | `#EEF2F7` · `#F7F5F0` |
| **Oro · solo filete de 2 pt** (nunca texto, relleno ni borde de tarjeta) | `#C9A962` |
| Confidencial | `#8B0000` |

El acento sigue al fondo: sobre fondo oscuro, azul claro `#8FB4E3`; sobre fondo claro, azul medio `#2F5FB0`. Ningún texto puede quedar del mismo color (o casi) que su fondo: se revisa a ojo en el PDF.

## Firma canónica

**Cuando el documento sale a nombre del Lic. Gilberto Objío Subero:**
```
Atentamente,

GILBERTO OBJÍO SUBERO
Abogado
PhD(c) en Inteligencia Artificial Productividad Empresarial
[OBJIO LEGAL | MEDICAL LAW, OBJIO LEGAL u OSM LEGAL, según el contexto]
```

**Cuando el documento sale a nombre de la Lic. Clara Alcántara:**
```
Atentamente,

Lic. Clara Alcántara
Abogada
[OBJIO LEGAL | MEDICAL LAW u OBJIO LEGAL, según el contexto]
```

Reglas de la firma:
- Si Clara no indica a nombre de quién sale, se pregunta una vez. Los escritos en los que el Lic. Objío es el abogado constituido salen a su nombre, aunque los prepare Clara.
- La firma va a continuación del último párrafo, **sin salto de página forzado**: nunca una página con solo la firma.
- Datos de contacto del despacho que pueden figurar en el documento: domicilio profesional, teléfono de oficina y web (ver más abajo). Cualquier otro dato personal (cédula, matrícula, celular, correo) solo si el documento lo exige y Clara lo aporta en la conversación.

**Datos institucionales del despacho:**
- Domicilio profesional: Av. Sarasota esq. El Embajador, Condominio Jardines del Embajador, Edif. 15, Suite 247, Bella Vista, Santo Domingo, D.N.
- Oficina: (809) 532-7773
- Web: objiolegal.com

## Cómo se genera el archivo en Claude

En Claude (web o escritorio) no hay carpetas locales del despacho. El archivo se genera con **la herramienta de creación de archivos o de ejecución de código de Claude**, y se entrega como descarga.

1. Redactar el contenido completo en la conversación (o en un borrador interno) y verificarlo.
2. Generar el .docx con `python-docx` usando el código de `formato_word.md` (márgenes, fuente, encabezado con filete, pie «Página X de Y», tablas y firma ya resueltos).
3. Generar el .pdf a partir del .docx (LibreOffice en modo sin interfaz, si está disponible en el entorno: `soffice --headless --convert-to pdf archivo.docx`). Si no lo está, generar el PDF directamente reproduciendo el mismo formato, o como último recurso entregar el .docx e indicar a Clara «Archivo > Guardar como > PDF» en Word.
4. **Abrir y comprobar** el resultado: extraer el texto del PDF y revisar tildes, número de páginas, encabezado, pie, firma y que no quede ningún corchete ni asterisco de Markdown impreso.
5. Si no hay herramienta de ejecución de código disponible, entregar el texto final con la especificación de formato de esta skill para que se aplique en Word, y decírselo a Clara con claridad.

**Nombre del archivo:** descriptivo y sin sufijos de versión: `Opinion_Juridica_Responsabilidad_Medica_2026-09-29.docx`, no `..._v2_FINAL.docx`. Cuando hay una versión nueva, reemplaza a la anterior con el mismo nombre (la fecha puede cambiar). Sin espacios dobles ni caracteres raros.

**Markdown:** si el contenido se redactó en Markdown, la conversión debe resolver negritas y cursivas; ningún `**` ni `#` puede quedar impreso. Las líneas de firma, direcciones y encabezados de actos se conservan como líneas separadas, no se funden en un párrafo.

## Tipos de documento

La estructura de cada tipo (demanda, escrito, contrato, opinión, poder, acto de alguacil, carta, correo de remisión) y el estándar de calidad de contratos están en `tipos_de_documento.md`. El informe ejecutivo premium (propuestas, briefings, memorandos con estética corporativa en A4) está en `informe_ejecutivo.md`.

## Ortografía (tolerancia cero)

- Tildes completas: á é í ó ú ñ Á É Í Ó Ú Ñ ¿ ¡. Mayúsculas acentuadas («ARTÍCULO», «OBJÍO»).
- Ningún carácter corrupto (del tipo `Ã©`, `Â`).
- Nombres de personas y entidades exactamente como constan en su documento de identidad o registro.
- Fechas en el formato del documento: en actos y contratos, en letras y números («a los veintinueve (29) días del mes de septiembre del año dos mil veintiséis (2026)»).

## Cierre de la entrega

La respuesta final a Clara contiene:
1. Los dos archivos (DOCX y PDF).
2. Una línea de verificación: «Verificado: N datos contra fuente · 0 pendientes» (o la lista exacta de lo pendiente y por qué).
3. Si procede, el correo de remisión ya redactado (breve: 20 a 60 palabras cuando remite un documento; el contenido vive en el anexo).
4. Solo lo que Clara debe hacer ella: firmar, decidir o enviar.
