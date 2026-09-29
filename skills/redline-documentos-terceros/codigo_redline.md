# Código del redline — para la ejecución de código de Claude

Probado con python-docx 1.2 (que trae comentarios de Word nativos, `doc.add_comment`). El archivo resultante se abrió en Word con todos los comentarios visibles, incluidos los que ya traía la contraparte.

Si el entorno tiene una versión anterior: `pip install -U "python-docx>=1.2"`. Si no se puede instalar, usar la alternativa manual de la skill.

## Flujo de uso

```python
import shutil
from docx import Document

ORIGINAL = "Contrato de servicios.docx"
REVISADO = "Contrato de servicios — Rev. OBJIO LEGAL.docx"

print(inventario(ORIGINAL))            # 1. comentarios previos y control de cambios
shutil.copy(ORIGINAL, REVISADO)        # 2. se trabaja sobre una copia; el original no se toca
doc = Document(REVISADO)

p = buscar(doc, "treinta (30) días")   # 3. cada cambio con su porqué
reemplazar(doc, p, "treinta (30) días", "noventa (90) días calendario",
           "El plazo de treinta días no cubre el ciclo de facturación de la cliente; "
           "noventa días calendario evita el incumplimiento involuntario desde el segundo mes.")

p = buscar(doc, "DÉCIMA:")
insertar_parrafo_despues(doc, p, "DÉCIMA PRIMERA: CONFIDENCIALIDAD. …",
           "Se añade: el contrato da acceso a datos de pacientes y no tenía obligación de "
           "confidencialidad; sin ella la cliente responde frente a los titulares de los datos.")

comentar_parrafo(doc, buscar(doc, "jurisdicción"),
           "Sin cambio de texto: se recomienda pactar mediación previa. Decisión de negocio de la cliente.")

doc.save(REVISADO)
print(verificar(ORIGINAL, REVISADO))   # 4. debe imprimir []  (lista vacía = sin fallos)
```

Después: convertir a PDF (`soffice --headless --convert-to pdf "<archivo>"`) si se remite en PDF, y extraer de nuevo `inventario(REVISADO)` para comprobar que están todos los comentarios, los propios y los ajenos.

## Qué hace cada función

| Función | Para qué |
|---|---|
| `inventario(ruta)` | Lista los comentarios que ya trae el documento (autor y texto) y cuenta inserciones y supresiones con control de cambios. Se ejecuta **antes** de opinar. |
| `reemplazar(doc, parrafo, viejo, nuevo, porque)` | Sustituye un fragmento dentro de un párrafo, resalta el texto nuevo y le ancla el comentario. No reconstruye el párrafo: conserva los comentarios y marcas que ya existían. |
| `insertar_parrafo_despues(doc, parrafo, texto, porque)` | Añade una cláusula o sección nueva con el mismo formato de párrafo, resaltada y comentada. |
| `comentar_parrafo(doc, parrafo, texto)` | Observación sin cambiar el texto, o respuesta a un comentario de la contraparte («En respuesta a …: …»). |
| `buscar(doc, fragmento)` | Encuentra el párrafo, también dentro de tablas. |
| `verificar(original, revisado)` | Dos pruebas mecánicas: todo comentario tiene su referencia, y todo párrafo modificado o nuevo tiene resaltado. Devuelve la lista de fallos. |

Para la segunda ronda de un mismo documento, cambiar `COLOR` a `WD_COLOR_INDEX.BRIGHT_GREEN`. Para comentar en nombre del Lic. Objío, cambiar `AUTOR` e `INICIALES`.

Límite conocido: `reemplazar` trabaja dentro de un párrafo. Un cambio que abarca varios párrafos se hace reemplazando en cada uno o insertando el párrafo nuevo y comentando la supresión del anterior.

## Código

