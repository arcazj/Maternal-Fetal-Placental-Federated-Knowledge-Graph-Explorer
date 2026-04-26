# Maternal-Fetal-Placental Federated Knowledge Graph Explorer

This ZIP contains a single-file Three.js prototype for browsing a federated maternal-fetal-placental data ecosystem.

## Files

- `index.html` — complete self-contained web application with embedded HTML, CSS, JavaScript, sample graph data, API inventory, mock query engine, and Three.js visualization.
- `README.md` — this guide.

## Live demo

- [Live Demo](https://arcazj.github.io/Maternal-Fetal-Placental-Federated-Knowledge-Graph-Explorer/index.html)
- Hosted live demo URL: `https://YOUR-GITHUB-USERNAME.github.io/mfp-kg-explorer/`

After deployment, replace the placeholder above with the real GitHub Pages, Netlify, Vercel, or static-hosting URL.

## How to run

Open `index.html` in a modern browser such as Chrome, Edge, Firefox, or Safari.

The app uses Three.js ES modules from the public `unpkg.com` CDN through an import map. No build system is required.

If your browser blocks ES modules from local `file://` pages, run a simple local web server from this directory:

```bash
python -m http.server 8080
```

Then open:

```text
http://localhost:8080/index.html
```

## What it includes

- Interactive Three.js knowledge graph
- Domain filters
- Access filters: public, aggregate, controlled, private, standards
- Search across nodes, variables, datasets, APIs, and concepts
- Dataset/API card browser
- Node inspector with URLs, Swagger/OpenAPI notes, variables, tags, and relationships
- Multiple graph layouts:
  - Domain clusters
  - Layered architecture
  - Radial relationship map
  - Force-directed relationship map
- Mock federated query explorer
- API / Swagger inventory
- Federated architecture diagram
- Export graph JSON button

## Scientific design principle

The central knowledge graph should store metadata, ontology terms, dataset descriptions, access rules, aggregate counts, provenance, and approved derived features.

Sensitive data should remain local or inside approved controlled environments:

- Raw patient records
- Raw genomes
- Detailed clinical notes
- Exact addresses
- Direct identifiers
- Restricted research records

## Important modeling rule

Do not treat race/ethnicity as a genetic variable.

- Genetic ancestry = genotype-derived population structure estimate.
- Race/ethnicity = self-reported social, historical, identity, and structural context variable.
- Social environment = lived context, care access, exposure, stress, geography, and inequality.

## Suggested next engineering step

Replace the embedded sample graph with live connectors:

- CDC WONDER connector
- Census connector
- EPA AQS connector
- NCBI E-utilities connector
- Human Cell Atlas connector
- CELLxGENE connector
- Controlled metadata importer for DASH/dbGaP/All of Us
- Local FHIR/OMOP connector for authorized clinical sites

Then expose your own gateway API:

```text
GET  /datasets
GET  /variables
GET  /cohorts
GET  /nodes/{id}/neighbors
POST /federated-query
POST /sparql
POST /graphql
GET  /beacon
GET  /openapi.json
GET  /swagger-ui
```

## Fix notes

### Pointer/raycast fix
This package includes a fix for the browser error:

```text
Uncaught TypeError: Cannot set properties of undefined (setting 'x')
Uncaught TypeError: Cannot read properties of undefined (reading 'x')
```

The graph state now initializes `graph.mouse = new THREE.Vector2()` before pointer and click handlers call `raycaster.setFromCamera()`.
