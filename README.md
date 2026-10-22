# Visor LINEAS07 · Cruce con el CUR

Visor web para hacer el seguimiento del cruce entre las tablas de afectaciones del Código Urbanístico (Cuadros 5.4, 5.5 a1, 5.5 a2 y 5.5 b) y la capa `lineas07`. Muestra sobre un mapa base:

- **Tramos del CUR** (CUR-001 a CUR-137), coloreados por estado del cruce o por resultado de la revisión.
- **lineas07**, por tipo: particularizada, afectación, apertura, servidumbre, rectificación y otros.
- **Ejes de calle oficiales** y **manzanero CUR 3D**.
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

## Cargar lo que vas estudiando

Cada afectación que estudiás se registra en su ficha del visor. Cada registro queda como un commit en GitHub, así se ve el procedimiento completo a lo largo del tiempo.

1. **Buscá la afectación.**
   - Tramos del cuadro del CUR: pestaña **Tramos CUR**. Podés filtrar por cuadro, estado o calle, o buscar `CUR-0xx` arriba.
   - Afectaciones que no están en los cuadros (por ejemplo la traza de Av. 27 de Febrero): pestaña **Sin respaldo**.
2. **Revisá en el mapa.** Al elegirla, el mapa va al tramo y resalta en rosa las líneas de lineas07 vinculadas. Un clic sobre una línea muestra su TIPO, SMP, OBS, plano y TEXTO.
3. **Completá la revisión** en el panel de abajo:
   - **Resultado**: Correcto, Falta cargar en lineas07, Corregir tramo/extensión, Corregir distancia, Dar de baja en lineas07 o No aplica. En Sin respaldo: Mantener (otra norma), Dar de baja o Revisar.
   - **Norma / fundamento**: por ejemplo «Ley 6.628, art. 1° — elimina el tramo del Cuadro 5.4».
   - **Enlace**: la ficha de normativaba u otra fuente que consultaste.
   - **Observaciones**: qué verificaste, qué falta y qué corregiste.
4. **Tocá «Guardar revisión».**
   - Con el token configurado se publica en el acto, con un commit del tipo «Revisión CUR-026: Falta cargar en lineas07 (tu nombre)».
   - Sin token queda en tu navegador, y el botón «Guardar en GitHub» muestra cuántas faltan publicar.
5. **Si cambia tu conclusión, volvé a guardar.** El resultado anterior no se pierde: pasa al **historial** de la ficha.
6. **Seguí el avance.**
   - Arriba ves «Revisados N/137».
   - En **Capas → Por revisión** el mapa colorea los tramos según su resultado.
   - Con **CSV** bajás la tabla completa para el informe.
7. **Consultá el procedimiento completo en GitHub.** En el repositorio, la pestaña **Commits** muestra cada revisión publicada, con fecha y autor. El historial de `data/revision.json` muestra qué cambió en cada paso.

## Editar tramos y lineas07 desde el visor

Todas las ediciones se guardan en `data/revision.json` junto con las revisiones (con token se publican al instante; sin token quedan en el navegador hasta «Guardar en GitHub»). Cada cambio queda en el historial y se puede deshacer desde la pestaña **Ediciones**.

**Corregir el trazado de un tramo del CUR.** En la ficha del tramo, bloque *Trazado y estado del tramo*:
- **Editar trazado**: arrastrá los vértices; clic en un punto intermedio agrega un vértice, clic derecho (o «Borrar vértice») lo quita. **Extender** agrega vértices al final. Con **Imán** los vértices se pegan a lineas07 y a los ejes.
- **Dibujar de nuevo**: borra el trazado y lo dibujás con clics sobre el mapa.
- Al **Guardar**, el visor recalcula el cruce con lineas07 sobre el trazado nuevo (cobertura por lado, distancia, estado).
- **Volver al automático** descarta el trazado editado.

**Cambiar el estado a mano.** En *Estado manual* elegí, por ejemplo, «Completa» y tocá **Guardar estado**. La ficha muestra igual el estado calculado, y el CSV marca el estado como «(manual)».

