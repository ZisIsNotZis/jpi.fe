<p align="center">
  <img src="assets/logo.svg" width="96" height="96" alt="jpi.fe logo">
</p>

<h1 align="center">jpi.fe</h1>

<p align="center"><strong>Edit JSON the way you read it: a tree of tables.</strong></p>

<p align="center">
  <strong>English</strong> · <a href="README.zh-CN.md">简体中文</a>
</p>

jpi.fe is a Vue 3 single-page app that renders an arbitrary JSON document as nested,
editable tables. Every object and array becomes a table, every scalar an inline input,
and the same two components repeat at any depth. Add a row, a column or a key, change a
value, then save that node back to the API.

It is a 2024 prototype kept as an archive. The REST backend it was written against is
not part of this repository.

## Quick start

```sh
npm install
npm run dev
```

Open the URL Vite prints (usually `http://localhost:5173`). The entity list and paging
call the protocol-relative base `//127.0.0.1:8080/api`, hardcoded in
[`src/App.vue`](src/App.vue); without a compatible backend the built-in sample document
still renders, but loading and saving do not.

## What it can do now

- Recursively render arrays, objects and scalars from any JSON shape
- Edit scalar values inline and add or remove object keys
- Add or delete table rows, and add or delete columns across a table
- Save one node or delete it through the REST endpoints
- Switch between entities and page through results
- Start with a small built-in sample document when no data is loaded

## Architecture

```text
src/
  main.js                 mounts the app
  App.vue                 entity picker, pagination, axios calls
  components/
    Trees.vue             recursive dispatcher: array / object / null / scalar
    Tables.vue            table view for arrays and objects, inline editing
```

`Trees.vue` is the core: it checks the value's type and renders itself for children,
so depth is limited only by the document. `App.vue` owns all HTTP traffic and keeps the
current document in `dat`. There is no router, store or test suite.

See [`docs/project-status.md`](docs/project-status.md) for the archive note.

## How to develop

- Node.js 18+ and npm; dependencies are Vue 3.4, Axios and Vite 5.
- `npm run dev` starts the Vite dev server with hot reload.
- `npm run build` writes a production bundle to `dist/`; `npm run preview` serves it.
- `@/` is aliased to `src/` in [`vite.config.js`](vite.config.js).
- To point the UI at another service, change the API base in
  [`src/App.vue`](src/App.vue) (every request uses it).

## How to contribute

This repository is archived and not actively maintained, so there is no roadmap
commitment. Issues and small pull requests that fix a clear defect are welcome — see
[`CONTRIBUTING.md`](CONTRIBUTING.md) for how to run the app, the one check that exists
(`npm run build`), and what a pull request should contain.

## Roadmap

**Implemented**

- Recursive rendering of arbitrary JSON
- Inline editing, plus add/remove for rows, columns, keys and array items
- Save and delete calls to a paginated REST API
- Entity switching and page navigation

**Planned / not built**

- Configurable API base URL instead of the hardcoded `127.0.0.1:8080`
- A small mock backend or demo mode so the UI can run on its own
- Tests, undo, and keyboard navigation
- Removal of the leftover Vite template package name (`vue-project`)

**Future vision**

The original idea was a generic admin surface for arbitrary JSON: one recursive pair of
components turns any document into an editable, spreadsheet-like tree, so small internal
tools would not each need a bespoke editor. That idea is still worth pursuing; this
repository is its first, unfinished sketch.

## License

GNU Affero General Public License v3.0 only — see [`LICENSE`](LICENSE). Third-party
dependencies keep their own licenses.
