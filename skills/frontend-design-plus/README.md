# Frontend Design Plus

This skill runs when you ask to create a page, improve a layout, restyle a dashboard, or polish existing HTML and CSS.

Without it, the agent often ships a page it already knows: cream field, serif H1, one accent, three equal cards... slop.

Follow [`SKILL.md`](SKILL.md). Occupancy is written first (the object's rectangles in DESIGN.md), then markup that matches that spine, then one critique against Fail-ifs. Critique does not invent a second look.

The run is Classify → Origin → Layout → markup from DESIGN.md → Floor → Critique once. Origin is greenfield (hex from the object's materials), redesign (disk owns tokens), or polish (keep the live palette; or ask focus). After markup, [critique.md](reference/critique.md) checks the spine. Design and copy Fail-ifs live in [anti-slop.md](reference/anti-slop.md). Operate recipes: [app-ui.md](reference/app-ui.md). Isolated component skips that file.

## This skill is not for

- Backend, SQL, CI, docs-only, and native mobile/desktop.
- CLI detector, live variant picker, or industry-to-palette matching.

If the harness has a browser tool, Walk is a served render of header (one row, drawer closed), first viewport, one scroll past enter, and the close fold at 1440 and 375.

## References

- [DESIGN.md format](https://github.com/google-labs-code/design.md/blob/main/docs/spec.md)
