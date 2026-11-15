# Agent guidance

## Repository status

- This repository currently contains planning and design Markdown only; there is no frontend, backend, package manifest, test suite, build script, or OpenCode project configuration yet.
- Do not claim that a build, lint, typecheck, or test command works until the corresponding application/tooling is added.
- Treat `README.md`, `REQUIREMENTS.md`, `FIGMA_AND_ANGULAR_MASTER_SPEC.md`, `ANGULAR_COMPONENTS_AND_FLOW.md`, `DESIGN_SYSTEM.md`, `ARCHITECTURE.md`, `ROADMAP_AND_TASKS.md`, and `WORKFLOW_AND_GIT.md` as planning documents, not executable sources.

## Product constraints

- The database requirement is Microsoft SQL Server; its schema is expected to be supplied by Paco. Do not invent or migrate the schema without reconciling it with that source.
- The domain must support recurrent trips, one-off/event trips, users acting as driver and/or passenger, Tajamar courses/events, reservations, and an event-trip waitlist.
- The waitlist is currently planned for Sprint 4; do not silently add it to Sprint 2/3 behavior unless the task explicitly asks for it.

## Technology decision to verify

- The planning files conflict: `ARCHITECTURE.md`/`README.md` present React as the recommendation, while the later design specification is explicitly Angular. Before scaffolding code, confirm Angular as the team decision and update the stale planning references; do not mix React and Angular conventions.
- The proposed backend alternatives are .NET 8 Web API/EF Core or Node.js/TypeScript. Select one before implementation and document the decision; neither backend exists in this checkout.

## Design-to-code workflow

- Keep Figma work linked from `design/FIGMA.md` (and export key screenshots/assets into `design/` when that directory is created).
- Preserve the Figma component mapping: reusable buttons, inputs, badges, cards, navbar, modals, and booking action states should map to reusable Angular shared components rather than page-specific duplicates.
- For every trip/event/booking screen, account for loading, error, empty, available, full, and already-booked states; the UI has distinct reserve versus event-waitlist actions.

## Git workflow

- Use `develop` as the integration branch and `main` only for stable delivery; feature branches should be named `feature/frontend-*`, `feature/backend-*`, or `feature/sql-*`.
- Do not commit directly to `main` or `develop`. Merge through a PR with at least one teammate review and working verification once code exists.
- Use focused Conventional Commits such as `feat(frontend): ...`, `fix(backend): ...`, and `docs: ...`.
- Coordinate API contract changes with the frontend before merging; the documented REST paths are proposals and must not be treated as implemented endpoints.

## Documentation

- Project analysis and requirements are expected in Markdown. Update the relevant planning document when changing requirements, routes, component responsibilities, stack, or team workflow.
