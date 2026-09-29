# Formato de Word de OBJIO LEGAL — código para la ejecución de código de Claude

Este código aplica la especificación de la skill: papel carta, márgenes 3 cm a la izquierda y 2,5 cm en el resto, Times New Roman 12, interlineado 1,5, texto justificado, encabezado con la marca en navy y filete dorado de 2 pt, pie «Página X de Y», tablas con cabecera navy y firma canónica. Se probó con python-docx 1.2 y el resultado se abrió en Word sin avisos.

## Uso

```python
doc = documento_objio(marca="OBJIO LEGAL | MEDICAL LAW", confidencial=True)
doc.add_paragraph("OPINIÓN JURÍDICA", style="Title")
doc.add_heading("I. Hechos", level=1)
doc.add_paragraph("Texto del párrafo…")
tabla(doc, ["Concepto", "Monto"], [["Honorarios", "RD$…"]])
firma(doc, firmante="clara", entidad="OBJIO LEGAL | MEDICAL LAW")   # o firmante="gilberto"
doc.save("Opinion_Juridica_2026-09-29.docx")
```

Después, convertir a PDF (`soffice --headless --convert-to pdf Opinion_Juridica_2026-09-29.docx`) y **abrir el PDF para comprobarlo** (texto, tildes, páginas, encabezado, firma).

Notas:
- `marca`: «OBJIO LEGAL | MEDICAL LAW», «OBJIO LEGAL» u «OSM LEGAL». En un contrato entre terceros no se usa `documento_objio`: se crea un `Document()` con los mismos márgenes y fuente, sin encabezado de marca.
- Si el contenido viene en Markdown, convertir negritas (`**texto**`) y cursivas (`*texto*`) en runs con `bold`/`italic`; nunca dejar los asteriscos impresos.
- El pie usa campos de Word: el total de páginas se actualiza al abrir o al convertir a PDF.

## Código

