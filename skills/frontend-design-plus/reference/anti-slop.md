# Anti-slop

Patterns that signal "AI made this." Rewrite matches. Keep a listed pattern when the brief names it, the existing product already ships it, or the sequence is real (01, 02, 03). Document why.

## The slop test

Run this before the _crit_ ([crit.md](crit.md)). Layout and copy each have to pass.

**Cross-register (always):** If someone could identify the output as AI-generated without hesitation, it failed.

**Common-layout check:** "Is this a layout a model ships by default?" Centered hero, three equal feature cards, dark mesh, purple glow, cream-and-brass craft, Inter-on-slate, dark charcoal + one orange accent + fake git-diff or terminal card (developer portfolio). If yes, pick a different family from [layout-patterns.md](layout-patterns.md) before adding polish.

**UX-expert check:** "How would a UX expert improve this for the briefing job?" Name one **layout family** (editorial split, magazine, sticky chrome), not a palette tweak.

**Category-reflex check:** If someone could guess the palette and layout from the product category alone ("SaaS landing", "fintech app", "restaurant site", "developer portfolio"), rework until the answer is not obvious from the domain. Vectors: [color.md](color.md#category-reflex-rework-if-this-was-the-first-idea).

**Second-order check:** The next saturated move ("not SaaS-purple, so editorial serif with mono labels") also fails. Rework until both levels pass.

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
- Empty cells in bento grids
- `border-t` + `border-b` on every row of long lists
- Zigzag image+text split repeated 3+ times consecutively
- Split-header: left big headline + right floating explainer paragraph
- Decoration strip at hero bottom (`BRAND. MOTION. SPATIAL.`)
- Scroll cues (`Scroll to explore`, animated mouse icons)
- Locale/weather strips (`LIS 14:23 · 18°C`) without a place-focused brief
- Version labels in hero (`V0.6`, `BETA`) unless a launch brief
- Pills overlaid on images (`Plate · Brand`)
- Developer-portfolio default: dark charcoal + coral/orange + fake git-diff or terminal window in the hero

## Copy tells

Every visible string is in scope: headlines, subtext, CTAs, nav, empty/error/success, quotes, sample data, alt text, `aria-label`, meta title/description.

**Self-audit:** re-read every string before pre-flight. If a sentence could move unchanged to another product, rewrite it with a fact, mechanism, or judgment from this brief. Doubt: write a functional sentence. One copy register per page. Invent no stats, names, or citations. User-supplied copy: keep the voice; cut only the tells below.

**Second-order:** swapping `elevate` for `unlock your potential` still fails. The replacement has to name a real action or object.

Empty, error, and loading shapes: [ux-principles.md](ux-principles.md#microcopy-and-sample-content).

| Pattern                 | Example                                                                                                                                                                                                                                                                                                          | Do instead                                                 |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| Banned words            | elevate, seamless, unleash, next-gen, revolutionize, empower, delve, foster, leverage, utilize, facilitate, streamline, robust, cutting-edge, game changer, tapestry, realm, beacon, multifaceted, meticulous, intricate, paramount, transformative, embark, supercharge, harness, ever-evolving, paradigm shift | Plain verb + object: "Save the invoice", "Ship on Tuesday" |
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
| Emoji as voice          | headings or buttons with 🚀✨                                                                                                                                                                                                                                                                                    | Words only, unless the brief is playful/social             |
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

## Color strategy anti-patterns

| Wrong                                           | Right                                                                                      |
| ----------------------------------------------- | ------------------------------------------------------------------------------------------ |
| Default warm cream body for "traditional" brief | Carry warmth via accent, type, imagery                                                     |
| New accent color per section                    | One accent locked for whole page                                                           |
| Dark because tools look cool                    | [Scene sentence](color.md#scene-sentence-decide-theme-before-picking-colors) decides theme |
| Light to be safe                                | [Scene sentence](color.md#scene-sentence-decide-theme-before-picking-colors) decides theme |

## AI aesthetic table (quick reference)

| AI default                     | Replace with                                   |
| ------------------------------ | ---------------------------------------------- |
| Inter everywhere               | Brand-appropriate font from brief              |
| Purple gradients               | Project palette or committed single accent     |
| Big rounded corners everywhere | Token radius system with intentional variation |
| Stock card grid                | Varied layout families                         |
| Lorem ipsum                    | Realistic copy at realistic lengths            |
| Spinner in content area        | Skeleton matching layout                       |
| Gray muted body on tinted bg   | Darker text for contrast                       |
