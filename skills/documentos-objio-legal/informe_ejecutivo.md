# Informe ejecutivo premium (A4, estética corporativa)

Para documentos cara al cliente que deben transmitir autoridad antes de que se lea una palabra: propuestas de servicios, briefings normativos, informes estratégicos, memorandos ejecutivos, brochure del despacho. Se construye en HTML con diseño de página A4 y se convierte a PDF.

> Norte: el destinatario abre el PDF y, antes de leer, ya quiere trabajar con OBJIO LEGAL. Belleza, verdad verificable y marca, en partes iguales.

## 1. Antes de escribir: la matriz

| Pregunta | Qué se aclara |
|---|---|
| **Qué** | Encargo, alcance, entregables, precio, plazo |
| **Quién** | Destinatario y tipo de relación con el despacho (cliente, prospecto, relacionado) |
| **Cómo** | Pago único, iguala mensual, sin precio (informativo) |
| **Cuándo** | Fechas críticas: vigencia de la oferta, entregas, fechas normativas |

Si falta algo, se pregunta **una sola vez** a Clara, agrupando todas las preguntas. Nunca se inventa la relación.

## 2. Cero invención (la regla que más documentos ha salvado)

| Dato | Solo si… | Si no… |
|---|---|---|
| Clientes que se nombran como referencia | Clara confirma en la conversación que son clientes y que pueden nombrarse | No se nombra ninguno. Nunca descriptores genéricos disfrazados de cliente («un centro líder en…») |
| Cifras de trayectoria (años, casos, clientes) | Clara las aporta y constan | Lenguaje cualitativo, sin números |
| Personas del equipo | Personas reales (el Lic. Gilberto Objío Subero, la Lic. Clara Alcántara y quien Clara indique) | No se añaden nombres |
| Citas de normas | Texto literal leído en la fuente primaria, con número, fecha y artículo exactos | No se cita |
| Citas atribuidas al Lic. Objío | Extracto literal de una publicación suya que Clara aporta o que se consulta en objiolegal.com | No se cita |

Además: todo nombre de empresa u organización que se mencione como cliente o aliado se cruza con la lista de contrapartes del despacho (Clara la conoce; si hay duda, se pregunta antes). Un nombre que resulta ser contraparte arruina el documento entero.

En documentos de difusión amplia (briefing a relacionados) no se nombran clientes ni asuntos, nunca.

## 3. Arquitectura según el caso de uso

```
¿El documento propone un servicio con precio?
├── Sí → ¿Puntual o continuo?
│        ├── Puntual  → A. Propuesta comercial
│        └── Continuo → A con bloque de iguala en lugar de pago único
└── No → ¿Para qué es?
         ├── Informar una novedad normativa a muchos → B. Briefing normativo
         ├── Sustentar una decisión (consejo, auditoría) → C. Informe estratégico
         ├── Responder una consulta jurídica concreta → D. Opinión jurídica corporativa
         ├── Algo breve y urgente (2 a 4 páginas) → E. Memorando ejecutivo
         └── Presentar el despacho sin destinatario concreto → F. Brochure
```

| Caso | Páginas | Secciones | Prohibido |
|---|---|---|---|
| A. Propuesta comercial | 10–11 | Portada · Quiénes somos · Referencias (solo confirmadas) · Servicios · Propuesta específica para el cliente · Entregables y precio · Urgencia normativa (si la hay) · Iguala (si aplica) · Cronograma · Equipo · Próximos pasos y contacto | — |
| B. Briefing normativo | 6–8 | Portada «Para nuestros relacionados» · Qué pasó (norma y cronología) · Qué cambia · Lista de obligaciones · Hoja de ruta sin precios · Quiénes somos (breve) · Contacto | Precio, clientes, propuesta específica |
| C. Informe estratégico | 6–10 | Portada · Resumen ejecutivo y hallazgos · Análisis por eje · Riesgos · Conclusiones y recomendaciones priorizadas | Precio, referencias de clientes, llamado comercial |
| D. Opinión jurídica corporativa | 5–8 | Portada · Hechos · Normas aplicables · Análisis · Conclusión · Firma | Clientes, precio, marketing |
| E. Memorando ejecutivo | 2–4 | Portada compacta · 1–2 páginas de sustancia · Próximos pasos y contacto | Todo lo demás |
| F. Brochure | 6–8 | Portada · Quiénes somos · Diferenciales · Servicios · Referencias confirmadas · Contacto | Precio, proyecto específico |

La estética es la misma en los seis casos; cambia la arquitectura. Si el encargo mezcla casos, manda el principal y se añade como mucho una página del secundario. En el cierre se informa a Clara qué caso de uso se aplicó.

## 4. Especificación visual

**Página:** A4 vertical (210 × 297 mm), `@page { size: A4 portrait; margin: 0; }`, un bloque conceptual por página, salto de página entre secciones, fondos preservados al imprimir (`print-color-adjust: exact`).

**Tipografía:** Playfair Display (títulos, portada, números decorativos) e Inter (cuerpo, tablas, rótulos), de Google Fonts, con respaldo `Georgia, serif` e `Arial, sans-serif` si el entorno no tiene internet. Tamaños: nombre del despacho en portada 30 pt · título de sección 22 pt · frase de marca 13 pt cursiva · cuerpo 9–10 pt · rótulos 7,5–8 pt en mayúsculas espaciadas.

