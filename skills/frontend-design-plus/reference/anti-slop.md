# Anti-slop

Run from the QA slot ([dispatch.md](dispatch.md#qa)) after markup, before the *crit* ([crit.md](crit.md)). Isolated component: this window. Unanswered blanks: the Packet, not [briefing.md](briefing.md).

Patterns that signal "AI made this." QA records matches as P0. Implement rewrites. Keep a listed pattern when the brief names it, the existing product already ships it, or the sequence is real (01, 02, 03). Document why.

## The slop test

Run this before the *crit* ([crit.md](crit.md)). Layout and copy each have to pass. Start with what must be on screen, then **Always**, then the branch for this task type. Isolated component: Always only, unless the component is a KPI strip or chart ([Dashboard tells](#dashboard-tells)).

**On screen (marketing greenfield/redesign):** Sketch masses at measured `tracks=`. Logo-swap breaks the read. Skip the object-swap fail when Packet `object-swap=n/a`; when the line is not `n/a`, still-reads fails ([composition.md](composition.md#frame)).

**On screen (app UI):** Packet `recipe=` (or `none` on settings) occupies `main`. Greeting nodes in `main` = 0. Implement returned `main=` / `proof=`.

### Always

**Cross-register:** If someone could identify the output as AI-generated without hesitation, it failed.

**Model-default triad:** Greenfield marketing with Look `you-decide` or Lock `style=none`: cream ~`#F4F1EA` + high-contrast serif + terracotta, near-black + one acid or vermilion, or broadsheet (hairline, radius 0, dense columns) fails unless Packet *tension* named that axis. A named catalog `id` or a brief that asked for one of these looks still passes. Skip on origin `polish` / `redesign` (disk owns the look). Pick clusters: [design-styles.md](design-styles.md#pick).

**Deletion check:** *Cut* already ran in Direction on marketing greenfield/redesign. Confirm Packet Cut competitors stayed off the page. Then name **one** remaining craft accessory the brief did not ask for (grain overlay, overlap-badge, `01` markers, a second card family, marquee) and fail if it is still on the page. Isolated component and app UI: name three competing blocks; remove extra until Job + Success still hold. Extra chrome (parallax, custom cursor, uniform fade-in, 3D blobs) fails unless the brief named it. What remains after the *cut* is the composition.

**Code-floor check:** A component kit (Shadcn, Material, the project library) supplies states and structure. Theme, type, radius, and copy come from DESIGN.md. Default kit chrome as the look fails unless that look is already on disk.

### Marketing

**Common-layout check:** First viewport shows the Sketch masses at measured `tracks=` ([crit.md](crit.md) Q1). Origin `polish`: name an in-place craft fix; keep the current family. Missing Sketch, missing `tracks=`, or missing *thesis* on greenfield or redesign: fail this check; the parent re-dispatches. `object-swap=` against measured enter still reads, or the line is missing: re-dispatch Direction — skip this fail when the line is `n/a`. A media-column + CTA-rail split without *kinship* of two sibling tasks: unjustified split; rewrite until Sketch masses are on screen. Centered hero + three equal feature cards, dark mesh, purple glow, cream-and-brass craft, Inter-on-slate, dark charcoal + one orange accent, spec-sheet title block, fake git-diff or terminal card, years-as-handle wordmark: rewrite until the Sketch masses are on screen.

**UX-expert check:** Name the *map* (first viewport + remaining folds from Packet *objects*, matched to Sketch `tracks=`), not a palette tweak. Origin `polish`: name an in-place craft fix.

**Category-reflex check:** Logo-swap breaks the read, and each first-viewport mass is a Packet *object*. Matching the domain is validation when occupancy traces to those *objects* (a studio site whose enter mass *is* the kiln). Rework when the first viewport is the category default *scaffold* with no *object* in the lead rectangle. Palette first-idea vectors: [color.md](color.md#category-reflex-rework-if-this-was-the-first-idea). A *scene* written on `you-decide` / invent-all is occupancy from *kinship*, not the category-default place ("desk at night" for a developer portfolio). Skip on origin `polish`.

**Second-order check:** The hop “not SaaS-purple, so editorial serif with mono labels” fails unless Packet *tension* names that axis. Rework the hop; do not invent a farther costume. Skip on origin `polish`.

**Interchangeability check:** Swap the wordmark for another company's. If the first viewport still reads, rewrite copy and composition until the job is visible without the name. Origin `greenfield` and `redesign`: this must fail (logo-swap breaks the read). Origin `polish`: skip as a composition gate; still rewrite portable slogans ([Copy tells](#copy-tells)).

### App UI

**Common-layout check:** Four equal KPI cards + donut + area/line + "Welcome back", or default kit chrome as the look. If yes, pick the matching recipe from [product-register.md](product-register.md#dashboards) (queue vs gallery) before adding polish. Origin `polish`: retire the tells in place; do not invent a new recipe. Do not pick a novel layout family.

**UX-expert check:** Name the product recipe (queue home, list+filter, editor, accounts) or an in-place craft fix if that recipe is already on screen. Not a marketing spine.

Skip category-reflex, second-order, and interchangeability on chrome. A CMS that still reads after a logo-swap **passes**. Sample data and empty copy still need domain nouns ([Dashboard tells](#dashboard-tells)).

## Absolute bans

Rewrite any element that matches:

| Pattern                                         | Why                                        | Do instead                                                                                |
| ----------------------------------------------- | ------------------------------------------ | ----------------------------------------------------------------------------------------- |
| Side-stripe borders (`border-left` >1px accent) | Never intentional on cards/alerts          | Hairline or inset from [material-craft.md](material-craft.md) on brand; tokens on product |
| Gradient text (`background-clip: text`)         | Decorative                                 | Solid ink on the display face                                                             |
| Glassmorphism as default                        | Rare                                       | Matte, hairline, or ink; glass only if the scene asks                                     |
| Hero-metric template                            | Big number + small label + stats row       | One proof point with a source, or cut                                                     |
| Identical card grids                            | Icon + heading + blurb × N                 | Magazine, container-free, or one card family ([layout-patterns.md](layout-patterns.md))   |
| Eyebrow on every section                        | Small caps `ABOUT` `PROCESS` above each H2 | Cap eyebrows at `ceil(sections / 3)`                                                      |
| Numbered section markers (`01 · About`)         | Fake sequence                              | Numbers only on a real sequence                                                           |
| Text overflowing container                      | Unchecked H1                               | Wide H1 container; test every breakpoint                                                  |
| Em dashes (`—`) anywhere visible                | LLM signature                              | `-`, commas, periods                                                                      |
| Three equal feature cards                       | Default SaaS scaffold                      | Split, bento, or a comparison table                                                       |

## Visual tells

- Neon outer glows on buttons
- Pure `#000000` / `#ffffff` (use off-black, off-white)
- Oversaturated accents on everything
- Custom mouse cursors
- Purple/blue gradient glow as default accent
- Cream/sand/beige body backgrounds (`#f5f1ea`, `--paper`, `--cream`, etc.) as default "warmth"
- Warm craft palette as default for premium consumer (beige + brass + oxblood + espresso) without brand justification

## Typography tells

**Reflex-reject fonts** (training-data defaults). Look further unless the pairing procedure in [typography.md](typography.md#font-pairing-structure-not-a-fashion-list) selected them on purpose:

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

App UI only. Rewrite if present. Keep only if the brief named that scaffold or disk already ships it. Do-instead: [product-register.md](product-register.md#dashboards). Chrome: [surfaces.md](surfaces.md).

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

**Self-audit:** re-read every string before pre-flight. If a sentence could move unchanged to another product, rewrite it with a fact, mechanism, or judgment from this brief. Doubt: write a functional sentence. One copy register per page. Invent no stats, names, or citations. User-supplied copy: keep the voice; cut only the tells below.

**Second-order:** swapping `elevate` for `unlock your potential` still fails. The replacement has to name a real action or object.

Empty, error, and loading shapes: [ux-principles.md](ux-principles.md#microcopy-and-sample-content).

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
| CTA wrap                | primary wrapping to 2+ lines at desktop                                                                                                                                                                                                                                                                          | ≤3 words, one line                                         |
| Long pull-quotes        | quotes >3 lines on a landing                                                                                                                                                                                                                                                                                     | One short line or cut                                      |
| Lorem / latin           | `Lorem ipsum`, `Your catchy headline here`                                                                                                                                                                                                                                                                       | Real draft copy at real length                             |
| Em dash / `--`          | decorative `—` in UI copy                                                                                                                                                                                                                                                                                        | `-`, comma, or period. Zero in short UI strings            |

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
| Dark because tools look cool                    | [briefing.md](briefing.md#theme) owns mode; scene owns temperature                         |
| Light to be safe                                | [briefing.md](briefing.md#theme) owns mode; scene owns temperature                         |
| Both / system shipped as one locked mode        | Two palettes plus a chrome control ([color.md](color.md#system-theme))                     |
| Tinted dark canvas (green/navy field)           | Charcoal surfaces; accent on actions ([color.md](color.md#dark-mode-construct-dont-invert))|
