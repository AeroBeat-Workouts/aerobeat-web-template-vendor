# AeroBeat Web Vendor Template

Use this template for AeroBeat-authored `aerobeat-web-vendor-*` adapter repos.

## Responsibility

Vendor adapter repos isolate significant, optional, heavyweight, or change-prone third-party runtime dependencies behind a narrow AeroBeat-owned public API. They normalize provider output before product/domain repos consume it.

This template is not for forked upstream repos. If a repo is a direct upstream fork, preserve the upstream shape and put AeroBeat service contracts in the wrapper repo above it.

## Folder Shape

Use the standard package layout unless preserving an upstream fork:

```text
/
  README.md
  LICENSE.md
  .gitignore
  package.json
  package-lock.json
  src/
    index.js
    adapters/
    models/
  .testbed/
    README.md
    package.json
    package-lock.json
    test/
    demo/
    scenes/
    debug-data/
    playwright.config.js
  scripts/
  fixtures/
  assets/
  docs/
    decisions/
  .github/
    workflows/
  .plans/
  .beads/
```

## Boundary Rules

- Expose stable AeroBeat shapes and names from public exports.
- Keep provider DTOs, vendor-native object graphs, model lifecycle details, and auth/config quirks behind the adapter boundary.
- Use `aerobeat-web-contracts` for shared shapes that cross repo boundaries.
- Product/domain repos should consume wrapper services such as `aerobeat-web-cv`, not raw vendor APIs, unless a later plan explicitly approves the import.

## First CV Vendor Posture

The first planned CV vendor is MoveNet/TensorFlow.js. `aerobeat-web-vendor-movenet` should provide worker-facing adapter exports for `aerobeat-web-cv`; `aerobeat-web-cv` remains the camera/CV singleton and normalized pose-frame owner.

## Validation

Run these commands before handoff:

```bash
npm run check
npm test
npm run test:browser
```

Placeholder validators enforce the same JSDoc/no-escape, public import-boundary, component-only scene, and Playwright console-noise posture as standard packages.

When a vendor adapter owns browser-visible demos or camera/CV validation, add `npm run testbed:serve` with host, port, cache-busting/version display, QR/link output, served roots, and HTTPS or secure-context behavior for Tailscale devices.
