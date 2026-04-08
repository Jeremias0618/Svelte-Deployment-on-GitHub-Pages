# Svelte Deployment on GitHub Pages

[![Svelte](https://img.shields.io/badge/Svelte-5-FF3E00?logo=svelte&logoColor=white)](https://svelte.dev/)
[![Vite](https://img.shields.io/badge/Vite-7-646CFF?logo=vite&logoColor=white)](https://vite.dev/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.9-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![License](https://img.shields.io/badge/license-Private-lightgrey)]()

[![Visitors](https://visitor-badge.laobi.icu/badge?page_id=Jeremias0618.Svelte-Deployment-on-GitHub-Pages)](https://github.com/Jeremias0618/Svelte-Deployment-on-GitHub-Pages)

Minimal **[Svelte](https://svelte.dev/)** single-page app built with **[Vite](https://vite.dev/)** and **TypeScript**, set up so it can be hosted on **[GitHub Pages](https://pages.github.com/)** under a **project site** URL (`https://<user>.github.io/<repository>/`).

**Repository:** [github.com/Jeremias0618/Svelte-Deployment-on-GitHub-Pages](https://github.com/Jeremias0618/Svelte-Deployment-on-GitHub-Pages)

**Live site (after you enable GitHub Pages on `gh-pages` or Actions):** [jeremias0618.github.io/Svelte-Deployment-on-GitHub-Pages](https://jeremias0618.github.io/Svelte-Deployment-on-GitHub-Pages/)

> [!NOTE]
> The live URL only works after you configure GitHub Pages in the repository settings and publish the built `dist` folder (for example via GitHub Actions).

## Tech stack

| Area | Technology | Role |
|------|------------|------|
| UI | [Svelte 5](https://svelte.dev/) | Components and reactivity |
| Bundler / dev server | [Vite 7](https://vite.dev/) | Fast HMR, optimized production builds |
| Language | [TypeScript](https://www.typescriptlang.org/) | Static typing |
| Tooling | [svelte-check](https://github.com/sveltejs/language-tools) | Svelte + TS diagnostics |

Dev dependencies also include `@sveltejs/vite-plugin-svelte`, `@tsconfig/svelte`, and `@types/node`. See `package.json` for exact versions.

## Prerequisites

- [Node.js](https://nodejs.org/) (LTS recommended)
- npm (bundled with Node)

## Getting started

```bash
git clone https://github.com/Jeremias0618/Svelte-Deployment-on-GitHub-Pages.git
cd Svelte-Deployment-on-GitHub-Pages
npm install
npm run dev
```

Open the URL Vite prints (usually `http://localhost:5173/`).

## Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Start the dev server with HMR |
| `npm run build` | Production build to `dist/` |
| `npm run preview` | Preview the production build locally |
| `npm run check` | Run `svelte-check` and TypeScript on Node config |

## GitHub Pages and `vite.config.ts`

GitHub **project sites** are served from a subpath: `/<repository-name>/`. Vite must emit asset URLs with that prefix, which is what [`base`](https://vite.dev/config/shared-options.html#base) does.

> [!IMPORTANT]
> The minimal snippet you often see in docs only shows `base` for brevity. In **this** project you still need **`plugins: [svelte()]`** from `@sveltejs/vite-plugin-svelte`. The correct shape is **both**: `base` **and** the Svelte plugin (plus any other options you add later).

If you rename the repository, update the `repoName` constant in `vite.config.ts` so `base` stays correct.

> [!TIP]
> For a **user or organization** site (`username.github.io` with the repo named `username.github.io`), the site is served from the root; in that case use `base: '/'` instead.

## Deploying (overview)

1. Run `npm run build` and upload the contents of `dist/` to the branch or artifact GitHub Pages uses, **or**
2. Add a **GitHub Actions** workflow that runs `npm ci`, `npm run build`, and deploys `dist` with [actions/upload-pages-artifact](https://github.com/actions/upload-pages-artifact) / [actions/deploy-pages](https://github.com/actions/deploy-pages).

Ensure the repository **Settings → Pages** source matches how you publish.

## Project structure

```
├── public/          # Static assets copied as-is
├── src/
│   ├── assets/
│   ├── lib/         # Example components (e.g. Counter)
│   ├── App.svelte
│   └── main.ts
├── index.html
├── vite.config.ts
├── svelte.config.js
└── tsconfig*.json
```

## Recommended IDE setup

[Visual Studio Code](https://code.visualstudio.com/) with the [Svelte extension](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode).
