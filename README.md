# nextjs-template

A runnable Next.js template for [icco](https://github.com/icco) projects, based on
`natwelch.com`, `lifeline`, `realworldsre.com`, and `go-template`.

## Start a project

```sh
gh repo create icco/my-site --public --template icco/nextjs-template --clone
cd my-site
nvm use
npm install --global pnpm@11.2.2
pnpm install --frozen-lockfile
pnpm dev
```

Open <http://localhost:8080>.

1. Update the name, description, and repository in `package.json`.
2. Set the site name, description, and production URL in `src/lib/site.ts`.
   This drives metadata, canonical URLs, robots, and the sitemap at build time.
3. Customize `src/app/page.tsx`, `public/icon.svg`, and this README.
4. Confirm Actions are enabled: `gh api repos/icco/my-site/actions/permissions`.
5. Run the checks below, commit, and push. Main publishes `ghcr.io/icco/my-site:main`.

## Commands

| Command           | Purpose                                                       |
| ----------------- | ------------------------------------------------------------- |
| `pnpm dev`        | Development server on port 8080                               |
| `pnpm check`      | ESLint, strict type checking, and formatting checks           |
| `pnpm lint:fix`   | Fix lint and import order                                     |
| `pnpm format`     | Format files and sort Tailwind classes                        |
| `pnpm build`      | Production build with standalone output                       |
| `pnpm start`      | Local production server (`PORT`, default 8080)                |
| `pnpm test:smoke` | Start production server and check routes and security headers |

## Defaults and provenance

- **natwelch.com / lifeline:** App Router under `src/app`, TypeScript, pnpm,
  Tailwind/daisyUI, standalone Docker on port 8080, and security headers.
- **natwelch.com:** Prettier style, import sorting, GHCR publishing with provenance,
  CodeQL, and weekly Dependabot updates. Actions are pinned to commit SHAs.
- **realworldsre.com:** Explicit type-check command.
- ESLint stays on 9 until Next.js's React, import, and accessibility plugins
  support ESLint 10; TypeScript stays on the established 6.0 line.
- **go-template:** Conventional PR titles and documented project initialization.
- CI checks a frozen lockfile, lint, types, formatting, a production build, and
  HTTP smoke tests. PRs build containers; only main publishes them, after CI passes.
- Server Components by default, accessible page landmarks, dark-mode-aware
  daisyUI themes, system fonts, and a health endpoint at `/healthz`.
- CSP allows inline scripts for Next.js static hydration; `unsafe-eval` is
  development-only. Caddy supplies HTTPS/HSTS at deployment.

`@icco/react-common` (theme providers, navigation, Web Vitals) and Contentlayer2
are optional additions when a project needs them. The starter installs using
the public npm registry without a GitHub Packages token. If adding the shared
package, follow `natwelch.com`'s scoped `.npmrc` and BuildKit secret pattern;
configure the project's reportd destination deliberately.
