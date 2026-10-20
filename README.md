# Visor LINEAS07 · Cruce con el CUR

Visor web para hacer el seguimiento del cruce entre las tablas de afectaciones del Código Urbanístico (Cuadros 5.4, 5.5 a1, 5.5 a2 y 5.5 b) y la capa `lineas07`. Muestra sobre un mapa base:

- **Tramos del CUR** (CUR-001 a CUR-137), coloreados por estado del cruce o por resultado de la revisión.
- **lineas07**, por tipo: particularizada, afectación, apertura, servidumbre, rectificación y otros.
- **Ejes de calle oficiales**, **manzanero CUR 3D** y **secciones catastrales**.
- **Líneas sin respaldo en el CUR**, agrupadas por su TEXTO (SR-001 a SR-018).

Los ID son los mismos de la planilla `Cruce_CUR_vs_lineas07.xlsx`.

## Antes de publicar: visibilidad

En una cuenta gratuita de GitHub, GitHub Pages solo funciona con repositorios **públicos**, así que cualquiera con el enlace puede ver el sitio y descargar los datos (lineas07, observaciones como «EN ESTUDIO - NO ENTREGAR A CUR», SMP, etc.).

- Con GitHub Pro, Team o Enterprise podés publicar desde un repositorio privado, pero **el sitio sigue siendo público** en internet.
- Solo GitHub Enterprise Cloud permite restringir el sitio a miembros de la organización.

Si los datos no pueden ser públicos, consultalo con tu área antes de subirlos.

## Publicar el sitio

1. En GitHub, creá un repositorio nuevo, por ejemplo `visor-lineas07`.
2. En el repositorio, entrá a **Add file → Upload files** y arrastrá el contenido de esta carpeta: `index.html`, `.nojekyll`, `README.md` y la carpeta `data` completa. Confirmá con **Commit changes**.
   - En Windows, `.nojekyll` puede quedar oculto. Si no lo subís, el sitio funciona igual.
3. Entrá a **Settings → Pages**. En *Build and deployment* elegí **Deploy from a branch**, rama **main** y carpeta **/ (root)**, y tocá **Save**.
4. En uno o dos minutos el sitio queda en `https://TU-USUARIO.github.io/visor-lineas07/`.

## Guardar revisiones (token)

Las revisiones se guardan en `data/revision.json` del repositorio. Cada vez que alguien publica, queda un commit con un mensaje como «Revisión CUR-012: Correcto (Junior)». El historial completo queda en GitHub.

Para publicar desde el visor, cada persona necesita un token propio:

1. En GitHub, entrá a **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token**.
2. En *Repository access*, elegí **Only select repositories** y marcá este repositorio.
3. En *Permissions → Repository permissions*, poné **Contents** en **Read and write**. No hace falta ningún otro permiso.
4. Elegí una fecha de vencimiento, generá el token y copialo.
5. En el visor, tocá **⚙** y completá:
   - tu nombre
   - el usuario y el repositorio (se completan solos si abrís el sitio desde github.io)
   - la rama (`main`)
   - el token
6. Tocá **Probar conexión**. Tiene que decir «podés publicar revisiones».

El token queda guardado solo en ese navegador. No lo configures en una computadora compartida, y revocalo desde GitHub cuando no lo uses más.

**Cómo funciona el guardado:**
- **Con token:** al tocar «Guardar revisión» se publica directamente en el repositorio. Si dos personas publican a la vez, el visor combina los cambios.
- **Sin token:** la revisión queda guardada en el navegador y el botón «Guardar en GitHub» muestra cuántas faltan publicar. Desde **⚙ → Descargar revision.json** podés bajar el archivo y subirlo a la carpeta `data` del repositorio con *Upload files*.
- **Ver lo que publicaron otros:** tocá **↻**. Con token lo ves al instante; sin token, cuando GitHub Pages termina de actualizar el sitio (uno o dos minutos).
- **Exportar:** el botón **CSV** baja la tabla completa con las revisiones, separada por punto y coma para abrirla en Excel.

## Mapas base

- **Mapa de la Ciudad**, **Mapa oficial CABA** y **Foto aérea 2021**: servicio de teselas de USIG (Gobierno de la Ciudad de Buenos Aires).
- **OpenStreetMap**.
- **Satélite**: Esri World Imagery.
- **Sin mapa base**: usa solo las capas propias, con partidos vecinos y río de referencia.

Si el servicio de USIG no responde, elegí otro mapa base en la pestaña **Capas**.

## Datos

Las capas se generaron el 15/10/2026 a partir de:

- `lineas07.shp`
- `ejes_cartografia_gis_2026.shp`
- `manzanero_cur3d_11092026.shp`

Las tres están en CABA-PG07 y se reproyectaron a Web Mercator (EPSG:3857) para superponerlas a los mapas base. El visor muestra igual las coordenadas en CABA-PG07 al pasar el mouse y al hacer clic.

| Archivo | Contenido |
|---|---|
| `data/lineas07.json` | Trazado de afectaciones con su object data |
| `data/ejes.json` | Ejes de calle oficiales (nombre, tipo, alturas) |
| `data/manzanas.json` | Manzanero (SM, tipo, superficie) |
| `data/secciones.json`, `data/ciudad.json`, `data/contexto.json` | Secciones catastrales, contorno de la Ciudad y partidos vecinos |
| `data/cruce.json` | Tramos del CUR, estado del cruce y grupos sin respaldo |
| `data/revision.json` | Seguimiento (lo escribe el visor) |

Si cambian los shapefiles, hay que regenerar los `.json` de `data` (salvo `revision.json`, que conserva el seguimiento) y subirlos de nuevo.
