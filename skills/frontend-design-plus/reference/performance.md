# Performance

Speed is UX. Treat Core Web Vitals as product constraints. Record whether the result is `guided`, `measured`, or `verified` in [verification.md](verification.md); implementation advice alone is not a runtime result.

## Targets (ship gate)

| Metric  | Target  | What it measures                                |
| ------- | ------- | ----------------------------------------------- |
| **LCP** | < 2.5s  | Perceived load — hero image, largest text block |
| **INP** | < 200ms | Responsiveness to taps/clicks/keyboard          |
| **CLS** | < 0.1   | Visual stability — no layout jump               |

Also watch **long tasks** (>50ms main-thread blocks) — they cause "stuck" feeling even when averages look fine.

## Performance budgets

Define limits **before** implementation:

- Max JavaScript shipped on initial route
- Max client-side rendering cost on initial load
- Max image weight above the fold
- Max third-party script count

Heavy routes get separate budgets. A dashboard can weigh more than a landing hero when heavy UI is isolated to its own route or request.

## Load strategy

Keep first paint lean. Ship critical layout and content as markup; defer heavy UI and secondary content to later requests.

| Priority | Approach | When |
| --- | --- | --- |
| **Critical** | Static markup for layout and above-fold | First paint, LCP element, primary message |
| **Heavy route** | Dedicated route or deferred data fetch | Dashboards, editors, large tables |
| **Optional UI** | Load on demand via navigation or fetch | Settings, modals, flows users may skip |
| **Below fold** | Lazy-load media and secondary sections | Images, far-down blocks |

Default to shipping markup first and enhancing with interactivity progressively. Only load heavy scripts when the UI truly requires them.

## Images

- Modern formats (WebP, AVIF); size to displayed dimensions
- `priority` / preload for LCP hero only; lazy-load below fold
- Reserve width/height (or aspect-ratio) to prevent CLS
- Decorative images still need alt="" or role="presentation"

## Fonts

- Self-host fonts via `@font-face`; subset when possible; limit variants shipped
- `font-display: swap` to prevent invisible text during load

## CSS and animation

- Animate `transform` and `opacity` only on critical paths
- Grain/noise on `fixed` overlays with `pointer-events-none`
- `will-change` sparingly

## Network and delivery

- Compression (Brotli/Gzip); cache static assets; defer third-party scripts
- Load only scripts the brief requires

## Data and lists

- Fetch above-fold data in parallel; show skeleton states while loading
- Lists/tables with **≥50** visible rows: paginate or virtualize
- Debounce high-frequency input (search, resize, filter)
- Visual press feedback within ~100ms (`:active` counts)

## Perceived performance

- Skeleton loaders matching final layout (not generic spinners)
- Optimistic UI for reversible actions
- Instant feedback on click even if server is slow

Lab tools (Lighthouse, DevTools) complement but do not replace real devices and networks. State what was NOT measured in the [verification](verification.md) block and pre-flight honesty.