**Editar lineas07.** Clic sobre una línea del mapa:
- **Editar atributos**: SMP, sección, manzana, parcela, TIPO, NRO_ORD, OBS, PLANO, TEXTO, etc. «← desde SMP» completa sección, manzana y parcela.
- **Editar geometría**: igual que los tramos.
- **Dar de baja / Reincorporar**: la línea queda punteada y deja de contar en el cruce Es para líneas que ya existen en lineas07: quedan marcadas para darlas de baja en el shapefile.
- **Eliminar línea** (solo en líneas nuevas): la borra por completo, sin dejar rastro en el mapa ni en las descargas. Pide confirmar con un segundo clic.
- **Línea nueva**: desde la ficha de un tramo («Agregar línea en lineas07», con los atributos precargados) o desde la pestaña Ediciones.

**Descargar con los cambios** (pestaña Ediciones), en CABA-PG07:
- **lineas07 (.dxf)**: una polilínea por parte, en capas por tipo (L07_PARTICULARIZADA, L07_AFECTACION, L07_APERTURA, …). Los atributos van como datos extendidos (XDATA, aplicación `LINEAS07`). Opcionalmente, las líneas dadas de baja en la capa L07_BAJA.
- **lineas07 (Shapefile .zip)**: mismo esquema de campos que el original, con la tabla de atributos. Es la opción para llevar los datos a AutoCAD Map 3D como object data (MAPIMPORT).
- **Tramos CUR (.dxf)**: los tramos con su estado, en capas CUR_<estado>.

## Actualizar las capas cuando corrijas lineas07

Cuando des de baja o corrijas líneas en `lineas07.shp`, el visor sigue mostrando la copia del 15/10/2026 hasta que se regeneren los datos:

1. Exportá de nuevo `lineas07.shp`, con el mismo esquema de object data.
2. Pasáselo a Claude y pedile que rehaga el cruce y los datos del visor. Así se recalculan el estado de cada tramo, los vínculos con las líneas y los grupos sin respaldo.
3. Subí al repositorio los archivos nuevos de `data` (**Add file → Upload files**). **No reemplaces `data/revision.json`**: ahí está todo el seguimiento.
4. Esperá uno o dos minutos y recargá el sitio con Ctrl+F5.

Las revisiones quedan asociadas a los ID (CUR-0xx, SR-0xx). Los CUR-0xx no cambian porque salen de los cuadros del CUR. Los SR-0xx pueden renumerarse si cambian las líneas sin respaldo; en ese caso, Claude conserva el seguimiento al regenerarlos.

## Mapas base

- **Argenmap gris** y **Argenmap**: Instituto Geográfico Nacional. Es el mapa por defecto.
- **Mapa claro**: CARTO, sobre datos de OpenStreetMap.
- **OpenStreetMap**.
- **Satélite**: Esri World Imagery.
- **Sin mapa base**: usa solo las capas propias, con partidos vecinos y río de referencia.

Los mapas de USIG (GCBA) no se pueden usar desde GitHub Pages. Su servidor de teselas solo funciona por http, y los navegadores bloquean esas imágenes dentro de un sitio https.

## Datos

Las capas se generaron el 15/10/2026 a partir de:

- `lineas07.shp`
- `ejes_cartografia_gis_2026.shp`
- `manzanero_cur3d_11092026.shp`

Las tres están en CABA-PG07 y se reproyectaron a Web Mercator (EPSG:3857) para superponerlas a los mapas base. El visor muestra igual las coordenadas en CABA-PG07 al pasar el mouse y al hacer clic.

| Archivo | Contenido |
|---|---|
| `data/lineas07.json` | Trazado de afectaciones con su object data |
| `data/lineas07_pg07.json` | lineas07 en CABA-PG07 con todos los atributos (para las descargas) |
| `data/ejes.json` | Ejes de calle oficiales (nombre, tipo, alturas) |
| `data/manzanas.json` | Manzanero (SM, tipo, superficie) |
| `data/ciudad.json`, `data/contexto.json` | Contorno de la Ciudad y partidos vecinos (solo para «Sin mapa base») |
| `data/cruce.json` | Tramos del CUR, estado del cruce y grupos sin respaldo |
| `data/revision.json` | Seguimiento y ediciones (lo escribe el visor) |

Si cambian los shapefiles, hay que regenerar los `.json` de `data` (salvo `revision.json`, que conserva el seguimiento) y subirlos de nuevo.
