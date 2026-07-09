# PR-001 Bootstrap Blueprint

## Objective
Create a production-ready monorepo foundation.

## Required Stack
- pnpm workspaces
- Turborepo
- Vite
- React
- TypeScript
- Biome
- Vitest
- Changesets
- GitHub Actions

## Workspace
apps/
  writing-company-demo/
packages/
  core/
  shared/
  progress/
  react/
  media/
  timeline/
  renderer/

## Acceptance Criteria
- Clean clone builds successfully.
- pnpm install && pnpm build succeeds.
- Lint passes.
- Tests pass.
- Demo app renders.
- Zero engine implementation in this PR.

## Architectural Constraints
- Core has no browser dependency.
- No React outside @snf/react.
- No GSAP dependency.
- No Lottie dependency.
- No runtime logic.
