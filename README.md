# Nikita Engine website

Two static pages with no build step. `index.html` is the landing page and
`docs.html` is the NikaScript reference and tutorials; each carries its own
styles and scripts. The landing hero runs the editor's background shader
ported to WebGL, so the site and the engine never drift apart visually.

## What the engine reads from here

| File | Read by |
|---|---|
| `versions.json` | The update check in the project manager |
| `mirrorlist/<version>.json` | The **Download and Install** button in the export template manager |

Both formats come from the engine, not from convention: see `EngineUpdateLabel`
and `ExportTemplateManager`. The mirrorlist points at a `.tpz` package, which
is what lets a user install export templates without leaving the editor.

## Publishing

The site repository holds one thing this folder does not: `downloads/`, with
the export template package. It is tens of megabytes, so it is kept out of the
engine history and copied in at publish time.

    python misc/scripts/publish_site.py

The script clones the site repository, copies these files over it, adds any
package found in `dist/`, and pushes. GitHub Pages serves the `main` branch
from the root, and `.nojekyll` keeps Jekyll away from the files.

To preview locally, open `index.html` in a browser. It needs no server.
