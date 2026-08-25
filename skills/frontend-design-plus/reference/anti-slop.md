# Anti-slop

Run from the QA slot ([dispatch.md](dispatch.md#qa)) after markup, before the *crit* ([crit.md](crit.md)). Isolated component: this window. Unanswered blanks: the Packet.

Patterns that signal "AI made this." QA records matches as P0. Implement rewrites. Keep a listed pattern when the brief names it, the existing product already ships it, or the sequence is real (01, 02, 03). Document why.

## Rule ids

Cite `rule=<id>` in the QA table when a listed tell matches. Fail-if is a grep, computed style, or DOM count — not a vibe. Do not invent ids outside this table.

| id | Fail-if |
| --- | --- |
| `model-default-triad` | Cream ~`#F4F1EA` + display serif + terracotta, acid-on-near-black, or broadsheet default on greenfield `style=none` ([Always](#always)) |
| `side-stripe` | `border-left` (or inline start) >1px accent on a card or alert |
| `gradient-text` | `background-clip: text` on a headline or CTA |
| `glass-default` | Backdrop blur / frost on a surface the scene did not name |
| `hero-metric` | Big number + small label + stats row as the first-viewport proof |
| `identical-cards` | Icon + heading + blurb × N unless Packet `:<form>` is `catalog-cards` |
| `eyebrow-every` | Uppercase eyebrow count > `ceil(sections / 3)` |
| `numbered-markers` | `01` section markers with no real sequence |
| `three-feature-cards` | Three equal feature cards as a fold |
| `generic-cta` | Primary label in the CTA check list and not Packet Success |
| `mesh-hero` | Centered hero + dark mesh gradient |
| `nested-cards` | Card inside a card on product UI |
| `overused-font-inter` | Inter / Geist / Outfit as unexamined brand default ([Typography tells](#typography-tells)) |
| `costume-vest` | First viewport matches Packet `first-character-costume=` |

## The slop test

Run this before the *crit* ([crit.md](crit.md)). Layout and copy each have to pass. Start with what must be on screen, then **Always**, then the branch for this task type. Isolated component: Always only, unless the component is a KPI strip or chart ([Dashboard tells](#dashboard-tells)).

**On screen (marketing greenfield/redesign):** First viewport **is** the Sketch masses at measured `tracks=`, the enter object noun is visible in that rectangle (not only `data-mass`), `scale=` holds, and the primary CTA is Packet Success. Occupancy grammar: [crit.md](crit.md) Q1. Costume vest fails.

**On screen (app UI):** Packet `recipe=` (or `none` on settings) occupies `main`. Greeting nodes in `main` = 0. Implement returned `main=` / `proof=`.

### Always

**Cross-register:** If someone could identify the output as AI-generated without hesitation, it failed.

**Model-default triad:** Greenfield marketing with Look `you-decide` or Lock `style=none`: cream ~`#F4F1EA` + high-contrast serif + terracotta, near-black + one acid or vermilion, or broadsheet (hairline, radius 0, dense columns) fails unless Packet *tension* named that axis. A named catalog `id` or a brief that asked for one of these looks still passes. Skip on origin `polish` / `redesign` (disk owns the look).

**Deletion check:** *Cut* already ran in Direction on marketing greenfield/redesign. Confirm Packet Cut competitors stayed off the page. Then name **one** remaining craft accessory the brief did not ask for (grain overlay, overlap-badge, `01` markers, a second card family, marquee) and fail if it is still on the page. Isolated component and app UI: name three competing blocks; remove extra until Job + Success still hold. Extra chrome (parallax, custom cursor, uniform fade-in, 3D blobs) fails unless the brief named it. What remains after the *cut* is the composition.

**Code-floor check:** A component kit (Shadcn, Material, the project library) supplies states and structure. Theme, type, radius, and copy come from DESIGN.md. Default kit chrome as the look fails unless that look is already on disk.

### Marketing

**Common-layout check:** First viewport shows the Sketch masses at measured `tracks=` ([crit.md](crit.md) Q1). Origin `polish`: name an in-place craft fix; keep the current family. Missing Sketch, `tracks=`, `scan=` / `form=`, or *thesis*: fail; the parent re-dispatches. Rewrite until those masses are on screen. Layout and visual tells stay in [Layout tells](#layout-tells) and [Visual tells](#visual-tells) — do not treat this check as a second list. Unjustified split (media column + CTA rail without two sibling tasks) and `break=none` with three equal bands fail Q1.

**UX-expert check:** Name the *map* (first viewport + remaining folds from Packet *objects* with `:<form>`, matched to Sketch `tracks=`), not a palette tweak. Origin `polish`: name an in-place craft fix.

**Category-reflex check:** Logo-swap breaks the read, and each first-viewport mass is a Packet *object*. Matching the domain is validation when occupancy traces to those *objects*. Rework when the first viewport vests `first-character-costume=`. First-idea palettes that fail: navy-for-law, indigo-for-SaaS, Neutrals-as-fear-default, mesh-HUD-for-tech. A *scene* written on `you-decide` / invent-all is occupancy from *kinship*, not the category-default place. Skip on origin `polish`.

**Costume-id check:** Lock `style=` is `professional` on a firm, `saas` / `enterprise` on "my SaaS", or `terminal` / `cyberpunk` on "tech", and briefing Look did **not** name that id: fail. Prefer `style=none` vesting the enter object. User named that id (prompt or Style pick): record the costume risk in the finding; do not P0 the authorship.

#### CTA check

The visible primary label is the Success verb+object. These strings fail as a generic closer unless that string **is** the user's Success: "Saiba mais", "Learn more", "Get started", "Compre aqui", "Book now". Other files point here; they do not recopy the list.

**Second-order check:** The hop “not SaaS-purple, so editorial serif with mono labels” fails unless Packet *tension* names that axis. Rework the hop; do not invent a farther costume. Skip on origin `polish`.

**Interchangeability check:** Swap the wordmark for another company's. If the first viewport still reads, rewrite copy and composition until the job is visible without the name. Origin `greenfield` and `redesign`: this must fail (logo-swap breaks the read). Origin `polish`: skip as a composition gate; still rewrite portable slogans ([Copy tells](#copy-tells)).

### App UI

**Common-layout check:** Four equal KPI cards + donut + area/line + "Welcome back", or default kit chrome as the look. If yes, Packet `recipe=` must be the matching queue vs gallery (`queue-home` / `list-filter` / `editor` / `accounts`) before adding polish. Origin `polish`: retire the tells in place; do not invent a new recipe. Do not pick a novel layout family.

**UX-expert check:** Name the product recipe (queue home, list+filter, editor, accounts) or an in-place craft fix if that recipe is already on screen. Not a marketing spine.

Skip category-reflex, second-order, and interchangeability on chrome. A CMS that still reads after a logo-swap **passes**. Sample data and empty copy still need domain nouns ([Dashboard tells](#dashboard-tells)).

## High-risk tells

Rewrite any element that matches unless the brief, existing system, semantic need, or selected visual language justifies it. Keep the reason in the QA finding when an exception remains.

| Pattern                                         | Why                                        | Do instead                                                                                |
| ----------------------------------------------- | ------------------------------------------ | ----------------------------------------------------------------------------------------- |
| Side-stripe borders (`border-left` >1px accent) | Never intentional on cards/alerts          | Hairline or inset from DESIGN.md tokens on brand; tokens on product                       |
| Gradient text (`background-clip: text`)         | Decorative                                 | Solid ink on the display face                                                             |
| Glassmorphism as default                        | Rare                                       | Matte, hairline, or ink; glass only if the scene asks                                     |
| Hero-metric template                            | Big number + small label + stats row       | One proof point with a source, or cut                                                     |
| Identical card grids                            | Icon + heading + blurb × N                 | Packet `:<form>`; catalog-cards only when the object is a catalog                         |
| Eyebrow on every section                        | Small caps `ABOUT` `PROCESS` above each H2 | Cap eyebrows at `ceil(sections / 3)`                                                      |
| Numbered section markers (`01 · About`)         | Fake sequence                              | Numbers only on a real sequence                                                           |
| Text overflowing container                      | Unchecked H1                               | Wide H1 container; test every breakpoint                                                  |
| Decorative em dashes (`—`) in UI copy           | Templated aside or LLM residue             | Use a comma, period, or hyphen; keep an em dash when the copy register genuinely needs it |
| Three equal feature cards                       | Default SaaS scaffold                      | The Packet fold `:<form>` (`magazine` / `table` / `one-proof` / `list`). Not a bento.     |

## Visual tells

- Neon outer glows on buttons
- Pure `#000000` / `#ffffff` (use off-black, off-white)
- Oversaturated accents on everything
- Custom mouse cursors
- Purple/blue gradient glow as default accent
- Cream/sand/beige body backgrounds (`#f5f1ea`, `--paper`, `--cream`, etc.) as default "warmth"
- Warm craft palette as default for premium consumer (beige + brass + oxblood + espresso) without brand justification

## Typography tells

**Reflex-risk fonts** (training-data defaults). Look further unless DESIGN.md, the selected visual language, or the project stack chose them on purpose:

Fraunces, Newsreader, Lora, Crimson family, Playfair Display, Cormorant, Syne, IBM Plex family, Space Mono, Space Grotesk, Inter (as **brand** default; product may follow the project), DM Sans/Serif, Instrument Sans/Serif.

Outfit and Plus Jakarta Sans: overused as unexamined defaults. Allowed when the pairing procedure chose them.

Geist, Clash Display, and PP Editorial New are the next Inter. Skip them as a premium default stack.

**Serif:** reach for a sans display unless the brief names serif or the aesthetic is editorial, luxury, or publication.

**Emphasis:** italic/bold of the same font. Keep serif words out of a sans headline.

## Layout tells

- Centered hero + dark mesh gradient (default LLM landing)
- 6-line wrapped H1 in a narrow container (use a wide container, fewer lines)
- Empty cells or empty bordered shells in any grid
- `border-t` + `border-b` on every row of long lists
- Zigzag image+text split repeated 3+ times consecutively
- Split-header: left big headline + right floating explainer paragraph
- Decoration strip at hero bottom (`BRAND. MOTION. SPATIAL.`)
- Scroll cues (`Scroll to explore`, animated mouse icons)
- Locale/weather strips (`LIS 14:23 · 18°C`) without a place-focused brief
- Version labels in hero (`V0.6`, `BETA`) unless a launch brief
- Pills overlaid on images (`Plate · Brand`) — overlap-badge in the gutter; the *break* can leave without killing P0
- Stock photo added to satisfy a “real visual” check when Packet P0 perception is type
- A *break* mass that can be removed without killing P0
- Developer-portfolio default: dark charcoal + coral/orange + spec-sheet / drawing title block (REV, DOC NO, SHEET, dashed PORTRAIT) or fake git-diff / terminal in the hero
- Years-as-handle wordmark (`SW-ENG-013`, `swe-13`) unless the user said that word

## Dashboard tells

App UI only. Rewrite if present. Keep only if the brief named that scaffold or disk already ships it. Do-instead: Packet `recipe=` (`queue-home`, `list-filter`, `editor`, `accounts`).

| Tell                                                      | Fail when                                                            |
| --------------------------------------------------------- | -------------------------------------------------------------------- |
| Four equal KPI cards + donut + area/line + "Welcome back" | Any 3 of those 4 in the first viewport                               |
| Unranked equal KPIs                                       | Same card chrome; Users / Sessions / Views / Bounce; no ranking      |
| Decorative traffic chart                                  | Line/area with no written question beside it                         |
| Device/browser donut                                      | Pie/donut >3 slices, or composition is not the job                   |
| Greeting as the main heading                              | "Welcome back" / "Good morning" as `h1` in `main`                    |
| Duplicate chrome                                          | Filled CTA in nav and header, or avatar in sidebar and header        |
| Control overflowing the rail                              | Sidebar or toolbar button kisses or crosses the chrome edge          |
| Workflow objects only in the sidebar                      | Draft / scheduled / inbox exist as nav only; `main` is charts        |
| Domain only in sample data                                | Sports / CMS / desk nouns missing from rows, filters, and empty copy |
| Chart gallery                                             | 3+ chart types, no question per chart                                |

## Copy tells

Every visible string is in scope: headlines, subtext, CTAs, nav, empty/error/success, quotes, sample data, alt text, `aria-label`, meta title/description.

**Self-audit:** re-read every string before pre-flight. Every marketing sentence names a fact, mechanism, or object from Inventory or Success. If a sentence could move unchanged to another product, rewrite it until that holds. Doubt: write a functional sentence. One copy register per page: this Job's nouns. Invent no stats, names, or citations. User-supplied copy: keep the voice; cut only the tells below.

**Divide check:** H1 names an Inventory or Success object. Subtext, when present, adds one fact or mechanism the H1 does not carry. Cover the H1: the sub still informs. Cover both: the CTA still names Packet Success ([CTA check](#cta-check)). Feeling copy (`easy`, `great`, `amazing`, `you'll love`, `Don't worry`) fails this target. Chrome-speak (`button`, `click here`, `abaixo`, `the tab below`) fails: cite the control's visible label. `role=alert`, empty, and error copy stay dry: what is missing or what failed, plus the one next step. They do not inherit the hero pitch. A copy fail leaves occupancy as it is: cut words if the H1 wraps past two desktop lines.

**Second-order:** swapping `elevate` for `unlock your potential` still fails. The replacement has to name a real action or object.

Empty: name what is missing and the action that fills it. Loading: skeleton; add text only for a long wait. Error: what happened and how to recover; no blame. Sample names and stats fit this Job's locale; never `Lorem ipsum`, `John Doe`, `Acme`, or unsourced `92%`.

| Pattern                 | Example                                                                                                                                                                                                                                                                                                          | Do instead                                                 |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| Banned words            | elevate, seamless, unleash, next-gen, revolutionize, empower, delve, foster, leverage, utilize, facilitate, streamline, robust, cutting-edge, game changer, tapestry, realm, beacon, multifaceted, meticulous, intricate, paramount, transformative, embark, supercharge, harness, ever-evolving, paradigm shift | Plain verb + object: "Save the invoice", "Ship on Tuesday" |
| Portable slogan         | "Build the future", "all-in-one platform", "Scale without limits", "transform your workflow"                                                                                                                                                                                                                     | Verb + object from this job (marketing: fail a logo-swap)  |
| Throat-clearing         | "Here's the thing.", "Welcome to the future of X.", "Let's dive in."                                                                                                                                                                                                                                             | Start with the claim or the CTA                            |
| Binary contrast         | "This is not a tool. It's a partner." / "Not just X, but Y."                                                                                                                                                                                                                                                     | State Y                                                    |
| Faux-insight            | "What most teams get wrong", "The part everyone misses"                                                                                                                                                                                                                                                          | Make the claim with no setup                               |
| Colon reveal            | "The difference: it just works."                                                                                                                                                                                                                                                                                 | A full sentence                                            |
| Superficial `-ing`      | "highlighting our commitment", "showcasing innovation"                                                                                                                                                                                                                                                           | Cause or consequence: "so you can find last week's draft"  |
| Importance puffery      | "marks a pivotal moment", "stands as a testament"                                                                                                                                                                                                                                                                | The fact: "first paid plan"                                |
| Weasel attribution      | "experts agree", "trusted by thousands", "studies show"                                                                                                                                                                                                                                                          | Name the source or cut                                     |
| Fake-strong verbs       | "serves as a hub", "enables teams to"                                                                                                                                                                                                                                                                            | "is" / "has" / the concrete verb                           |
| Synonym cycling         | "platform… solution… ecosystem" for one product                                                                                                                                                                                                                                                                  | Repeat the clear word                                      |
| Rule of three           | "Fast. Simple. Powerful." as the whole pitch                                                                                                                                                                                                                                                                     | One specific promise                                       |
| Dramatic fragments      | "That's it. That's the whole thing."                                                                                                                                                                                                                                                                             | Complete sentences                                         |
| Rhetorical setup        | "What if we told you…", "Ready to transform?"                                                                                                                                                                                                                                                                    | The action                                                 |
| Fake-profound kicker    | closing metaphor or mic-drop under the CTA                                                                                                                                                                                                                                                                       | End on the action or the next step                         |
| Chatbot residue         | "Oops!", "Great question!", "I hope this helps!"                                                                                                                                                                                                                                                                 | Direct error or empty copy                                 |
| Title Case Headlines    | "Strategic Insights For Modern Teams"                                                                                                                                                                                                                                                                            | Sentence case, except proper nouns                         |
| Emoji as voice          | headings or buttons with rocket or sparkle emoji                                                                                                                                                                                                                                                                 | Words only, unless the brief is playful/social             |
| Generic people/brands   | John Doe, Sarah Chan, Acme, Nexus, SmartFlow                                                                                                                                                                                                                                                                     | Names that fit the domain and locale                       |
| Fake-precise stats      | `92%`, `4.1×`, `99.99%` with no source                                                                                                                                                                                                                                                                           | Real data, or qualitative proof, or cut                    |
| Poetic craftsman labels | "Field notes", "On our desks", "Quietly in use at"                                                                                                                                                                                                                                                               | Ordinary section names                                     |
| Duplicate CTA intent    | "Get in touch" + "Let's talk"                                                                                                                                                                                                                                                                                    | One intent, one label                                      |
| Generic CTA             | closer that is not Packet Success                                                                                                                                                                                                                                                                                | [CTA check](#cta-check)                                    |
| CTA wrap                | primary wrapping to 2+ lines at desktop                                                                                                                                                                                                                                                                          | ≤3 words, one line                                         |
| Long pull-quotes        | quotes >3 lines on a landing                                                                                                                                                                                                                                                                                     | One short line or cut                                      |
| Lorem / latin           | `Lorem ipsum`, `Your catchy headline here`                                                                                                                                                                                                                                                                       | Real draft copy at real length                             |
| Decorative em dash      | Templated aside or LLM residue in UI copy                                                                                                                                                                                                                                                                        | Keep it when the register needs it                         |

Filler adverbs (`just`, `literally`, `simply`, `actually`, `truly`, `fundamentally`, `crucially`) and phrases (`at its core`, `in today's world`, `when it comes to`, `in order to`) come out when they delay the point. Keep them only when they are the product's spoken voice.

## Asset tells

- Div-based fake screenshots (styled rectangles as "product UI")
- Hand-rolled SVG icons (use icon libraries)
- Hand-rolled decorative illustrations as default
- Plain text wordmarks in logo walls (use SVG marks from project assets or icon libraries)
- Industry labels under logos (brand name + category caption under each logo)
- Broken or unverified remote image URLs

## Motion tells

- `window.addEventListener('scroll')` driving UI state every frame
- Motion claimed but page is static
- Animation library on every section without purpose
- Two+ horizontal marquees on one page
- Infinite loops on every card
- Bounce/elastic easing on product UI
- Uniform fade-in on every section (same duration, same easing)
- Parallax or animated background as default "craft"

## Color strategy anti-patterns

| Wrong                                           | Right                                                                                      |
| ----------------------------------------------- | ------------------------------------------------------------------------------------------ |
| Default warm cream body for "traditional" brief | Carry warmth via accent, type, imagery                                                     |
| New accent color per section                    | One accent locked for whole page                                                           |
| Dark because tools look cool                    | Lock `theme=` owns mode; occupancy owns temperature                                        |
| Light to be safe                                | Lock `theme=` owns mode; occupancy owns temperature                                        |
| Both / system shipped as one locked mode        | Two palettes plus a labeled chrome control that sets `data-theme` or a class on `html`     |
| Tinted dark canvas (green/navy field)           | Charcoal surfaces; accent on actions                                                       |
