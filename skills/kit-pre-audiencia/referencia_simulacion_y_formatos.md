# Referencia · simulación, formatos y control de calidad del kit pre-audiencia

## 1. Puntaje antes y después (10 dimensiones)

Mide al empezar y al terminar; cada dimensión vale 0 (no está), 0,5 (parcial) o 1 (completa). El producto no se entrega por debajo de 8 de 10.

| # | Dimensión |
|---|---|
| 1 | Identidad de partes, tribunal y audiencia verificada contra documentos |
| 2 | Inventarios listados y piezas catalogadas con referencia exacta |
| 3 | Informes clave leídos completos y sintetizados |
| 4 | Cronología procesal y fáctica mapeada |
| 5 | Tesis nucleares definidas |
| 6 | Base de interrogatorios v2 destilada |
| 7 | Simulación adversarial realizada (≥ 2 rondas) |
| 8 | Soporte de piezas resaltado en 4 capas |
| 9 | Guion integrado armado |
| 10 | Producto cerrado: nada pendiente que pudiera haberse resuelto antes de entregar |

Reporta a Clara el puntaje antes → después y lo que falta, si falta algo.

## 2. Protocolo de simulación adversarial

**Personajes** (los interpretas tú, uno por turno, marcando quién habla):

- **Interrogador:** usa solo la base v2; no improvisa preguntas que no estén en ella, salvo la repregunta a una evasiva.
- **Testigo:** cada parte o testigo adverso, con su perfil de evasión más plausible. Perfiles típicos:
  - *El técnico:* convierte cada pregunta en una exposición doctrinal para diluir el foco.
  - *El que no recuerda:* «no recuerdo», «habría que ver el expediente».
  - *El que traslada la responsabilidad:* «eso le correspondía a otro servicio / a otro empleado».
  - *El que discute el documento:* «esa no es mi firma», «ese informe está mal hecho».
  - *El que responde otra pregunta:* contesta lo que le conviene y no lo que se le preguntó.
- **Juez:** con acceso pleno al expediente; interrumpe, pide aclaraciones, interpela al testigo con un documento, rechaza preguntas sugestivas en el directo o impertinentes, y ordena hacer constar en acta.

**Ciclo por ronda:**

1. Ronda completa por bloques temáticos (un bloque = una tesis o un grupo de tesis).
2. Puntaje de cada bloque con la escala de 1 a 5 estrellas (hasta 30 puntos por bloque si se usan 6 preguntas-objetivo).
3. Auditoría: qué evasivas no estaban previstas, qué preguntas abrieron la puerta al testigo, qué pieza faltó.
4. Refuerzo: repreguntas para cada evasiva, reorden de la secuencia, nueva pieza o nueva cita textual.
5. Repetir hasta ≥ 25/30 por bloque o 5 rondas.

**Salida de la simulación:**

- Tabla de puntajes por ronda y por bloque.
- Las **3 advertencias críticas** para la sala real (la evasiva más peligrosa de cada testigo y cómo neutralizarla).
- El **guion ganador**:
  - Apertura de 90 segundos (qué se va a demostrar y con qué piezas).
  - Interrogatorios en secuencia, por actor, con la pieza de cada pregunta.
  - Repreguntas preparadas para las evasivas previstas.
  - Conclusiones que se pedirá hacer constar en acta.
  - Cierre con pedimentos.

## 3. Página separadora (antes de cada pieza física)

Una página A4 o carta por pieza, con estos campos:

| Campo | Contenido |
|---|---|
| Encabezado | Título del guion · audiencia (fecha y hora) · número de expediente · tribunal |
| Banda | `PIEZA NN · Bloque temático` |
| Actor | Interrogador → testigo |
| Ubicación en el expediente | Inventario (referencia y fecha de depósito) · núm. de pieza · página interna |
| Momento de uso | Número de pregunta en la secuencia y contexto |
| Pregunta exacta | En recuadro, en cursiva, para leer literal |
| Admisión o contradicción buscada | Lo que se quiere que quede en acta |
| Tesis nuclear | T# vinculada |
| Pie | Paginación |

## 4. Resaltado en cuatro capas (legible en color y en B/N)

Cada pasaje a exhibir lleva:

1. Resaltado amarillo nativo con opacidad de alrededor de 0,5 (se ve en color).
2. Recuadro negro de 1,4 pt alrededor del pasaje (se ve siempre).
3. Barra vertical negra de 4 pt en el margen izquierdo, a la altura del pasaje (se ve siempre).
4. Triángulo negro ▶ que apunta al inicio del pasaje (se ve siempre).

