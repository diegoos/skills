# Verification

Open from Implement after the first viewport exists, then from QA. This file records evidence; it does not replace visual judgment. A DOM measurement is not a screenshot, and a static inspection is not a browser pass.

## Evidence levels

| Level | Evidence | Claim allowed |
| --- | --- | --- |
| `browser` | A real render was inspected at the required viewports and the relevant interaction was exercised | Visual, responsive, and interaction findings may be marked pass when the evidence supports them. |
| `dom` | `getBoundingClientRect`, `scrollWidth`, source, and computed structure were inspected without a render | Geometry and structure may be marked pass; visual polish and interaction remain `unverified` unless separately tested. |
| `static` | Files, tokens, markup, and CSS were inspected without runtime measurements | Implementation intent may be recorded; layout, visual, and runtime claims remain `unverified`. |
| `unverified` | No meaningful inspection was available | Do not claim the surface is visually verified. List the missing evidence. |

## Required checks

Run the checks that apply to the surface. Use 320px, 768px, and 1024px for responsive inspection; add 1440px for the first viewport and app chrome when a browser or DOM measurement is available.

### Geometry

- Marketing: measure `data-mass="enter"`, `rest`, and `break` when present; compare to the Packet Sketch within one column.
- App UI: confirm `main` contains the Packet recipe rather than greeting or chrome.
- All surfaces: check `scrollWidth <= clientWidth` at 320px and confirm fixed or sticky elements do not cover focused content.

### Interaction and accessibility

- Exercise the primary action, keyboard order, visible focus, and any changed state.
- Check labels, accessible names, reduced motion, and contrast pairs that the surface actually uses.
- Record whether an automated accessibility checker ran. Source inspection alone is not an automated pass.

### Performance

Use `performance=guided` when only implementation rules were followed, `performance=measured` when runtime metrics were captured, and `performance=verified` only when the measured result meets the targets in [performance.md](performance.md). Do not convert a target into a result by assumption.

## Return block

Implement returns this block after its viewport proof. QA updates it rather than inventing a second format.

```txt
Verification:
proof=browser|dom|static|unverified
viewports=320 pass|fail|unverified; 768 pass|fail|unverified; 1024 pass|fail|unverified; 1440 pass|fail|unverified
geometry=pass|fail|unverified
interaction=pass|partial|unverified
accessibility=pass|partial|unverified; automated=<yes|no>
performance=guided|measured|verified
screenshots=<paths or none>
not-verified=<comma-separated evidence gaps or none>
```

The block is valid only when every field exists. `not-verified=none` is allowed only when the declared evidence level supports every applicable check.

## Ship rule

A P0, a failed required check, or a missing return field blocks the surface. An `unverified` field does not become a pass; it remains a limitation in the final hand-off. If the harness had a browser or screenshot tool this run and the slot did not use it, that unused capability is a **P1** (not a visual P0). If the user asked for measured performance, browser QA, or real-device confidence, `unverified` is a P1 until the requested evidence exists. Honesty `0` on the visual rubric blocks ship.

## Done

The return block exists, each applicable check is marked with evidence, and the hand-off states what was not verified.
