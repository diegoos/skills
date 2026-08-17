# File architecture

Bind the stack and file tree before the first markup. A *cold reader* who opens the repo after this pass can name where HTML, CSS, and JS live.

## Detect

Read `package.json`, lockfiles, and framework config (`next.config.*`, `astro.config.*`, `vite.config.*`, `nuxt.config.*`, `svelte.config.*`, `angular.json`, `vue.config.*`). Match neighboring pages: same folder shape, same styling method, same CSS entry.

If a README or skill note cites a path that is not on disk, **disk wins**; then ask. Do not rebuild a palette, button, or layout the repo already has.

Redesign stays on that stack (patch existing files). Greenfield with no stack uses the default below. Migrating framework or CSS library needs explicit user approval ([redesign.md](redesign.md#never-change-silently)). Two live conventions (BEM vs modules, Vite vs static): ask once; do not coin-flip.

## Ask

Greenfield with no detectable stack and no invent-all: include **Stack** in the *briefing* batch. Offer at least: simple HTML+CSS+JS, Next.js, React, Vue, Astro, Svelte, Tailwind, Material UI. The user may name another.

Do not default in the same turn as that ask. If they pick nothing after answering, or the run is invent-all with no stack named, use the **default**.

## Default (no stack named)

Vanilla files at the surface root the user named (or `.` if they named none):

| File         | Owns                                                                                                                                                                                              |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `index.html` | Structure only. Link `main.css` and `main.js`. No `<style>` blocks except a last-resort critical snippet under 20 lines.                                                                          |
| `main.css`   | All layout, type, color, motion. Tokens as custom properties on `:root` matching DESIGN.md. Hex belongs here or in DESIGN.md, not in HTML/JSX (SVG fills that must be literal are the exception). |
| `main.js`    | Behavior. Empty file with a comment is valid when the surface is static.                                                                                                                          |

A single HTML file that also holds the stylesheet fails pre-flight on this default.

## Project or framework named

Follow that project's conventions. Do not invent a parallel tree.

| Signal                   | Put files where                                                                   |
| ------------------------ | --------------------------------------------------------------------------------- |
| Next.js App Router       | `app/` routes, CSS per existing pattern (`globals.css`, CSS modules, or Tailwind) |
| Vite React/Vue           | `src/` entry the template already uses                                            |
| Astro                    | `.astro` pages + existing `src/styles`                                            |
| SvelteKit                | `src/routes`                                                                      |
| Tailwind already in repo | utilities in the project's CSS pipeline; still no giant `<style>` in markup       |
| Sass/BEM in repo         | partials the project already uses                                                 |
| DESIGN.md present        | tokens in CSS/theme files; values copied from DESIGN.md, not a second palette     |

One styling system per surface. Mixing a new utility framework into a token CSS codebase is a new stack; ask first.

## Greenfield with a named framework

Scaffold only what the task needs (one page, one layout, the CSS/JS entry). Skip extra config, sample counters, and README spam.

Done when the Lock `stack=` names the detected, asked, or default stack **and matches the files on disk**, and markup, styles, and behavior live in separate files unless the project's convention is single-file components (`.vue`, `.svelte`, `.astro`) with styles in the component's style block or the project's CSS entry.