**Colores** (los de la marca; el oro solo como filete o línea fina):

```css
:root {
  --navy: #1B365D;        /* portada, titulares, bandas oscuras */
  --azul: #2F5FB0;        /* segundo plano; acento sobre fondo claro */
  --azul-claro: #8FB4E3;  /* acento sobre fondo oscuro */
  --gris-1: #546879;      /* texto secundario */
  --gris-2: #798CA0;
  --gris-3: #D3DDEA;      /* bordes finos */
  --papel: #EEF2F7;       /* fondos suaves */
  --papel-calido: #F7F5F0;
  --oro: #C9A962;         /* SOLO filetes y líneas divisorias de 1-2 pt */
  --confidencial: #8B0000;/* urgencias y plazos */
  --blanco: #FFFFFF;
}
```

Reglas de color: el oro nunca es texto, relleno ni borde grueso de tarjeta; sirve para el filete bajo la marca, la línea divisoria bajo un título y el contorno fino del monograma. Los números decorativos grandes van en azul con opacidad baja. Sobre fondo oscuro, rótulos en `--azul-claro`; sobre fondo claro, en `--azul`. Ningún texto del color de su fondo.

**Componentes:**

| Componente | Uso | Diseño |
|---|---|---|
| Portada | Página 1 | Degradado navy · monograma circular «OL» con contorno oro fino · «OBJIO LEGAL» en Playfair 30 pt · rótulo «Medical Law» espaciado · filete oro de 70 × 2 px · tipo y título del documento · destinatario en un recuadro de línea fina · fecha y «Documento confidencial» al pie |
| Encabezado de página | Páginas interiores | Marca a la izquierda, destinatario y año a la derecha, línea navy de 2 px debajo |
| Frase de marca | Apertura de sección | Playfair cursiva 13 pt con línea vertical fina a la izquierda |
| Número de sección | Decoración | Playfair 64 pt, azul con opacidad 0,12, arriba a la derecha |
| Tarjetas de diferenciales (3) | Quiénes somos | Fondo papel, línea superior fina, marcador tipográfico «— 01» |
| Servicios (6) | Portafolio | Cuadrícula 2 × 3, línea vertical izquierda, marcador «— I» |
| Lista de dimensiones | Pasos o ejes del proyecto | Fondo papel, número romano grande, título y texto |
| Bloque de entregables | Precio | Fondo navy, entregables en 2 × 2, precio en Playfair 28 pt en blanco o azul claro |
| Bloque normativo | Urgencia de una norma | Fondo papel, línea izquierda `--confidencial`, título, cita literal con su fuente, «qué cambia / qué exige», línea de tiempo con el hito activo en `--confidencial` |
| Iguala | Servicio continuo | Lista de lo incluido y tarjeta navy con el monto mensual |
| Cronograma | Plan por semanas | Filas con barras horizontales en azul |
| Equipo | Personas asignadas | Foto circular (solo si Clara la adjunta) y rol |
| Próximos pasos (3) | Cierre | Tres tarjetas numeradas |
| Contacto | Última página | Fondo navy, domicilio profesional y datos institucionales |

Iconografía: ninguna. Ni emojis, ni entidades HTML de emoji, ni iconos web. Solo geometría, líneas finas y tipografía.

**Bloque de contacto** (datos institucionales permitidos):
- OBJIO LEGAL · Medical Law
- Av. Sarasota esq. El Embajador, Condominio Jardines del Embajador, Edif. 15, Suite 247, Bella Vista, Santo Domingo, D.N.
- Oficina: (809) 532-7773 · objiolegal.com
- Firmante y su correo profesional, solo con los datos que Clara indique en la conversación.

## 5. Producción en Claude

1. Escribir el HTML completo (una `<div class="page">` por página) directamente, sin delegar la redacción. Quien escribe es quien verifica.
2. Mostrar el HTML como vista previa si el entorno lo permite y revisarlo.
3. Convertir a PDF con la herramienta de ejecución de código (por ejemplo, WeasyPrint o Chromium sin interfaz si están disponibles), en A4, sin márgenes y con fondos. Si no es posible, entregar el HTML e indicar a Clara: abrirlo en el navegador, «Imprimir > Guardar como PDF», tamaño A4, márgenes «Ninguno», «Gráficos de fondo» activado.
4. Abrir el PDF generado y comprobar: número de páginas (sin páginas en blanco al final), tildes, texto seleccionable, que ninguna sección se corte a media página.

## 6. Lista de control antes de entregar

- [ ] Cada cliente o persona nombrada está confirmada por Clara en la conversación y no es contraparte.
- [ ] Ninguna cifra de trayectoria sin fuente.
- [ ] Cada cita normativa es literal y se leyó en la fuente primaria vigente.
- [ ] Cero emojis y cero iconos.
- [ ] Cero caracteres corruptos; `<meta charset="UTF-8">` presente.
- [ ] Cero marcadores sin completar (`[CLIENTE]`, `{{ }}`, `XXX`).
- [ ] Oro solo en filetes y líneas finas.
- [ ] Datos institucionales exactos (domicilio, oficina, web).
- [ ] PDF abierto y revisado.
- [ ] Pasó por `verificacion-antes-de-enviar`.
- [ ] Si se remite: correo breve redactado, con destinatarios indicados por Clara.

Si cualquier casilla falla, el documento no está cerrado.
