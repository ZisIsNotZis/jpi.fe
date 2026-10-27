# Contributing to jpi.fe

## Scope

This repository is an archived 2024 prototype: a Vue 3 client that edits arbitrary JSON
as a recursive tree of tables. The REST backend it was written against is not here, so
keep contributions to things the current code can actually demonstrate — defect fixes,
small UX corrections, doc corrections. Features that assume a new API shape belong in a
pull request that describes that API, not in a silent change.

## Running the app locally

```sh
npm install
npm run dev
```

Vite prints the URL (usually `http://localhost:5173`). Entity list and paging call
`//127.0.0.1:8080/api`, hardcoded in `src/App.vue`; without a compatible backend the
built-in sample document still renders, but loading and saving do not.

## Checks

There is no test suite, linter or formatter in this repository, and none is wired into
commit hooks. The only mechanical check is that the production build succeeds:

```sh
npm run build
```

Run it before opening a pull request, and describe whichever backend (if any) you
exercised the UI against. Keep the diff focused; unrelated reformatting makes a small
fix hard to review.

## Pull requests

- One concern per pull request, with a message in Conventional Commits form
  (`fix:`, `docs:`, `chore:`).
- Preserve the existing shape: `App.vue` owns HTTP and paging, `Trees.vue` recurses,
  `Tables.vue` renders the table. New abstractions need a reason in the description.
- Say how you verified the change — build output, browser used, backend or no backend.

## Issues

State what you expected, what happened, and the JSON shape involved (redact anything
private). Because the project is not maintained, a clear reproduction is the best chance
a report has of being fixed; feature requests are welcome as discussion but carry no
roadmap commitment.
