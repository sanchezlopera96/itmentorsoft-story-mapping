# Story Map — Tutor Inteligente ITM (ITMentorSoft)

Sitio estático (una carpeta, sin servidor) que **muestra el Story Map** del proyecto, publicable en **GitHub Pages**.

Estructura del mapa:

- **Objetivo del usuario** (arriba).
- **Columna vertebral:** los **Temas** (actividades) con sus **Épicas** debajo como sub-encabezados.
- **Tarjetas:** las **Historias de Usuario** (con estado, puntos y nº de tareas).
- **Filas = Releases:** Release 1 / MVP, Release 2, Release 3 (prioridad de entrega).

Es **solo de lectura**: el mapa se genera leyendo `data/backlog.csv` (export de Azure DevOps). Para actualizarlo, se **reemplaza ese archivo** y se publica de nuevo.

URL (una vez publicado): **https://sanchezlopera96.github.io/itmentorsoft-story-mapping/**

---

## Actualizar el Story Map

1. En Azure DevOps exporta los work items a **CSV** con las columnas:
   `ID, Title, Work Item Type, State, Effort, Tags`.
2. Renombra el archivo a **`backlog.csv`** y reemplázalo en `data/`.
3. En GitHub Desktop: *Changes* → *Commit to main* → *Push origin*.
4. Recarga la página en ~1 minuto.

### Cómo se interpreta el backlog

- La **jerarquía se arma por orden y tipo**: `Epic` (Tema) → `Feature` (Épica) → `Product Backlog Item` (HU) → `Task`.
- Cada **HU** es una tarjeta, ubicada en la columna de su Épica.
- La **Release** de cada HU se toma de la etiqueta **Tags**:
  - `MVP` → **Release 1 / MVP**
  - `R2` (o `Release 2`) → **Release 2**
  - `R3` (o `Release 3`) → **Release 3**
  - sin etiqueta de release → fila **Posterior**
- El nº de **tareas** de cada HU se cuenta a partir de sus filas `Task`.
- El **título** de la HU se toma de *Title* quitando el prefijo `HU x.y.z`.

> Para controlar las releases desde Azure, basta etiquetar cada Product Backlog Item con `MVP`, `R2` o `R3` en el campo *Tags*.

---

## Publicar en GitHub Pages

1. Sube el contenido de esta carpeta al repositorio (con `index.html` en la **raíz**).
2. **Settings → Pages → Source → Deploy from a branch**, rama `main`, carpeta `/ (root)`, **Save**.

## Estructura de la carpeta

```
.
├── index.html            # el Story Map (lee el backlog y lo dibuja)
├── .nojekyll
├── data/
│   └── backlog.csv       # FUENTE — export de Azure DevOps
└── README.md
```

## Notas técnicas

- Lee el backlog con **SheetJS (xlsx)** desde cdnjs (requiere internet); acepta `.csv` y `.xlsx` (el archivo debe llamarse `backlog.csv`).
- Abierto por doble clic (`file://`) muestra una **versión de respaldo incluida**; publicado en GitHub Pages (`https://`) lee el backlog con normalidad.
- Botón **Imprimir / PDF** (A3 horizontal).
