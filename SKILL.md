---
name: nima-front
description: Orchestrate end-to-end frontend design, implementation, browser inspection, responsive visual QA, anti-generic design review, and final verification for substantial frontend work such as new pages, landing pages, dashboards, redesigns, screenshot or Figma implementations, and responsive UI changes.
metadata:
  short-description: Orchestrate polished frontend design and QA
---

# Nima Front Skill

Use this skill as the primary orchestrator when the user expects a complete, polished frontend result rather than an isolated code snippet. It is a control plane: route to the existing specialist skills by responsibility and do not copy their full instructions into this skill.

## Hard quality gate

Never say “done,” “finished,” “complete,” “production-ready,” or equivalent for substantial frontend implementation unless the actual rendered interface has been inspected in a real browser across relevant viewports and meaningful UI states, defects have been addressed, and the result has been visually verified again. Build success, tests, TypeScript success, Lighthouse, and a clean console are not visual verification.

If required browser or screenshot tooling is unavailable, report `UNVERIFIED` with the reason. Do not silently mark the frontend as passed.

## Specialist routing

- `design-reference-analyzer`: when screenshots, images, Figma references, URLs, or existing websites exist. Consume its `DESIGN_REFERENCE_BRIEF`; never use it to implement the frontend.
- `art-direction`: before substantial creative implementation. Consume its `ART_DIRECTION_BRIEF`; it turns project context and optional references into concrete visual decisions.
- `frontend-design`: the primary creative implementation skill. Use the installed Anthropic upstream version unchanged.
- `ui-ux-pro-max`: advisory support for accessibility, usability, responsive conventions, UX patterns, and component behavior. It must not erase intentional project direction.
- `browser-runtime-inspector`: real-browser technical evidence—DOM, computed styles, geometry, overflow, stacking, interaction states, page/runtime errors, and screenshots.
- `visual-qa`: objective rendered-interface QA and responsive visual verdict. Consume or produce `VISUAL_QA_REPORT`.
- `anti-ai-ui-review`: post-QA design criticism for generic, templated, or AI-looking patterns. Consume or produce `ANTI_AI_UI_REVIEW`; do not use it as a generic bug checker.

Read [workflow.md](references/workflow.md) for routing and handoff detail, [visual-testing.md](references/visual-testing.md) for the browser protocol, and [definition-of-done.md](references/definition-of-done.md) for the completion gate.

## Branch immediately on references

With a visual reference:

`design-reference-analyzer → art-direction → frontend-design → implementation → browser-runtime-inspector → visual-qa → anti-ai-ui-review → refinement → browser-runtime-inspector → visual-qa`

Without a visual reference:

`art-direction → frontend-design → implementation → browser-runtime-inspector → visual-qa → anti-ai-ui-review → refinement → browser-runtime-inspector → visual-qa`

For close reproduction, prioritize fidelity to the supplied evidence and do not invent a radically different direction. For a new design, do not force the user to provide references and do not fall back to generic AI aesthetics.

## Operating rules

1. Inspect the existing project, framework, design system, assets, components, and styling architecture before changing code. Preserve working conventions and avoid unnecessary rewrites or dependencies.
2. Establish the visual direction before substantial implementation. Common patterns are allowed only when justified by product context, existing brand rules, or the briefs.
3. Use `frontend-design` for the real implementation, with `ui-ux-pro-max` as supporting knowledge where it materially improves usability or accessibility.
4. Run technical checks before polish: application starts, routes load, assets and fonts resolve, and no blocking runtime errors remain. This is a checkpoint, not completion.
5. Perform mandatory real-browser visual testing. Capture representative mobile, tablet, and desktop evidence; inspect meaningful states that actually exist; diagnose visible problems with `browser-runtime-inspector`; and use `visual-qa` for the visual report.
6. Fix objective visual defects before running `anti-ai-ui-review`. Apply only targeted high-impact refinements, then repeat browser inspection and `visual-qa` with fresh evidence. Normally stop after one or two meaningful refinement passes.

## Precedence

Resolve conflicts in this order: explicit user requirements → existing product/brand system → `DESIGN_REFERENCE_BRIEF` → `ART_DIRECTION_BRIEF` → `frontend-design` principles → generic `ui-ux-pro-max` recommendations. Accessibility and functional usability remain mandatory exceptions and must not be sacrificed for aesthetics.

## Lightweight routing

Do not activate the entire pipeline for every UI task. A single text-color change may need no design skill; an overflow bug may need `browser-runtime-inspector → visual-qa`; one supplied component may need `frontend-design → targeted browser verification`; an existing page cleanup may need `browser-runtime-inspector → visual-qa → anti-ai-ui-review → refinement → re-test`. New landing pages, dashboards, major redesigns, and screenshot recreations use the appropriate full branch.

## Delivery response

When the work is genuinely verified, report briefly:

```text
FRONTEND DELIVERY

Implemented:
Tested:
States checked:
Visual fixes:
Verification:
Remaining issues:
```

Use `Verification: PASSED` only with actual browser evidence. Otherwise use `Verification: UNVERIFIED`.
