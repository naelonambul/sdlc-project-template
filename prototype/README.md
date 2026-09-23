# Prototype

A disposable UI/UX discovery workspace for exploratory prototypes, spikes, mock implementations, and interaction experiments.

Prototype content is supporting evidence, not SDLC authority. It must not override the root `../intent.md` and `../spec.md` baseline or an approved change packet in `../changes/`. If a prototype changes the understanding of the problem, requirements, design, or implementation approach, update the relevant change artifact and obtain owner approval through the normal gate.

## Technology boundary

The starter is intentionally simple:

- plain semantic HTML;
- plain CSS;
- vanilla JavaScript;
- no framework, TypeScript, bundler, or build step.

Replace this baseline when a prototype genuinely needs a different stack rather than adding complexity by default.

## Run locally

Open `index.html` directly in a browser, or serve the directory with any static server:

```sh
cd prototype
python3 -m http.server 8000
```

## Quality tooling

The prototype keeps its lint/format tooling inside this directory so it remains self-contained.
Node.js is required for quality checks only, not at runtime. The supported range is
`^20.19.0 || ^22.13.0 || >=24` (declared in `package.json` `engines`; ESLint 10 sets the floor).
`package-lock.json` is committed, so install exactly the locked versions with `npm ci`.

```sh
cd prototype
npm ci

npm run lint          # ESLint + Stylelint + HTMLHint
npm run format        # Prettier: rewrite files
npm run format:check  # Prettier: check only
npm run check         # format:check + lint
```

Configuration:

- JavaScript: `eslint.config.mjs`
- CSS: `stylelint.config.mjs`
- HTML: `.htmlhintrc`
- formatting: `.prettierrc.json`

Do not weaken these checks merely to make prototype validation pass.
