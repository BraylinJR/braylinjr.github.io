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

Orden de la página: portada y cifras → Pulso del sector → 01 Casos → 02 Conferencias → 03 Docencia → 04 Reconocimientos → 05 Trayectoria → 06 Formación → 07 Cómo trabajo → Contacto.

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
