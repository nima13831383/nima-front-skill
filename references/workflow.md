# Nima Front Workflow

This reference defines the end-to-end routing contract. The specialist skills remain independently usable; `nima-front` coordinates them when the user expects a complete frontend result.

## Reference provided

```text
User brief and visual reference
        ↓
design-reference-analyzer
        ↓  DESIGN_REFERENCE_BRIEF
art-direction
        ↓  ART_DIRECTION_BRIEF
frontend-design
        ↓
implementation
        ↓
browser-runtime-inspector
        ↓  real-browser evidence
visual-qa
        ↓  VISUAL_QA_REPORT
anti-ai-ui-review
        ↓  ANTI_AI_UI_REVIEW
targeted refinement
        ↓
browser-runtime-inspector
        ↓
visual-qa
        ↓
delivery
```

Use the reference as primary visual evidence. Analyze structure, spacing, proportions, typography, hierarchy, color, borders, radii, imagery, alignment, responsive implications, and interaction patterns before implementation. For close reproduction, preserve fidelity and do not redesign the reference unnecessarily. Avoid protected branding or assets unless they were supplied or authorized.

## No reference provided

```text
User brief
        ↓
art-direction
        ↓  ART_DIRECTION_BRIEF
frontend-design
        ↓
implementation
        ↓
browser-runtime-inspector
        ↓
visual-qa
        ↓
anti-ai-ui-review
        ↓
targeted refinement
        ↓
browser-runtime-inspector
        ↓
visual-qa
        ↓
delivery
```

Use product purpose, audience, content, brand information, constraints, and existing design-system evidence. Do not block merely because a reference is absent. Do not default to a generic SaaS hero, purple gradient, floating dashboard, endless rounded cards, identical feature grids, gradient text, excessive glass effects, or component-demo composition unless the context makes the choice intentional.

## Handoff contracts

### Design reference

`design-reference-analyzer` produces `DESIGN_REFERENCE_BRIEF`. It records evidence, inference, transferable principles, reference-specific elements not to copy, and risks of direct imitation. It does not implement.

### Art direction

`art-direction` consumes the project brief and optional `DESIGN_REFERENCE_BRIEF`, then produces `ART_DIRECTION_BRIEF` with concrete product, audience, task, typography, layout, color, imagery, spacing, shape, interaction, motion, memorable-device, and avoidance decisions.

### Implementation

`frontend-design` consumes requirements and the available briefs. Preserve the existing framework, architecture, design tokens, components, and styling approach unless they prevent the requested result. `ui-ux-pro-max` is advisory for accessibility, usability, responsive behavior, and component conventions.

### Rendered QA

`browser-runtime-inspector` provides technical browser evidence. `visual-qa` owns the objective rendered verdict and produces `VISUAL_QA_REPORT`. Objective defects come before subjective polish.

### Anti-generic review

`anti-ai-ui-review` runs after objective visual defects are mostly resolved. It produces `ANTI_AI_UI_REVIEW`, judges context rather than banning common components, and prioritizes only a few high-impact corrections.

## Precedence

Use: explicit user requirements → existing product/brand system → `DESIGN_REFERENCE_BRIEF` → `ART_DIRECTION_BRIEF` → `frontend-design` principles → generic `ui-ux-pro-max` recommendations. Accessibility and functional usability are mandatory exceptions.

## Lightweight routing

- One text-color or copy change: make the scoped change; no full pipeline.
- One overflow or CSS geometry bug: `browser-runtime-inspector → visual-qa`.
- One supplied component: `frontend-design → targeted browser verification`.
- Existing page visual cleanup: `browser-runtime-inspector → visual-qa → anti-ai-ui-review → targeted refinement → re-test`.
- New landing page, dashboard, major redesign, or screenshot recreation: use the applicable full branch.

## Finite refinement

After corrections, rerun `browser-runtime-inspector → visual-qa` on every previously failing viewport or state. A second anti-AI pass is appropriate only when the visual direction changed materially. Stop after one strong refinement pass, or a second when substantial issues remain, unless the user explicitly requests further iteration.
