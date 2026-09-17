# Nima Front Skill

Nima Front Skill is an orchestration Skill for Codex that coordinates frontend design, implementation, browser inspection, responsive visual QA, anti-generic design review, and final verification.

It is a control plane for substantial frontend work. It routes work to specialist Skills instead of replacing them or copying their full instructions.

## Download

### Latest Skill Package

GitHub CLI was not available when this repository was published, so no Release URL is claimed. The installable package is available at [`dist/skill.zip`](dist/skill.zip) in the repository.

### Repository ZIP

<https://github.com/nima13831383/nima-front-skill/archive/refs/heads/main.zip>

`skill.zip` is the installable Skill package. The repository ZIP contains the Skill, documentation, license, and publishing files.

## What it coordinates

Nima Front supports:

- frontend implementation from screenshots, Figma references, images, URLs, or existing sites
- frontend implementation when no visual reference exists
- project-specific art direction
- responsive implementation across relevant breakpoints
- browser-based visual inspection
- multi-viewport responsive QA
- interaction and UI-state QA
- breakpoint-edge testing
- anti-AI and anti-template design review
- targeted refinement
- mandatory visual re-testing after fixes

A substantial frontend task is not considered complete until the rendered interface has been visually inspected in a real browser. The Skill reports `Final verification: PASSED` only after the required browser evidence exists and the post-fix retest succeeds. If browser verification cannot run, it reports `Verification: UNVERIFIED` with the reason.

## Skill Dependencies