```python
import copy, difflib, re, zipfile
from docx.text.run import Run
from docx.text.paragraph import Paragraph
from docx import Document
from docx.enum.text import WD_COLOR_INDEX
from docx.oxml.ns import qn

AUTOR = "Lic. Clara Alcántara — OBJIO LEGAL"   # o "Lic. Gilberto Objío Subero — OBJIO LEGAL"
INICIALES = "CA"                               # o "GOS"
COLOR = WD_COLOR_INDEX.YELLOW                  # segunda ronda: WD_COLOR_INDEX.BRIGHT_GREEN


def inventario(ruta):
    """Lo que el texto no muestra: comentarios previos y control de cambios."""
    z = zipfile.ZipFile(ruta)
    xml = z.read("word/document.xml").decode("utf-8")
    com = []
    if "word/comments.xml" in z.namelist():
        cx = z.read("word/comments.xml").decode("utf-8")
        for autor, cuerpo in re.findall(r'<w:comment [^>]*w:author="([^"]*)"[^>]*>(.*?)</w:comment>', cx, re.S):
            com.append((autor, "".join(re.findall(r"<w:t[^>]*>([^<]*)</w:t>", cuerpo))))
    return {"comentarios": com,
            "inserciones_rastreadas": xml.count("<w:ins "),
            "supresiones_rastreadas": xml.count("<w:del ")}


def _resaltar(run):
    run.font.highlight_color = COLOR


def comentar(doc, runs, texto):
    """Comentario de Word real, anclado a uno o varios runs del mismo párrafo."""
    return doc.add_comment(runs, text=texto, author=AUTOR, initials=INICIALES)


def reemplazar(doc, parrafo, viejo, nuevo, porque):
    """Sustituye `viejo` por `nuevo` dentro del párrafo sin destruir los runs
    ajenos (comentarios de la contraparte, notas, campos). Resalta y comenta."""
    runs = [r for r in parrafo.runs if r.text]
    texto = "".join(r.text for r in runs)
    i = texto.find(viejo)
    if i < 0:
        raise ValueError(f"No encontré «{viejo}» en: {texto[:80]}")
    fin, pos, primero, run_nuevo = i + len(viejo), 0, True, None
    for r in runs:
        a, b = pos, pos + len(r.text)
        pos = b
        if b <= i or a >= fin:
            continue
        antes, despues = r.text[: max(i - a, 0)], r.text[max(fin - a, 0):] if fin < b else ""
        if primero:
            r.text = antes
            e = copy.deepcopy(r._r)
            r._r.addnext(e)
            run_nuevo = Run(e, parrafo)
            run_nuevo.text = nuevo
            _resaltar(run_nuevo)
            if despues:
                e2 = copy.deepcopy(r._r)
                e.addnext(e2)
                Run(e2, parrafo).text = despues
            primero = False
        else:
            r.text = despues
    for r in runs:  # limpia runs vaciados que solo tenían texto
        if not r.text and all(h.tag in (qn("w:rPr"), qn("w:t")) for h in r._r):
            r._r.getparent().remove(r._r)
    comentar(doc, run_nuevo, porque)
    return run_nuevo


def insertar_parrafo_despues(doc, parrafo, texto, porque):
    """Párrafo nuevo (cláusula o sección añadida), resaltado y comentado."""
    nuevo = copy.deepcopy(parrafo._p)
    for hijo in list(nuevo):
        if hijo.tag != qn("w:pPr"):
            nuevo.remove(hijo)
    parrafo._p.addnext(nuevo)
    p = Paragraph(nuevo, parrafo._parent)
    run = p.add_run(texto)
    _resaltar(run)
    comentar(doc, run, porque)
    return p


def verificar(ruta_original, ruta_revisada):
    """Dos pruebas mecánicas antes de entregar. Devuelve la lista de fallos."""
    fallos = []
    z = zipfile.ZipFile(ruta_revisada)
    xml = z.read("word/document.xml").decode("utf-8")
    inicios = set(re.findall(r'<w:commentRangeStart w:id="(\d+)"', xml))
    refs = set(re.findall(r'<w:commentReference w:id="(\d+)"', xml))
    if inicios - refs:
        fallos.append(f"Comentarios sin referencia: {sorted(inicios - refs)}")
    orig = [p.text for p in Document(ruta_original).paragraphs]
    rev = Document(ruta_revisada).paragraphs
    sm = difflib.SequenceMatcher(a=orig, b=[p.text for p in rev])
    for op, _, _, j1, j2 in sm.get_opcodes():
        if op in ("replace", "insert"):
            for p in rev[j1:j2]:
                if p.text.strip() and not any(r.font.highlight_color for r in p.runs):
                    fallos.append(f"Cambio sin resaltar: {p.text[:70]}")
    return fallos


def todos_los_parrafos(doc):
    """Párrafos del cuerpo y de las tablas (doc.paragraphs no entra en tablas)."""
    yield from doc.paragraphs
    for t in doc.tables:
        for fila in t.rows:
            for celda in fila.cells:
                yield from celda.paragraphs


def buscar(doc, fragmento):
    for p in todos_los_parrafos(doc):
        if fragmento in p.text:
            return p
    raise ValueError(f"No encontré «{fragmento}»")


def comentar_parrafo(doc, parrafo, texto):
    """Comentario sobre un párrafo entero sin cambiar su texto (observación o respuesta)."""
    runs = [r for r in parrafo.runs if r.text]
    return comentar(doc, [runs[0], runs[-1]] if len(runs) > 1 else runs[0], texto)
```
