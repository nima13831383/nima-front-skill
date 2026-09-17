# Definition of Done

`nima-front` may declare a substantial frontend task complete only when every applicable item below is satisfied with evidence.

## Implementation

- [ ] Requested frontend is implemented.
- [ ] Existing framework, architecture, components, and design system were preserved where reasonable.
- [ ] Application builds and runs.
- [ ] Relevant routes load.
- [ ] No blocking runtime failure affects the requested flow.
- [ ] Assets and fonts load or limitations are documented.

## Responsive

- [ ] Mobile was inspected.
- [ ] Tablet was inspected.
- [ ] Desktop was inspected.
- [ ] Important breakpoint boundaries were inspected when relevant.
- [ ] No known horizontal overflow, clipping, or off-screen controls remain.
- [ ] Navigation, sticky, fixed, and overlay behavior is usable at relevant widths.

## Visual

- [ ] Representative viewport screenshots were captured and reviewed.
- [ ] Full-page screenshots were reviewed when page length or section rhythm matters.
- [ ] Spacing and alignment were checked.
- [ ] Typography scale, line length, wrapping, and hierarchy were checked.
- [ ] Color and visible contrast were checked.
- [ ] Image crops and focal points were checked.
- [ ] Borders, radii, shadows, density, and visual rhythm are coherent.
- [ ] The composition follows the available `ART_DIRECTION_BRIEF` or a clearly stated project-specific direction.

## Interaction

- [ ] Important existing states were inspected.
- [ ] Menus and navigation were checked when present.
- [ ] Forms were checked when present.
- [ ] Dialogs, dropdowns, accordions, tabs, and drawers were checked when present.
- [ ] Focus, hover, active, disabled, loading, empty, error, and success states were checked when present or material.
- [ ] Reduced-motion behavior and visible keyboard focus are acceptable.

## Quality

- [ ] `VISUAL_QA_REPORT` was completed.
- [ ] Objective visual defects were fixed before subjective polish.
- [ ] `ANTI_AI_UI_REVIEW` was completed when appropriate.
- [ ] High-impact generic or incoherent design patterns were addressed or explicitly accepted with rationale.
- [ ] Critical/high issues affecting the requested result are resolved.

## Final verification

- [ ] Fixes were visually re-tested with fresh browser evidence.
- [ ] Previously failing viewports and states were rechecked.
- [ ] No known blocking visual defects remain.
- [ ] Remaining limitations are reported in the delivery response.

If browser-based visual inspection could not be performed, the frontend must be reported as `UNVERIFIED`, not `COMPLETE` or `PASSED`.
