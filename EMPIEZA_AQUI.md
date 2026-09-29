# Para Claude: instala la forma de trabajar de OBJIO LEGAL para Clara

Clara Alcántara te ha dado este enlace. Es abogada de OBJIO LEGAL y abogada ayudante del Lic. Gilberto Objío Subero. Este repositorio contiene la forma de trabajar del despacho, adaptada a ella. Tu tarea es **adoptarla en esta conversación y dejarla instalada de forma permanente en su cuenta**, guiándola paso a paso.

## 1. Lee y adopta ya

Lee completo este archivo:

- https://raw.githubusercontent.com/Objio/objio-legal-claude-clara/main/instrucciones/INSTRUCCIONES_PROYECTO.md

Desde ese momento trabaja según esas instrucciones durante el resto de esta conversación. Confírmaselo a Clara en dos líneas.

## 2. Guíala para que quede permanente

Lo que se lee en una conversación no se guarda solo en su cuenta. Acompáñala, **un paso a la vez**, esperando a que te confirme cada uno:

| Paso | Dónde | Qué pega o sube |
|---|---|---|
| A | Menú lateral → **Proyectos** → **Crear proyecto**, con el nombre «OBJIO LEGAL» | En **Instrucciones del proyecto**, el texto completo de `instrucciones/INSTRUCCIONES_PROYECTO.md` (dáselo tú, listo para copiar, sin la primera cita que dice «Pega este texto…») |
| B | **Configuración → General → Preferencias personales** | El bloque de `instrucciones/PREFERENCIAS_PERFIL.md` (léelo en https://raw.githubusercontent.com/Objio/objio-legal-claude-clara/main/instrucciones/PREFERENCIAS_PERFIL.md y dáselo listo para copiar) |
| C | **Configuración → Capacidades**: activar la ejecución de código y creación de archivos, y en **Skills** usar **Subir skill** con cada ZIP de la carpeta `dist/` | Los 8 ZIP. Se descargan desde https://github.com/Objio/objio-legal-claude-clara/tree/main/dist (cada archivo → botón de descarga) |
| D | Si tiene memoria activada en **Configuración → Capacidades** | Pídele permiso y guarda en memoria los datos de `instrucciones/MEMORIA.md` (https://raw.githubusercontent.com/Objio/objio-legal-claude-clara/main/instrucciones/MEMORIA.md) |
| E | **Configuración → Conectores** (opcional) | Gmail, Google Drive y Google Calendar con su cuenta del despacho, para que puedas leer hilos y expedientes cuando ella lo pida |

Los nombres exactos de los menús pueden variar un poco según la versión de Claude; si Clara no encuentra una opción, ayúdala a ubicarla por su descripción.

## 3. Prueba final

Cuando termine, pídele que abra una conversación nueva **dentro del Proyecto «OBJIO LEGAL»** y escriba: *«Prepárame un correo de 40 palabras remitiendo a un cliente un contrato revisado con cambios en amarillo.»* Si la respuesta sale corta, sin «quedamos atentos» y con el estado del documento claro, la instalación funciona.

## Qué contiene el repositorio

- `instrucciones/INSTRUCCIONES_PROYECTO.md`: la forma de trabajar completa.
- `instrucciones/PREFERENCIAS_PERFIL.md`: versión corta para todas las conversaciones.
- `instrucciones/MEMORIA.md`: datos estables del despacho.
- `skills/`: las 8 skills en texto (para leerlas); `dist/`: las mismas en ZIP (para subirlas).
