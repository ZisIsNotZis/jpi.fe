# jpi.fe — recursive JSON tree/table editor (Vue 3 SPA)

**One-line:** A single-page Vue 3 front-end that renders an arbitrary JSON
document as an editable recursive tree of tables, backed by a paginated REST API.

**Why it exists:** Experimental front-end for browsing and mutating nested JSON
entities (each entity = a list of objects, each value editable inline). The
recursive `Trees.vue` / `Tables.vue` pair is the interesting part: the same
component re-renders itself for arrays, objects, and scalars, and each node can
add/delete rows and columns at runtime. Built Dec 2024 as a personal experiment
(project name `jpi`), never finished or shipped.

**How to run:**
```sh
npm install
npm run dev        # Vite dev server; expects the API at http://127.0.0.1:8080
```
The original backend is **not** in this directory. All data calls are hardcoded
to `//127.0.0.1:8080/api` (`src/App.vue`), so the UI renders empty/broken without
a matching service.

**Status:** deprecated (2024 era) — kept as an archive. Vue 3.4 / Vite 5
scaffold, one weekend of exploratory UI work; superseded, no users, no tests, no
build config beyond the stock template.

**License:** No LICENSE file. Assumed the owner's own experimental code; add a
license before any public use. The Vite/Vue scaffold is MIT (upstream template).

---
