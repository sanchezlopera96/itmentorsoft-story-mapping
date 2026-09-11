# Story Map — Tutor Inteligente ITM (ITMentorSoft)

Sitio estático (una carpeta, sin servidor) que **muestra el Story Map** del proyecto *Tutor Inteligente ITM*, publicable en **GitHub Pages**.

Es **solo de lectura**: el mapa se genera leyendo el backlog exportado de Azure DevOps (`data/backlog.csv`). Para actualizarlo, se **reemplaza ese archivo** y se publica de nuevo.

> El diagrama WBS / EDT vive en un repositorio aparte; este repo contiene únicamente el Story Map.

URL (una vez publicado): **https://sanchezlopera96.github.io/itmentorsoft-story-mapping/**

---

## Actualizar el Story Map

1. En Azure DevOps (Boards / Backlog) exporta los work items a **CSV** con las columnas:
   `ID, Title, Work Item Type, State, Effort, Iteration Path, Tags`.
2. Renombra el archivo a **`backlog.csv`** y reemplázalo en `data/`.
3. En GitHub Desktop: *Changes* → *Commit to main* → *Push origin*.
4. Recarga la página en ~1 minuto.

Cómo se interpreta el backlog:

- La **jerarquía se arma por orden y tipo**: `Epic` (Tema) → `Feature` (Épica) → `Product Backlog Item` (HU) → `Task`.
- Cada **HU** es una tarjeta, ubicada en la columna de su Épica y en la **fila de su sprint** (número tomado de *Iteration Path*, p. ej. `…\Sprint 4`).
- La etiqueta **MVP** (columna *Tags*) resalta la tarjeta en dorado.
- El nº de **tareas** de cada HU se cuenta a partir de sus filas `Task`.
- El **título** de la HU se toma de *Title* quitando el prefijo `HU x.y.z`.

> También lee `.xlsx`, pero el archivo debe llamarse `backlog.csv` (o cambia la constante `CSV_URL` dentro de `index.html`).

---

## Publicar en GitHub Pages

1. Sube el contenido de esta carpeta al repositorio (con `index.html` en la **raíz**).
2. **Settings → Pages → Source → Deploy from a branch**, rama `main`, carpeta `/ (root)`, **Save**.
3. La URL será `https://TU-USUARIO.github.io/TU-REPO/`.

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

- Lee el backlog con **SheetJS (xlsx)** desde cdnjs (requiere internet).
- Abierto por doble clic (`file://`) el navegador bloquea la lectura del archivo y muestra una **versión de respaldo incluida**; publicado en GitHub Pages (`https://`) lee el backlog con normalidad.
- Botón **Imprimir / PDF** (A3 horizontal).
