# Nima Front Skill

Nima Front Skill is an orchestration Skill for Codex. It coordinates design-reference analysis, art direction, frontend implementation, real-browser inspection, responsive QA, interaction-state inspection, visual QA, anti-generic design review, defect fixing, and final visual re-testing.

It is the primary Skill in this repository, but it is not a replacement for the specialist Skills. The main package coordinates them by Skill name.

## Download

### Nima Front

Installable Skill: [`dist/skill.zip`](https://raw.githubusercontent.com/nima13831383/nima-front-skill/main/dist/skill.zip)

Repository: <https://github.com/nima13831383/nima-front-skill>

Repository ZIP: <https://github.com/nima13831383/nima-front-skill/archive/refs/heads/main.zip>

### Bundled dependency packages

The four custom specialist Skills are separately installable from this repository:

- [`design-reference-analyzer.zip`](https://raw.githubusercontent.com/nima13831383/nima-front-skill/main/dist/dependencies/design-reference-analyzer.zip)
- [`art-direction.zip`](https://raw.githubusercontent.com/nima13831383/nima-front-skill/main/dist/dependencies/art-direction.zip)
- [`anti-ai-ui-review.zip`](https://raw.githubusercontent.com/nima13831383/nima-front-skill/main/dist/dependencies/anti-ai-ui-review.zip)
- [`visual-qa.zip`](https://raw.githubusercontent.com/nima13831383/nima-front-skill/main/dist/dependencies/visual-qa.zip)

## Bundled Custom Skills

These Skills were created specifically for the Nima Front workflow and are distributed as separate installable packages in this repository. They are not nested inside the main `nima-front` package.

| Skill | Purpose | Download |
|---|---|---|
| `design-reference-analyzer` | Analyze screenshots and references and create `DESIGN_REFERENCE_BRIEF` | [ZIP](https://raw.githubusercontent.com/nima13831383/nima-front-skill/main/dist/dependencies/design-reference-analyzer.zip) |
| `art-direction` | Create `ART_DIRECTION_BRIEF` before implementation | [ZIP](https://raw.githubusercontent.com/nima13831383/nima-front-skill/main/dist/dependencies/art-direction.zip) |
| `anti-ai-ui-review` | Detect generic or template-like frontend design | [ZIP](https://raw.githubusercontent.com/nima13831383/nima-front-skill/main/dist/dependencies/anti-ai-ui-review.zip) |
| `visual-qa` | Inspect rendered frontend quality and responsiveness | [ZIP](https://raw.githubusercontent.com/nima13831383/nima-front-skill/main/dist/dependencies/visual-qa.zip) |

## External Skill Dependencies

External Skills are not owned or redistributed by this repository. Install them from their original upstream sources and follow their own licenses.

### frontend-design

Role: Primary creative frontend implementation.

Official source: <https://github.com/anthropics/skills/tree/main/skills/frontend-design>

Author: Anthropic

Status: **External dependency — not bundled.**

### browser-runtime-inspector

Role: Browser inspection, DOM and computed-style inspection, runtime diagnostics, screenshots, and geometry analysis.

Source: <https://github.com/nima13831383/playwright-browser-inspector>

Installable source: <https://github.com/nima13831383/playwright-browser-inspector/blob/main/README.md>

Status: **External repository — not bundled here.** The installed local Skill was verified against this upstream repository at the same `main` commit.

### ui-ux-pro-max

Role: Optional supporting UX, accessibility, design-system, typography, and interaction guidance.

Source: **Source currently unverified.**

Status: **Optional supporting dependency — not redistributed by this repository.** Do not assume ownership or infer an upstream URL.

## Dependency model

`nima-front` does not contain every dependency inside the main `skill.zip`.

- The main Skill is the orchestrator.
- Custom dependencies are separately downloadable from this same repository under `dist/dependencies/`.
- External dependencies must be installed from their original upstream sources.
- `ui-ux-pro-max` is optional and must be installed separately if its source is available in the user’s environment.

The machine-readable summary is available in [`dependencies.json`](dependencies.json).

## Installation layout

Skill directory names must remain exactly these names because `nima-front` references them by Skill name.

```text
~/.codex/skills/
├── nima-front/
├── frontend-design/
├── design-reference-analyzer/
├── art-direction/
├── anti-ai-ui-review/
├── visual-qa/
├── browser-runtime-inspector/
└── ui-ux-pro-max/        # optional / if available
```

## Windows installation

For each bundled ZIP:

1. Download the package from the links above.
2. Extract the ZIP into `%USERPROFILE%\.codex\skills` — the parent directory, not into a same-named child directory.
3. Confirm the result has this shape:

```text
C:\Users\<username>\.codex\skills\visual-qa\SKILL.md
```

Do not extract into `%USERPROFILE%\.codex\skills\visual-qa` when the archive already contains a `visual-qa/` root, or you may create the incorrect nested path `visual-qa\visual-qa\SKILL.md`.

PowerShell example for a downloaded bundled package:

```powershell
$skillsPath = Join-Path $HOME '.codex\skills'
Expand-Archive -LiteralPath .\visual-qa.zip -DestinationPath $skillsPath -Force
```

Install the main package the same way:

```powershell
$skillsPath = Join-Path $HOME '.codex\skills'
Expand-Archive -LiteralPath .\skill.zip -DestinationPath $skillsPath -Force
```

Reload or restart Codex Skill discovery after installation.

## Recommended Setup

Install in this order:

1. `frontend-design` from Anthropic
2. `browser-runtime-inspector` from its upstream repository
3. `design-reference-analyzer` from the bundled ZIP
4. `art-direction` from the bundled ZIP
5. `anti-ai-ui-review` from the bundled ZIP
6. `visual-qa` from the bundled ZIP
7. optional `ui-ux-pro-max` if its source is available
8. `nima-front` from the main ZIP

Then reload Codex Skill discovery.

## What it coordinates

Nima Front supports:

- implementation from screenshots, Figma references, images, URLs, or existing sites
- implementation when no visual reference exists
- project-specific art direction
- responsive implementation across relevant breakpoints
- browser-based visual inspection
- multi-viewport responsive QA
- interaction and UI-state QA
- breakpoint-edge testing
- anti-AI and anti-template design review
- targeted refinement
- mandatory visual re-testing after fixes

A substantial frontend task is not considered complete until the rendered interface has been visually inspected in a real browser. The Skill reports `Final verification: PASSED` only after browser evidence exists and the post-fix retest succeeds. If browser verification cannot run, it reports `Verification: UNVERIFIED` with the reason.

## Workflow

### With a visual reference

```text
design-reference-analyzer
        ↓
art-direction
        ↓
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
refinement
        ↓
browser-runtime-inspector
        ↓
visual-qa
        ↓
delivery
```

### Without a visual reference

```text
art-direction
        ↓
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
refinement
        ↓
browser-runtime-inspector
        ↓
visual-qa
        ↓
delivery
```

Small fixes do not necessarily activate the entire pipeline. Routing should match the scope and risk of the change while preserving the real-browser gate for substantial frontend work.

## Visual testing

The default viewport matrix is 320px, 375/390px, 430px, 768px, 1024px, 1440px, and 1728/1920px when relevant.

QA should include breakpoint edges, mobile menu states, hover/focus states, forms, dropdowns, modals, drawers, tabs, and loading/error/empty states when present. Inspect overflow, clipping, typography, image crops, geometry, stacking, and console/runtime issues. See [`references/visual-testing.md`](references/visual-testing.md) for the detailed workflow.

## Definition of Done

Substantial frontend work requires successful rendering, real-browser inspection, mobile/tablet/desktop QA, relevant interaction states, visual QA, high-impact anti-AI review, fixes, and a final browser re-test.

```text
Build success != visual verification.
Typecheck success != visual verification.
Code inspection != visual verification.
```

If browser verification cannot run:

```text
Verification: UNVERIFIED
```

## Licensing

Nima Front and the bundled custom Skills in this repository are released under the MIT License in [`LICENSE`](LICENSE). External dependencies are not covered by this repository’s MIT License; their upstream licenses and attribution requirements remain in force.

## Project status

This repository contains the Nima Front orchestrator and four bundled custom dependency packages. It does not automatically install external dependencies, and it does not claim ownership of `frontend-design`, `browser-runtime-inspector`, or `ui-ux-pro-max`.