**Cómo hacerlo en Claude web:**

- Si la ejecución de código está disponible y Clara subió el PDF, usa PyMuPDF (`fitz`): localiza el texto con `page.search_for("frase exacta")` (en PDF escaneado sin capa de texto, ubica el pasaje leyendo la imagen y estima el rectángulo, o pide a Clara el número de página y la frase) y aplica las cuatro capas:

```python
import fitz  # PyMuPDF

def resaltar_4_capas(page, rect):
    a = page.add_highlight_annot(rect)            # 1. amarillo
    a.set_colors(stroke=(1, 0.92, 0.23)); a.set_opacity(0.5); a.update()
    page.draw_rect(rect, color=(0, 0, 0), width=1.4)                  # 2. recuadro
    barra = fitz.Rect(rect.x0 - 12, rect.y0, rect.x0 - 8, rect.y1)
    page.draw_rect(barra, color=(0, 0, 0), fill=(0, 0, 0))            # 3. barra
    y = (rect.y0 + rect.y1) / 2
    tri = [fitz.Point(rect.x0 - 20, y - 4), fitz.Point(rect.x0 - 20, y + 4),
           fitz.Point(rect.x0 - 14, y), fitz.Point(rect.x0 - 20, y - 4)]
    page.draw_polyline(tri, color=(0, 0, 0), fill=(0, 0, 0))          # 4. marcador

doc = fitz.open("pieza.pdf")
for r in doc[PAGINA].search_for("FRASE EXACTA"):
    resaltar_4_capas(doc[PAGINA], r)
doc.save("pieza_resaltada.pdf")
```

- Si no hay ejecución de código, entrega a Clara la lista de pasajes (pieza, página, frase exacta) y las instrucciones para marcarlos en Acrobat o en el lector de PDF: resaltador amarillo + herramienta de rectángulo en negro de 1,4 pt + línea vertical gruesa en el margen + flecha o triángulo.
- Incluye solo las páginas que se van a exhibir, no el documento entero.

## 5. Estructura del documento maestro

1. Portada: título, tribunal, número de expediente, fecha y hora de la audiencia, «Uso interno · OBJIO LEGAL».
2. Ficha técnica y tesis nucleares (T1…Tn).
3. Apertura de 90 segundos e interrogatorio directo de los propios.
4. Por cada parte o testigo adverso:
   - Página resumen: rol, debilidades, qué admitirá, qué negará, estrategia.
   - Por cada pieza: página separadora + pieza resaltada.
5. Cierre: conclusiones que se pedirá hacer constar en acta y advertencias críticas.
6. Apéndice: índice de piezas (tabla con inventario, número, página, pregunta y tesis).

Control final: cada pieza con referencia exacta; cada pregunta con su admisión graduada; cada bloque con su tesis.

## 6. Después de la audiencia (ciclo de mejora)

Cuando Clara vuelva de sala, ofrece cerrar el ciclo con lo que cuente o con el acta:

- **Post mortem:** qué funcionó, qué falló, en qué se equivocó la simulación frente a la realidad.
- **Biblioteca de preguntas-contraste:** guarda las preguntas que produjeron admisión, etiquetadas por tesis, materia y tipo de testigo, para la próxima audiencia análoga.
- **Biblioteca de evasivas:** cada evasiva nueva con su repregunta canónica, útil si el mismo testigo vuelve a declarar.
- **Lecciones:** uno a tres patrones nuevos que valga la pena incorporar a este kit.

Como Claude web no guarda archivos entre conversaciones, entrega estas bibliotecas como un documento que Clara pueda conservar y volver a subir.

## 7. Casos de uso típicos

1. Comparecencia personal de las partes en materia civil.
2. Comparecencia personal en materia laboral (trabajador y empleador).
3. Informativo testimonial con testigos de la contraparte.
4. Juicio de fondo penal (interrogatorio a testigos, peritos o, cuando proceda, declaración del imputado).
5. Audiencias de familia con comparecencia de los padres.
6. Responsabilidad médica: interrogatorio a profesionales de la salud o a representantes del centro demandado, con historia clínica e informes oficiales como piezas.
7. Cualquier audiencia en la que se exhiban documentos del expediente para obtener admisiones.
