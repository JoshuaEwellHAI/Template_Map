# AGENTS.md

## Cursor Cloud specific instructions

This is a **zero-dependency static web application** (vanilla HTML/JS/CSS). There is no package manager, no build step, no Node.js, and no backend service.

### Running the application

Serve the project root with any static HTTP server:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000/` in Chrome. The app loads `template-map.json` and `component-map.json` via `fetch()`, so it **must** be served over HTTP (not `file://`).

### Key files

- `index.html` — Main application (single-file SPA, ~4500 lines of embedded JS/CSS)
- `template-map-viewer.html` — Alternate/duplicate template viewer
- `template-map.json` — Template definitions and CPT mappings
- `component-map.json` — Component definitions with picklists

### Testing

There are no automated tests, linters, or build checks. Validation is done via manual browser testing. The JSON schema at `templates/schema/template.schema.json` can be used for schema validation of individual template files.

### Saving changes

The app uses the File System Access API (with download fallback) to save changes to `template-map.json` and `component-map.json`. In headless/automated contexts, saves may trigger a file download instead of overwriting in place.
