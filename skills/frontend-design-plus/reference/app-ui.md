# App UI

Recipes for product surfaces: dashboard, admin, CMS, settings, data tables, authenticated tools. The interface disappears into the task.

Open when Mode is `Operate` and Origin is greenfield or redesign. Polish keeps the live recipe.

Done when `main` matches the recipe (or settings with no recipe), greeting nodes in `main` = 0, and filled primary count = 1.

## Pick

Write "the user is here to ______," then pick **one** recipe per view. Settings and odd tools stay on the [app shell](#app-shell) with no recipe id.

| Surface                                        | Recipe                                                                       |
| ---------------------------------------------- | ---------------------------------------------------------------------------- |
| CMS / admin / editorial home                   | `queue-home` (`main` = what needs me now)                                    |
| CRM home that asks for action                  | `queue-home`                                                                 |
| Record catalog, inbox, ops list                | `list-filter`                                                                |
| Deal / post / record / deep settings that edit | `editor`                                                                     |
| People and roles                               | `accounts`                                                                   |
| Settings and tools outside those four          | app shell only                                                               |
| Job is BI, not a queue                         | KPI Label→Value→Delta→Time; chart only with a question; table or queue below |

One sans family for UI. Near-neutral surfaces + accent ≤10%. Semantic color for status. Nested cards fail. A card is a clickable unit (feed item), not a KPI row, settings row, table row, or form group.

## App shell

Default: top bar + side nav. Top bar only when destinations fit one row. Split / master-detail when a list drives a pane. Command palette may pair.

Persistent nav in a predictable place. Collapse the side nav below `lg`. Bottom nav ≤5, icon+label, top-level only. Mark where the user is. One primary work area. Controls stay inside the rail ([critique.md](critique.md#surfaces)).

## queue-home

`h1` names the queue (Drafts, Scheduled, Failing), not a greeting. Filters visible in `main`. One filled primary in the view header. KPI optional: one strip, 1 hero number + at most 2 ranked siblings — never 4 equal cards. Workflow objects exist as rows in `main`.

## list-filter

The table or dense list is the spine. Search plus 2–4 filters on the same plane. Empty, loading (skeleton rows), and error on the list. A view with ≥8 rows has ≥1 visible filter.

## editor

Content canvas + meta panel. Save (or the persist verb) is the filled primary and stays visible. Same nav as the list.

## accounts

Rows are people or seats. Filters are role / status. `main` is a people list, not a KPI gallery.

## Shared

Left-align text, right-align numbers. Sticky table header. Empty / loading / error on lists. First-run is one next step that completes the Job — not a welcome `h1` in `main`.
