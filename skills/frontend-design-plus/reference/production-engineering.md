# Production engineering

Load when [load-map.md](load-map.md) attaches this file. Component and app UI attach the full file. Marketing always attaches [Resilient text](#resilient-text); attach the rest of this file when the surface has forms or async, or when the Harden row matches. Unanswered blanks belong to the Packet.

Build UIs that look designed and ship reliably.

Patterns below are shown in HTML/CSS for clarity. Translate the syntax to the project's framework (JSX, Vue/Svelte SFCs, template engines, native components) while preserving the semantics: native elements, state separation, and accessibility behavior carry across all of them.

See also: [performance.md](performance.md) and [typography.md](typography.md) when those paths are attached. Anti-slop and pre-flight stay in the QA slot.

## Component architecture

### File structure

Colocate related files:

```txt
components/
  task-list/
    index.html
    styles.css
    script.js            # if interactivity required
    README.md            # if component is shared
```

### Patterns

**Composition over configuration:**

```html
<!-- Good -->
<article class="card">
  <header class="card-header">
    <h2 class="card-title">Tasks</h2>
  </header>
  <div class="card-body">
    <task-list data-tasks="..."></task-list>
  </div>
</article>

<!-- Avoid -->
<div
  class="card"
  data-title="Tasks"
  data-padding="md"
  data-content="tasks"></div>
```

**Separate data from presentation:**

Separate data fetching from rendering. The component that loads data should handle states (loading, error, empty) and pass clean data to the presentation layer:

```html
<!-- Container handles state -->
<div class="task-list-container" data-state="loading">
  <div class="skeleton" aria-busy="true" aria-label="Loading tasks"></div>
</div>

<div class="task-list-container" data-state="error">
  <div class="error-state">
    <p>Failed to load tasks.</p>
    <button type="button" class="retry">Try again</button>
  </div>
</div>

<div class="task-list-container" data-state="empty">
  <div class="empty-state">
    <h3>No tasks</h3>
    <p>Create a task to see it here.</p>
    <button type="button" class="create">Create task</button>
  </div>
</div>

<!-- Presentation receives clean data -->
<ul class="task-list" role="list">
  <li class="task-item">Task one</li>
  <li class="task-item">Task two</li>
</ul>
```

**Keep modules focused** — split when a single file exceeds ~200 lines or combines multiple responsibilities (data, presentation, and logic).

## Accessibility (WCAG 2.2 AA)

Detect the project's framework and translate these patterns. Never assume React, Tailwind, or Next.js. If the stack matters and the repo does not reveal it, ask once.

### Viewport

```html
<meta name="viewport" content="width=device-width, initial-scale=1" />
```

Omit `maximum-scale` and `user-scalable=no`. Body and form controls are ≥16px on mobile so iOS does not zoom on focus.

### Skip link and headings

Page and app shells: first focusable control is a skip link to `#main`. One `h1` per view; heading levels sequential.

```html
<a class="skip-link" href="#main">Skip to content</a>
<main id="main">…</main>
```

The skip link may be visually hidden until `:focus`. Isolated components skip this rule.

### Keyboard

```html
<!-- Good — native button -->
<button type="button">Save</button>

<!-- Avoid — div click without keyboard -->
<div onclick="...">Save</div>
```

### Labels

```html
<label for="email">Email</label>
<input id="email" type="email" />

<button type="button" aria-label="Close dialog">
  <span class="icon-close" aria-hidden="true"></span>
</button>
```

**Label-in-Name (WCAG 2.5.3).** Visible text is the accessible name, or `aria-label` contains that visible text. An `aria-label` that replaces visible words fails. Icon-only controls keep `aria-label`. Omit `aria-label` when the visible label already names the control.

### Focus management

Move focus into modals on open. Trap focus inside dialogs. Restore focus on close. Sticky headers, cookie banners, and FABs must not cover the focused control — set `scroll-padding-top` / `scroll-padding-bottom` to the chrome height. After a client-side route change, move focus to `main`.

### Icon roles

The same glyph has three jobs. Decorative beside visible text: `aria-hidden="true"`. Meaningful without visible text: text alternative. Control: accessible name plus pressed/expanded state when it applies. Meaningful icons need ≥3:1 contrast against adjacent color.

### Meaningful states

```html
<div role="status">
  <span class="icon-empty" aria-hidden="true"></span>
  <h3>No tasks</h3>
  <p>Create a task to see it here.</p>
  <button type="button">Create task</button>
</div>
```

### Contrast checklist

- Body text ≥4.5:1 against background
- Large text (≥18px or bold ≥14px) ≥3:1
- Placeholder text ≥4.5:1 (not default muted gray)
- Gray on colored backgrounds → use darker shade of bg hue or text transparency
- Button text readable on button bg (no white-on-white)
- Modal scrim: measure the **composed** result against the real background (including dark theme); a generic `background: rgb(0 0 0 / 0.5)` often fails

## Forms

Field contract — every control:

- Visible `<label for>` (not placeholder-as-label)
- Semantic `type` and `inputmode` (`email`, `tel`, `url`, `numeric`)
- Real `autocomplete` (`name`, `email`, `username`, `current-password`, `new-password`, address tokens)
- Required indicated in the label (asterisk or the word), not only the `required` attribute
- Helper and error **below** the field, wired with `aria-describedby`
- Related fields in `<fieldset>` / `<legend>`
- `readonly` visually and semantically distinct from `disabled`
- Password fields include a show/hide toggle
- Auth: paste allowed; never `autocomplete="off"` on username/password

**Effort.** Do not add a step that restates a value the user already entered. Keep fields the browser can fill (`autocomplete` tokens above). On app UI, the P0 action is in `main` without a greeting hop; a visible control or documented shortcut is enough.

**Layout.** Field groups are CSS Grid cells (one group = label + control + error/helper). An inline error may grow its row; the next row's labels share a y. Paint one error on the first field of a paired row to prove it. An odd last field spans remaining columns. Two stacked columns of fields fail this. Recheck at 768 and 1024.

Validate **on blur and on submit**. Do not paint errors on every keystroke.

After a failed submit: a focusable error summary at the top with links to each invalid field, **and** inline errors. Focus the summary (or the first invalid field if there is no summary). Messages state cause + how to fix. Use `aria-live="polite"` or `role="alert"` on the error; toasts must not steal focus.

Async submit: disable the control (or ignore a second click), show a loading label, re-enable on failure. One click = one request.

Confirm before dismissing a modal/sheet with unsaved changes. Long forms auto-save drafts when the brief is a multi-step flow.

**Choice of control:**

| Situation | Control |
| --- | --- |
| 2–5 mutually exclusive options, all should be visible | Radio |
| Independent options | Checkbox |
| Long exclusive list | Native `<select>` |
| Persistent binary | Toggle (with a visible label) |
| Three options in a custom dropdown | Fail — use radio |

Native `<select>`, `<dialog>`, and date inputs on product UI unless the brand register requires a custom control.

## Buttons

In any viewport, at most three visual weights: **primary** (one filled), **secondary** (outline or quieter fill), **tertiary** (text/ghost). Destructive is a fourth weight and sits apart from the primary and from nav.

Product: one filled primary per **view**. Marketing: one filled primary per **fold** (the same Success verb may repeat later; that is not a new family).

## Responsive design

Mobile-first breakpoints — test 320, 768, 1024, 1440:

```css
/* Mobile-first grid */
.grid-responsive {
  display: grid;
  gap: 1rem;
  grid-template-columns: 1fr;
}

@media (min-width: 640px) {
  .grid-responsive {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1024px) {
  .grid-responsive {
    grid-template-columns: repeat(3, 1fr);
  }
}
```

Auto-fit grids without breakpoints:

```css
grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
```

An `auto-fit` / `minmax` track that sits empty at 768 is a fail — span the odd item or pick explicit breakpoints.

Rules:

- Touch targets ≥44×44px **and** ≥8px gap between adjacent targets
- Press feedback without changing padding, border, or width (`transform` / opacity / elevation)
- Interactive elements that a reset left as `cursor: default` get `cursor: pointer` on the web
- Primary actions fire on click/tap; hover is not the only path
- `touch-action: manipulation` on controls to reduce tap delay
- No horizontal scroll on mobile
- Explicit mobile collapse for asymmetric layouts; overlap/rotation off below 768px
- `min-height: 100dvh` not `height: 100vh` (iOS Safari address bar)
- Fixed nav / bottom CTA: padding on the scrolling content ≥ chrome height; with `viewport-fit=cover` also `env(safe-area-inset-*)`
- One primary scroll; nested `overflow: auto` only with a reason (virtualized list, code pane)

## Loading and transitions

Prefer skeleton loaders matching final layout over generic spinners:

```html
<div aria-busy="true" aria-label="Loading tasks">
  <div class="skeleton-row"></div>
  <div class="skeleton-row"></div>
  <div class="skeleton-row"></div>
</div>
```

Motion rules:

- Ease-out curves (quart/quint/expo) — no bounce/elastic for product UI
- 150–300ms for state changes (product); longer for brand choreographed reveals
- Exit ~60–70% of enter duration
- `@media (prefers-reduced-motion: reduce)` → crossfade or instant
- Reveal animations must not gate content visibility (hidden tabs, blank sections on initial load)
- Async buttons: disabled or second-click ignored, with a loading label

## Interaction gotchas

- Dropdowns inside `overflow: hidden` get clipped → use `<dialog>`, popover API, `position: fixed`, or portal
- Animate `transform` and `opacity` only — not width/height/top/left. Press states must not shift layout bounds. Name the properties that change; zero `transition: all` / `transition-all` ([surfaces.md](surfaces.md#css-budget))
- `will-change` only on `transform`, `opacity`, or `filter`, and only while the element is animating
- Scroll/mouse-driven animation: use CSS `scroll-timeline` or compositor-only transforms — never update layout-triggering properties on every frame
- Drag/sort: provide a keyboard and simple-pointer alternative; do not rely on drag alone
- Prefer native interactive elements (`button`, `a`, `select`) over clickable `div`s

## Harden

Open this heading when [load-map.md](load-map.md) attaches it: Focus is a11y (or the user named edge cases / production-ready), Constraints named i18n or RTL, or the surface already ships locale. Skip on default greenfield marketing.

**Data overflow.** Layout holds a long unbreakable string, a 1000-row list (paginate or virtualize), and an oversized number without clipping the control or the chrome.

**i18n.** If Constraints named locale or RTL: `html` has `lang`; `dir` matches the locale; copy and labels still fit at ~30% longer strings. Unnamed Constraints: do not invent `lang`/`dir` work.

**Error taxonomy.** Validation (fix this field), network (retry), and permission (who can act) are distinct messages. Do not reuse the hero pitch.

**Offline / slow.** If the Job is async: timeout or degraded copy plus a retry. Skip when the surface is static.

Done when each applicable row has a DOM fact. Do not reopen the occupancy Sketch.

## Resilient text

Heading wrap is progressive enhancement, not a promise that one word stays on the last line. Essential labels reflow at 320px, browser zoom, and text scaling without clipping. Long URLs and identifiers may wrap.

Chip and tag collections wrap or use an operable `+n` disclosure. A compact label stays whole when practical; unavoidable truncation needs an accessible full-value path (tooltip, `title` plus keyboard access, or expand).

Badge meaning cannot rely on color alone. Interactive chips use native semantics, visible focus, and programmatic state.

Rapid interactions may cancel animation. The final semantic state, focus, and content stay correct. `prefers-reduced-motion` still wins. Do not open [motion.md](motion.md) from this heading.
