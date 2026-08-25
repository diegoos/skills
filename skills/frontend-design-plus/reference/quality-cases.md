# Quality cases

Use these short cases to calibrate the [visual rubric](visual-rubric.md). They are textual fixtures, not substitutes for a render. A project-specific screenshot wins over these examples.

## Kiln booking

Brief: a studio manager books the next kiln firing slot in a short scan. Objects: kiln heat, open slot, booking action.

Weak: centered headline, abstract gradient, three equal benefits, and a generic closer ([anti-slop.md](anti-slop.md#cta-check)). It names the industry in copy but wears `first-character-costume=`.

Strong: the kiln or the next open slot is the lead mass, the booking control is visible without scroll, and the schedule is a later object when it is on Inventory. Job and Hierarchy score `2` when the render shows that task. Overlap, split, or stack may all pass when they match the Sketch and are not the costume.

## Developer portfolio

Brief: a hiring manager scans selected work and contacts the engineer.

Weak: charcoal background, orange accent, fake terminal, years-as-handle, and three project cards. The details are recognizable as a category costume, not as the person's work.

Strong: the lead project artifact, decision, or constraint determines the first-viewport mass; the contact action is visible without competing with it; project evidence uses the engineer's actual domain nouns.

## CMS queue

Brief: an operator triages pending records and resolves the oldest exception.

Weak: greeting, four equal KPIs, donut, and traffic chart. The workflow exists only in navigation.

Strong: the work queue occupies `main`, the oldest exception is ranked, filters are visible when the list is long, and empty/loading/error states belong to the same plane. Originality is not required in the chrome; specificity and scan speed are.

## Custom register vs catalog costume

Brief: a kiln studio site with Look `you-decide`. Tension is industrial heat + calendar precision.

Weak: Pick sets `style=industrial` or `style=swiss` because those ids feel “designed,” and that id *is* the costume. Occupancy is three firing-type cards.

Strong: `style=none` (or `style=custom` only when writing a register). Craft comes from the enter object. Occupancy follows the Sketch. Language scores `2` on `style=custom` only when the render shows that signature.

## Law firm (loose prompt)

Brief: “Site para um escritório de advocacia.” Job named; no occupancy, theme, or palette.

Weak: navy + serif + columns, a justice photo, three “áreas de atuação” cards, a generic closer ([anti-slop.md](anti-slop.md#cta-check)). `character=` said trust but the surface wears `first-character-costume=`.

Strong: A/B picked a document stack or a split of matter + proof. Enter is the parecer or case in `form=magazine`. CTA is “Agendar consulta” or the picked Success verb. `scan=pyramid`. `style=none` unless the user named an id that is not `professional`. Domain scores `2` only when navy columns fail in the DOM.

## Tech product landing (loose prompt)

Brief: “Landing page de um produto de tecnologia.”

Weak: mesh, HUD, fake terminal, `id=cyberpunk` or `id=terminal` because the Job said tech.

Strong: enter is the instrument or artifact from the prompt, or Success's object if none was named. Join is the A/B pick. Costume (mesh/HUD) is off screen. Language comes from the object's material, not from neon.

## SaaS they built (loose prompt)

Brief: “Landing page para o SaaS que eu criei.”

Weak: indigo, three feature cards, a generic closer ([anti-slop.md](anti-slop.md#cta-check)), `id=saas`.

Strong: the product occupies enter. Folds use Packet `:<form>` (table for plans, one proof, CTA). Primary label is the Success verb from the A/B pick. `id=saas` is refused. Distinctness names the indigo-card costume and points at a DOM fact that kills it.

## Copy divide

Brief: a kiln studio. Occupancy is kiln heat plus the booking control.

Weak: H1 "Book your firing.", sub "Reserve a kiln slot today.", CTA "Book a firing". Three paraphrases of Success. Occupancy can still hold. Copy *divide* fails ([anti-slop.md](anti-slop.md#copy-tells)).

Strong: H1 names the kiln or the open slot. Sub adds one fact (next window, cone, duration). CTA is the Success verb+object.

## Accessible gray box

Brief: the same kiln. Contrast is "fixed" by flattening enter into a pale card of body type.

Weak: AA contrast on a generic card. Sketch masses gone. Language `2` claimed from an a11y checklist.

Strong: contrast and the accessible name sit on the kiln mass. Occupancy and `scale=` still hold.

## Calibration rule

If a case sounds strong but the screenshot does not show the claimed relationship, score the evidence that exists. Do not award points for text quality. Domain or Language `2` without a render this run is a miss. `See:` that only cites `data-mass` is a miss. H1, sub, and CTA that paraphrase each other are a miss. `style=custom` Language `2` without the signature in the first viewport is a miss. A layout is not weak solely because the *join* is ordinary.
