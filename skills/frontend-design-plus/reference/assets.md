# Assets

Load when [load-map.md](load-map.md) attaches this file (Constraints or Look name photo, video, or illustration). Unanswered blanks belong to the Packet.

Images, video, icons, and other media are design language. Treat them with the same care as type and color.

## Images

### Priority (marketing surfaces)

Marketing pages are visual products. Apply this order before writing markup:

1. **Generate** section-specific images when an image tool is available (hero, product, texture, mood). Match the section aspect ratio.
2. **Use real photography** from the brief, brand assets, or a seeded placeholder URL whose seed describes the section.
3. **Leave labeled slots** (`<!-- TODO: hero product photo, 1600x1200 -->`) and list the missing placements for the user.

Zero images on a landing or portfolio fails pre-flight unless the brief is abstract-only. Isolated components and app UI skip this mandate unless the brief is image-led.

Div-based fake screenshots (styled rectangles as "product UI") fail pre-flight. Prefer a real screenshot, a generated image, a live mini-UI, or no preview.

### Image selection

- Match tone to brand voice: editorial photography for luxury, candid for consumer, precise for enterprise.
- Avoid generic stock feel (overposed business scenes, sterile offices).
- One strong image beats five mediocre ones.

### Technical delivery

| Concern | Guideline |
| --- | --- |
| **Format** | Modern formats first: AVIF, WebP; JPEG as fallback |
| **Sizing** | Serve images close to displayed dimensions; avoid scaling 4000px images to 400px |
| **Aspect ratio** | Reserve space with `aspect-ratio` or explicit `width`/`height` to prevent layout shift (CLS) |
| **Loading** | Lazy-load below-fold images; eager-load hero/LCP image only |
| **Alt text** | Descriptive for content images; empty (`alt=""`) for decorative images |
| **Compression** | Balance quality and weight; aggressive compression ruins brand perception |

### Responsive images

Provide multiple resolutions for critical images so the browser chooses the optimal size:

```html
<img
  src="hero-800.webp"
  srcset="hero-400.webp 400w, hero-800.webp 800w, hero-1600.webp 1600w"
  sizes="(max-width: 600px) 100vw, 50vw"
  alt="..."
  width="800"
  height="600" />
```

## SVG

### When to use SVG

- Icons, logos, wordmarks, simple illustrations
- Any graphic that needs crisp scaling across screen densities

### Rules

- Optimize SVGs before shipping (remove editor metadata, invisible layers).
- Use inline SVG for icons that need CSS color theming (`currentColor`).
- Use `<img>` or background for decorative illustrations that do not need styling.
- Set `focusable="false"` on inline icons; provide `aria-label` or `aria-hidden` on parent interactive elements.
- Never hand-roll complex decorative illustrations as default — prefer established illustration libraries or commissioned assets.

## Icons

- Pick one family and one stroke weight for the entire project. Follow the project; do not default a library by name.
- Do not mix filled and outlined variants without a documented rule.
- Icon + label > icon alone for ambiguous actions. Icon-only controls need an accessible name.
- Decorative icons beside visible text: `aria-hidden="true"` (or native equivalent).
- Meaningful standalone icons need a text alternative; they also need ≥3:1 contrast against adjacent color.
- Icon libraries are preferred over hand-rolled SVG icons for standard UI.
- Emoji is not an icon system. Allow emoji only when the brief asks for a playful/social voice, and never in nav, settings, or controls.

## Logo walls

Logo wall = logos only, placed in a section **under** the hero. Use SVG marks from project assets or a maintained icon set. Invented brands get a simple monogram SVG, not a styled word. No industry/category captions under each logo.

## Video

- No autoplay with sound. Ever.
- Use `poster` image for lazy-loaded videos.
- Respect `prefers-reduced-motion`: pause autoplay videos for users who request reduced motion.
- Lazy-load videos below the fold.
- Prefer `<video>` over GIF for animations — better compression, pause control, accessibility.

## Favicons and meta imagery

- Provide a crisp favicon in multiple sizes and formats (SVG when supported).
- Social sharing images (Open Graph, Twitter Cards): design them intentionally, not as an afterthought. Match brand tone.

## Asset pipeline checklist

- [ ] Images optimized and sized to displayed dimensions
- [ ] Modern formats served with fallbacks
- [ ] Aspect ratios reserved to prevent CLS
- [ ] Alt text on all content images
- [ ] SVGs optimized and accessible
- [ ] Icons consistent in family and weight
- [ ] Video respects autoplay and reduced-motion rules
- [ ] Marketing imagery follows gen → real/seed → TODO slots (no fake screenshots)
- [ ] Logo walls use SVG marks only, under the hero
