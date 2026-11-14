# Braylin Jiménez · IA y datos para seguros y farmacia

Portafolio profesional de Braylin A. Jiménez Reynoso, economista y científico de datos en Santo Domingo, República Dominicana. Casos de seguros, farmacia y salud, todos con código abierto.

**Sitio:** <https://braylinjr.github.io/>

## Estructura

| Ruta | Contenido |
|---|---|
| `index.html` | Página completa (HTML, CSS y JavaScript propios en un solo archivo, sin librerías ni compilación) |
| `assets/` | Imágenes, videos, CV en PDF e imagen para compartir (`og.png`, 1200×630) |
| `404.html` | Página de error con el estilo del sitio y botón "Volver al inicio" |
| `robots.txt`, `sitemap.xml` | Indicaciones para buscadores |
| `.nojekyll` | Indica a GitHub Pages que publique los archivos tal cual |

Orden de la página: portada y cifras → Pulso del sector → 01 Casos → 02 Publicaciones → 03 Conferencias → 04 Docencia → 05 Reconocimientos → 06 Trayectoria → 07 Formación → 08 Cómo trabajo → Contacto.

## Agregar una publicación (paper o informe)

1. **Limpia los metadatos** del PDF (autor, programa, fechas, XMP) y deja solo título, autor y palabras clave.
2. **Archivos** en `assets/publicaciones/`, con nombre `apellido-año-tema-corto`:
   - `….pdf` — el documento.
   - `….jpg` — portada: la mitad superior de la primera página, unos 490 × 615 px.
3. **La tarjeta** — copia un `<article class="paper">` completo dentro de `<div class="papers">` (el más nuevo va primero) y cambia:
   - `id="pub-…"` (sirve como enlace directo: `/#pub-…`).
   - Tipo, fecha, páginas e idioma en `.paper-meta`; título, autores, resumen, tres cifras (`.kpis`) y etiquetas.
   - Los enlaces al PDF y a la portada.
   - Los ids de la cita: `aria-controls`/`id` de `.cite-box` y los `data-copy`/`id` de APA y BibTeX deben ser únicos.
   - Opcional: `<div class="new-tag" data-pub="AAAA-MM-DD">NUEVO</div>` (desaparece sola a los 60 días).
   - Cuando tenga DOI, quita `hidden` del botón DOI, pon el enlace `https://doi.org/…` y agrega el DOI a las citas.
4. **Inglés** — en `<script id="i18n-en">`: los textos nuevos en `t` y el resumen en `h` (marcado con `data-i18n="pub-…-abs"`).
5. **Buscadores** — agrega una entrada `ScholarlyArticle` al bloque JSON-LD de publicaciones en `<head>` y la URL del PDF a `sitemap.xml`.

El efecto morado (borde, brillo y el destello que cruza la tarjeta) se aplica solo a toda tarjeta `.paper`; no hay que tocar CSS ni JavaScript.

## Agregar un caso

Cada caso tiene tres piezas en `index.html`:

1. **La tarjeta** — un `<article class="card">` dentro de `<div class="pgrid">`, con:
   - `data-areas` con uno o más filtros: `seguros`, `farmacia`, `economia`, `software` (los conteos de los filtros se calculan solos).
   - `data-open="clave"` en la portada (`.card-media`, con `role="button"`, `tabindex="0"` y `aria-label="Ver caso: …"`) y en el botón "Ver caso completo".
   - La **etiqueta de origen** dentro de `.tags`: `<span class="origin">…Datos públicos | Datos sintéticos | Datos de ejemplo | Software publicado</span>`. Ninguna cifra sintética debe aparecer sin esta etiqueta.
   - La fecha de publicación en el pie: `<time class="pub" datetime="2026-10">Oct 2026</time>`.
   - Opcional: `<div class="new-tag" data-pub="AAAA-MM-DD">NUEVO</div>`; la insignia desaparece sola a los 60 días.
2. **El detalle** — una entrada con la misma `clave` en el bloque `<script id="proj-data">` (JSON): `title`, `eyebrow`, `tags`, `lead`, `sections`, `stack`, `links`, y:
   - `"origen": {"label": "Datos sintéticos", "base": "De dónde salen"}` (se muestra en la ventana, debajo de las etiquetas).
   - `"sintetico": true` si los datos son sintéticos: agrega la nota "Los datos son sintéticos y replican un problema real de seguros…".
3. **El orden** — la ventana del caso navega con "Caso anterior / siguiente" en el mismo orden de las tarjetas visibles (más las tarjetas pequeñas de "Más análisis").

Enlaces útiles: `/#caso-lince` abre un caso directamente; `/?f=seguros` abre la página con un filtro aplicado.

## Idiomas (español / inglés)

El botón **ES / EN** de la barra cambia el idioma sin recargar. El español vive en el HTML (es lo que ven los buscadores y quien no tiene JavaScript); el inglés sale de dos bloques JSON en `index.html`:

- `<script id="i18n-en">` — `t`: texto exacto en español → inglés (sirve para textos, `aria-label`, `title` y `alt`); `h`: bloques con formato interno (negritas, cursivas) marcados en el HTML con `data-i18n="clave"`.
- `<script id="proj-data-en">` — el detalle de los casos, con las mismas claves y estructura que `proj-data`.

Idioma inicial: `?lang=en` o `?lang=es` en el enlace → la última elección (se guarda en el navegador) → el idioma del navegador. Al **cambiar un texto en español hay que cambiar también su entrada en `t`** (la clave es el texto en español); si no coincide, ese texto se queda en español. Las cifras no se traducen.

## Pulso del sector

La franja bajo la portada lee los datos que el [Radar Farma & Seguros RD](https://braylinjr.github.io/radar-farma-seguros-rd/) publica cada 6 horas:

- `https://raw.githubusercontent.com/BraylinJR/radar-farma-seguros-rd/main/datos/indicadores.json` — tarjetas `inflacion_salud`, `inflacion_interanual`, `tpm` y `salud_actividad` (campos `nombre`, `texto_valor`, `periodo`, `direccion`, `serie[].valor`) y la fecha `actualizado`.
- `https://raw.githubusercontent.com/BraylinJR/radar-farma-seguros-rd/main/datos/resumen_semanal.json` — `total` y `por_prioridad.alta`.

Si la carga tarda más de 4 segundos, falla o los datos tienen más de 14 días, la franja se pliega sin dejar hueco. Sin JavaScript no aparece. El código está en la función `cargarPulso()`.

## Imagen para compartir

`assets/og.png` se generó desde una plantilla HTML con el estilo del sitio, capturada con Chrome sin ventana a 1200×630. Si cambian las cifras de la portada, hay que regenerarla.

## Editar y probar

Los textos están en `index.html`. Para verlo en tu computadora:

```bash
python -m http.server 8000
```

y abre <http://localhost:8000>.