```python
from docx import Document
from docx.enum.table import WD_TABLE_ALIGNMENT
from docx.enum.text import WD_ALIGN_PARAGRAPH, WD_LINE_SPACING
from docx.oxml import OxmlElement
from docx.oxml.ns import qn
from docx.shared import Cm, Pt, RGBColor

NAVY = RGBColor(0x1B, 0x36, 0x5D)
GRIS = RGBColor(0x54, 0x68, 0x79)
ROJO_CONFIDENCIAL = RGBColor(0x8B, 0x00, 0x00)
ORO_HEX = "C9A962"        # solo filete de 2 pt; nunca texto ni relleno
PAPEL_HEX = "EEF2F7"      # filas alternas de tabla
NAVY_HEX = "1B365D"


def _campo(parrafo, instruccion):
    """Inserta un campo de Word (PAGE, NUMPAGES) que se actualiza solo."""
    for tipo, texto in (("begin", None), (None, instruccion), ("end", None)):
        run = parrafo.add_run()
        if tipo:
            fc = OxmlElement("w:fldChar")
            fc.set(qn("w:fldCharType"), tipo)
            run._r.append(fc)
        else:
            it = OxmlElement("w:instrText")
            it.set(qn("xml:space"), "preserve")
            it.text = texto
            run._r.append(it)


def _filete(parrafo, lado="bottom", color=ORO_HEX, grosor_octavos=16):
    """Filete bajo (o sobre) un párrafo. 16 octavos de punto = 2 pt."""
    ppr = parrafo._p.get_or_add_pPr()
    bdr = OxmlElement("w:pBdr")
    borde = OxmlElement(f"w:{lado}")
    borde.set(qn("w:val"), "single")
    borde.set(qn("w:sz"), str(grosor_octavos))
    borde.set(qn("w:space"), "4")
    borde.set(qn("w:color"), color)
    bdr.append(borde)
    ppr.append(bdr)


def documento_objio(marca="OBJIO LEGAL | MEDICAL LAW", confidencial=False):
    """Documento en blanco con el formato de la casa."""
    doc = Document()
    for s in doc.sections:
        s.left_margin = Cm(3)
        s.right_margin = s.top_margin = s.bottom_margin = Cm(2.5)

        cab = s.header.paragraphs[0]
        cab.alignment = WD_ALIGN_PARAGRAPH.RIGHT
        r = cab.add_run(marca)
        r.font.name, r.font.size, r.font.bold = "Times New Roman", Pt(10), True
        r.font.color.rgb = NAVY
        _filete(cab)

        pie = s.footer.paragraphs[0]
        pie.alignment = WD_ALIGN_PARAGRAPH.CENTER
        pie.add_run("Página ")
        _campo(pie, "PAGE")
        pie.add_run(" de ")
        _campo(pie, "NUMPAGES")
        for r in pie.runs:
            r.font.name, r.font.size = "Times New Roman", Pt(9)
            r.font.color.rgb = GRIS
        if confidencial:
            c = s.footer.add_paragraph()
            c.alignment = WD_ALIGN_PARAGRAPH.CENTER
            rc = c.add_run("CONFIDENCIAL")
            rc.font.name, rc.font.size, rc.font.bold = "Times New Roman", Pt(8), True
            rc.font.color.rgb = ROJO_CONFIDENCIAL

    normal = doc.styles["Normal"]
    normal.font.name = "Times New Roman"
    normal.element.rPr.rFonts.set(qn("w:eastAsia"), "Times New Roman")
    normal.font.size = Pt(12)
    pf = normal.paragraph_format
    pf.alignment = WD_ALIGN_PARAGRAPH.JUSTIFY
    pf.line_spacing_rule = WD_LINE_SPACING.ONE_POINT_FIVE
    pf.space_after = Pt(6)

    for nombre, tam in (("Title", 14), ("Heading 1", 13), ("Heading 2", 12), ("Heading 3", 12)):
        st = doc.styles[nombre]
        st.font.name, st.font.size, st.font.bold = "Times New Roman", Pt(tam), True
        st.font.color.rgb = NAVY
        for a in ("asciiTheme", "hAnsiTheme", "eastAsiaTheme", "cstheme"):
            st.element.rPr.rFonts.attrib.pop(qn(f"w:{a}"), None)  # que el tema no imponga otra fuente
    titulo = doc.styles["Title"]
    titulo.paragraph_format.alignment = WD_ALIGN_PARAGRAPH.CENTER
    ppr = titulo.element.find(qn("w:pPr"))
    if ppr is not None and ppr.find(qn("w:pBdr")) is not None:
        ppr.remove(ppr.find(qn("w:pBdr")))  # sin la raya azul del tema
    return doc


def tabla(doc, encabezados, filas):
    """Tabla con cabecera navy y texto blanco, filas alternas en papel."""
    t = doc.add_table(rows=1, cols=len(encabezados))
    t.style = "Table Grid"
    t.alignment = WD_TABLE_ALIGNMENT.CENTER
    for i, h in enumerate(encabezados):
        celda = t.rows[0].cells[i]
        run = celda.paragraphs[0].add_run(h)
        run.bold, run.font.size = True, Pt(10)
        run.font.color.rgb = RGBColor(0xFF, 0xFF, 0xFF)
        shd = OxmlElement("w:shd")
        shd.set(qn("w:val"), "clear")
        shd.set(qn("w:fill"), NAVY_HEX)
        celda._tc.get_or_add_tcPr().append(shd)
    for n, fila in enumerate(filas, start=1):
        celdas = t.add_row().cells
        for i, valor in enumerate(fila):
            run = celdas[i].paragraphs[0].add_run(str(valor))
            run.font.size = Pt(10)
            if n % 2 == 0:
                shd = OxmlElement("w:shd")
                shd.set(qn("w:val"), "clear")
                shd.set(qn("w:fill"), PAPEL_HEX)
                celdas[i]._tc.get_or_add_tcPr().append(shd)
    return t


def firma(doc, firmante="gilberto", entidad="OBJIO LEGAL | MEDICAL LAW"):
    """Bloque de firma canónico, alineado a la izquierda, sin saltos forzados."""
    doc.add_paragraph()
    lineas = {
        "gilberto": [("Atentamente,", False), ("", False),
                     ("GILBERTO OBJÍO SUBERO", True), ("Abogado", False),
                     ("PhD(c) en Inteligencia Artificial Productividad Empresarial", False),
                     (entidad, False)],
        "clara": [("Atentamente,", False), ("", False),
                  ("Lic. Clara Alcántara", True), ("Abogada", False), (entidad, False)],
    }[firmante]
    for texto, negrita in lineas:
        p = doc.add_paragraph()
        p.alignment = WD_ALIGN_PARAGRAPH.LEFT
        p.paragraph_format.space_after = Pt(0)
        p.paragraph_format.keep_with_next = True
        r = p.add_run(texto)
        r.bold = negrita
```