| Skill | Role | Source |
|---|---|---|
| `frontend-design` | Primary frontend design and implementation | [Anthropic Skills](https://github.com/anthropics/skills/tree/main/skills/frontend-design) |
| `design-reference-analyzer` | Extract transferable design language from references | [Nima repository](https://github.com/nima13831383/nima-design-reference-analyzer) |
| `art-direction` | Create project-specific visual direction before implementation | [Nima repository](https://github.com/nima13831383/nima-art-direction) |
| `anti-ai-ui-review` | Detect generic or AI-looking UI patterns | [Nima repository](https://github.com/nima13831383/nima-anti-ai-ui-review) |
| `visual-qa` | Rendered visual and responsive QA | [Nima repository](https://github.com/nima13831383/nima-visual-qa) |
| `ui-ux-pro-max` | Supporting UX, accessibility, and design knowledge | Local dependency — source currently unpublished |
| `browser-runtime-inspector` | Browser, DOM, runtime, and geometry inspection | [nima13831383/playwright-browser-inspector](https://github.com/nima13831383/playwright-browser-inspector) |

Nima Front Skill orchestrates these Skills; it does not bundle or redistribute them unless explicitly present in this repository.

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

Small fixes do not necessarily activate the entire pipeline. The routing should match the scope and risk of the change while preserving the real-browser verification gate for substantial frontend work.

## Visual testing

The default viewport matrix is:

- 320px
- 375px or 390px
- 430px
- 768px
- 1024px
- 1440px
- 1728px or 1920px when relevant

Testing should include breakpoint edges, mobile menu states, hover and focus states, forms, dropdowns, modals, drawers, tabs, and loading/error/empty states when present. Inspect overflow, clipping, typography, image crops, geometry, stacking, and console/runtime issues. Use the detailed workflow in [`references/visual-testing.md`](references/visual-testing.md).

## Installation

### Manual installation from GitHub

Clone the repository:

```powershell
git clone https://github.com/nima13831383/nima-front-skill.git
```

Copy only the installable Skill files into Codex:

```powershell
$skillPath = Join-Path $HOME '.codex\skills\nima-front'
New-Item -ItemType Directory -Force $skillPath | Out-Null
Copy-Item -Recurse -Force .\nima-front-skill\SKILL.md $skillPath
Copy-Item -Recurse -Force .\nima-front-skill\agents $skillPath
Copy-Item -Recurse -Force .\nima-front-skill\references $skillPath
```

This keeps repository-only files such as `.git`, `README.md`, `LICENSE`, and `dist` out of the installed Skill directory.

### ZIP installation

1. Download [`dist/skill.zip`](dist/skill.zip) from the repository, or use the repository ZIP above.
2. Extract it into `~/.codex/skills/` so the package creates `~/.codex/skills/nima-front/`.
3. Reload or restart Codex Skill discovery.

The ZIP contains only the installable Skill package: `SKILL.md`, `agents/openai.yaml`, and the three reference files.

## Installing Dependencies

Nima Front is an orchestrator and works best with the full dependency stack installed. Skill names must remain unchanged because the orchestrator references them by name.

Expected Codex layout:

```text
~/.codex/skills/
├── nima-front/
├── frontend-design/
├── design-reference-analyzer/
├── art-direction/
├── anti-ai-ui-review/
├── visual-qa/
├── ui-ux-pro-max/
└── browser-runtime-inspector/
```

### Individual install links

| Dependency | Repository or source | Package status |
|---|---|---|
| `frontend-design` | [Anthropic Skills](https://github.com/anthropics/skills/tree/main/skills/frontend-design) | Install from upstream |
| `design-reference-analyzer` | [nima-design-reference-analyzer](https://github.com/nima13831383/nima-design-reference-analyzer) | Repository ZIP and `dist/skill.zip`; Release pending |
| `art-direction` | [nima-art-direction](https://github.com/nima13831383/nima-art-direction) | Repository ZIP and `dist/skill.zip`; Release pending |
| `anti-ai-ui-review` | [nima-anti-ai-ui-review](https://github.com/nima13831383/nima-anti-ai-ui-review) | Repository ZIP and `dist/skill.zip`; Release pending |
| `visual-qa` | [nima-visual-qa](https://github.com/nima13831383/nima-visual-qa) | Repository ZIP and `dist/skill.zip`; Release pending |
| `ui-ux-pro-max` | Local dependency | Source currently unpublished; do not guess or redistribute |
| `browser-runtime-inspector` | [playwright-browser-inspector](https://github.com/nima13831383/playwright-browser-inspector) | Use the verified upstream repository |

Each custom repository contains its own `dist/skill.zip`. Until a GitHub Release is created, use the repository ZIP or download the package from the repository’s `dist` path. No install-all helper is included because the custom repository targets are not yet public and third-party provenance is intentionally not guessed.

## Usage examples

### Without a reference

```text
Use $nima-front.

Build a responsive personal portfolio.
Use a restrained Swiss-inspired visual direction.
Do full browser QA and visual verification before delivery.
```

### With a reference

```text
Use $nima-front.

Implement the attached design as faithfully as possible.
Preserve its typography, spacing, hierarchy and proportions.
Perform the complete visual QA workflow before delivery.
```

### Existing UI cleanup

```text
Use $nima-front.

Inspect this existing frontend, fix responsive and visual issues,
remove generic AI-looking patterns, then visually re-test it.
```

## Definition of Done

Substantial frontend work requires:

- successful rendering
- real-browser inspection
- mobile QA
- tablet QA
- desktop QA
- relevant interaction states
- visual QA
- high-impact anti-AI review
- fixes for material defects
- a final browser re-test

```text
Build success != visual verification.
Typecheck success != visual verification.
Code inspection != visual verification.
```

If browser verification cannot run:

```text
Verification: UNVERIFIED
```

## Project status

This is an orchestration Skill. It does not automatically install its dependencies. Four custom dependencies are prepared in local publishing workspaces, but their GitHub repositories still require manual creation because GitHub CLI is unavailable in the current environment. `ui-ux-pro-max` remains a local dependency with currently unpublished source because its provenance could not be verified. Missing dependencies may reduce or prevent parts of the workflow; the agent should report that limitation rather than pretending the full pipeline ran.

## License

Nima Front Skill is released under the [MIT License](LICENSE). Dependency Skills are referenced by name and are not redistributed by this repository unless explicitly included here.
