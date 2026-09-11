# WBS + Story Map — Tutor Inteligente ITM

Sitio estático (una carpeta, sin servidor) con **dos vistas** del proyecto *Tutor Inteligente ITM (ITMentorSoft)*, publicable en **GitHub Pages**:

- **`index.html`** — Diagrama **WBS / EDT** (solo lectura). Lee `data/WBS_Tutor_Inteligente_ITM.xlsx`.
- **`storymap.html`** — **Story Map** (solo lectura). Lee `data/backlog.csv` (export de Azure DevOps).

Ambas páginas están enlazadas entre sí por una barra de navegación y son **solo de lectura**: nadie modifica el contenido desde el navegador. Para actualizar, se **reemplaza el archivo de datos** correspondiente y se publica de nuevo.

URL del proyecto: **https://sanchezlopera96.github.io/itmentorsoft-wbs/**

---

## Actualizar el WBS

1. Edita `data/WBS_Tutor_Inteligente_ITM.xlsx` (columnas `Código · Nivel · Entregable/… · Rama`; la jerarquía se deduce del `Código`: `1` → `1.1` → `1.1.1`). La fila `Código = 0` es el nombre del proyecto.
2. Guarda con el mismo nombre en `data/`.
3. En GitHub Desktop: *Changes* → *Commit to main* → *Push origin*.
4. Recarga la página en ~1 minuto.

## Actualizar el Story Map

1. En Azure DevOps (Boards / Backlog) exporta los work items a **CSV** incluyendo las columnas:
   `ID, Title, Work Item Type, State, Effort, Iteration Path, Tags`.
2. Renombra el archivo a **`backlog.csv`** y reemplázalo en `data/`.
3. Commit + Push. Recarga `storymap.html`.

Cómo se interpreta el backlog:

- La **jerarquía se arma por orden y tipo**: `Epic` (Tema) → `Feature` (Épica) → `Product Backlog Item` (HU) → `Task`.
- Cada **HU** es una tarjeta; se ubica en la columna de su Épica y en la **fila de su sprint** (número tomado de *Iteration Path*, p. ej. `…\Sprint 4`).
- La etiqueta **MVP** (columna *Tags*) resalta la tarjeta en dorado.
- El nº de **tareas** de cada HU se cuenta a partir de sus filas `Task`.
- El **título** de la HU se toma de *Title* quitando el prefijo `HU x.y.z`.

> El export también acepta `.xlsx`; si lo prefieres, guarda el archivo como `data/backlog.csv` de todos modos (el visor lee ambos formatos, pero el nombre debe ser `backlog.csv`) o ajusta la constante `CSV_URL` dentro de `storymap.html`.

---

## Publicar en GitHub Pages

1. Sube el contenido de esta carpeta al repositorio (con `index.html` en la **raíz**).
2. **Settings → Pages → Source → Deploy from a branch**, rama `main`, carpeta `/ (root)`, **Save**.
3. La URL será `https://TU-USUARIO.github.io/TU-REPO/`.

---

## Estructura de la carpeta

```
.
├── index.html                              # Diagrama WBS (lee el Excel)
├── storymap.html                           # Story Map (lee el backlog)
├── .nojekyll
├── data/
│   ├── WBS_Tutor_Inteligente_ITM.xlsx      # FUENTE del WBS
│   └── backlog.csv                         # FUENTE del Story Map (export Azure DevOps)
└── README.md
```

## Notas técnicas

- Ambas páginas leen los datos con **SheetJS (xlsx)** desde cdnjs (requiere internet).
- Abiertas por doble clic (`file://`) el navegador bloquea la lectura del archivo y muestran una **versión de respaldo incluida**; publicadas en GitHub Pages (`https://`) leen los datos con normalidad.
- Botón **Imprimir / PDF** en cada página (A3 horizontal).
