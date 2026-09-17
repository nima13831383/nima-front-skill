# Visual Testing Protocol

Use this protocol for substantial frontend work. Not every state applies to every project; test meaningful states that actually exist and do not fabricate product behavior solely for the audit.

## Evidence rule

Inspect the rendered interface in a real browser. Source code, a successful build, passing tests, Lighthouse, and a clean console are supporting evidence only. If browser or screenshot tooling is unavailable after reasonable attempts, report visual verification as `UNVERIFIED`.

## Preflight

1. Inspect the existing project for its documented start command, browser harness, route, framework, and viewport conventions.
2. Start the application without replacing its architecture or installing dependencies without a meaningful reason.
3. Open the real route in the available browser. Record the final URL, page errors, console errors, and whether fonts/assets resolve.
4. Use `browser-runtime-inspector` for DOM state, computed styles, bounding boxes, overflow, stacking, interaction states, and technical screenshots. Do not expose credentials, cookies, tokens, customer data, or sensitive page text.

## VIEWPORT MATRIX

| Viewport | Purpose |
| --- | --- |
| 320px | Narrowest practical phone: clipping, overflow, tiny controls, wrapping |
| 375px or 390px | Standard phone layout |
| 430px | Large phone behavior |
| 768px | Tablet breakpoint and navigation/grid transition |
| 1024px | Small laptop and breakpoint edge cases |
| 1440px | Normal desktop composition |
| 1728px or 1920px | Wide desktop max-width, whitespace, and oversized-type behavior when relevant |

Test the widths relevant to the implementation, including at least mobile, tablet, and desktop for substantial responsive work.

## BREAKPOINT EDGE TESTING

Inspect just above and below important project breakpoints when a layout changes near them. For a 768px transition, test 767px and 769px when there is a reason to suspect a breakpoint issue. Also check the implementation’s actual custom breakpoints rather than blindly relying on this preset matrix.

At every relevant size check horizontal overflow, clipped content, grids, scrollbars, navigation, wrapping, button dimensions and placement, forms, cards, images, hero proportions, text collisions, section spacing, sticky/fixed elements, dialogs, footer, edge padding, and overall composition.

## SCREENSHOTS

Capture representative viewport screenshots for mobile, tablet, and desktop. Use viewport screenshots for fold composition, navigation, dialogs, breakpoint issues, and state testing. Use full-page screenshots for section rhythm, repetition, footer, spacing consistency, and overall composition. Wait for fonts and transitions to settle. Keep screenshots temporary unless the user requests deliverables.

## INTERACTION STATE TESTING

Test only meaningful states that exist in the product:

- Navigation: menu closed/open, mobile menu, dropdown, sticky behavior.
- Buttons: hover, focus, active, disabled where relevant.
- Forms: empty, focused, filled, invalid, error, disabled, and success when implemented.
- Tabs: default and alternate tabs.
- Accordions: collapsed and expanded.
- Dropdowns: closed and open, including viewport fit.
- Modals/dialogs: closed and open, viewport fit, background scroll behavior.
- Drawers: closed and open.
- Tables: narrow viewport, long values, and overflow behavior.
- Interactive cards: long titles/descriptions, missing optional imagery where realistic, hover where applicable.
- Loading, empty, error, and success states when they exist or are important to the requested flow.

After each interaction, assert the expected state and inspect the visible result again. Check Escape, outside click, focus return, and post-close state for overlays when applicable.

## CONTENT STRESS TESTING

When useful, exercise realistic variation: long headings, long names, long navigation labels, multi-line button text, long table values, missing optional images, and unusually long paragraphs. This is inspection only; do not permanently replace production content unless required by the task.

## DOM / COMPUTED STYLE INSPECTION

When a visual issue appears, diagnose rather than guessing. Inspect bounding boxes, computed width/height, margin, padding, display, position, overflow, flex/grid behavior, z-index, stacking contexts, actual font, line-height, and viewport bounds. Use `browser-runtime-inspector` to locate the likely CSS owner and repeat the same measurement after a fix.

## CONSOLE / RUNTIME CHECKS

Record console errors, page errors, and obvious runtime failures affecting the rendered route. A lack of console errors does not establish visual correctness. Separate technical runtime findings from visual layout findings in the `VISUAL_QA_REPORT`.

## OVERFLOW AND NAVIGATION

Compare `document.documentElement.scrollWidth` with `clientWidth` at relevant viewports. Check whether controls, popovers, dialogs, sticky headers, and fixed actions remain inside the viewport. Verify responsive navigation transitions, accessible focus visibility, and usable touch targets.

## RETEST AFTER FIXES

After corrections, capture fresh evidence. Reinspect every viewport and state that previously failed, plus representative mobile, tablet, and desktop views. Do not infer that a fix worked from source changes alone. Pass only when the rendered evidence supports the result; otherwise report `UNVERIFIED` or the remaining defects.
