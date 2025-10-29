## Context Engineering Starter (quick_context)

A minimal, opinionated starter for building projects with strong context-engineering practices and smooth deployment to Netlify via GitHub. This repo includes Cursor rules, lightweight docs, and structure guidance to keep implementation focused and reviewable.

### What’s inside
- `.cursor/rules/*` — repo-wide rules for architecture, generation, style, and workflow
- `Docs/` — lightweight project guides: Project Structure, Implementation Notes, UI/UX, Bug Tracking
- `PRD.md` — product requirements (source of truth above rules)
- `context_eng.md` — context-engineering principles and collaboration patterns

### Getting started
1) Create a new GitHub repo using this as a template or push this repo to GitHub.
2) Connect GitHub repo to Netlify and select the appropriate build command and publish directory (see Deployment below).
3) Fill in project specifics under Docs and PRD.

### Deployment (Netlify via GitHub)
- Connect your GitHub repository in Netlify.
- Configure:
  - Build command: add when your framework is chosen (e.g., `npm run build`)
  - Publish directory: framework-dependent (e.g., `dist`, `build`, or framework default)
  - Environment variables: add in Netlify UI under Site settings → Environment variables
- Optional: add `netlify.toml` for consistent CI/CD across environments.

Example `netlify.toml` to start from:
```toml
[build]
  command = "npm run build"
  publish = "dist"

[[plugins]]
  package = "@netlify/plugin-lighthouse"
```

### Cursor rules (high-level summary)
- Architecture (`arch.mdc`):
  - UI ↔ State ↔ Services ↔ Infra; do not skip boundaries
  - Local-first state; avoid global mutable singletons
  - DTOs at boundaries; IO behind interfaces in `services/`
  - No secrets in code; validate all external inputs
- Generate (`generate.mdc`):
  - Minimal diffs, include types/docstrings for public APIs
  - Fail fast with typed errors; log context, not secrets
  - Update README/docs when adding/altering public APIs
  - Prefer simple first; annotate hotspots
- Style (`style.mdc`):
  - TypeScript strict, ESLint+Prettier
  - Naming: verbs for functions; is/has/should for booleans
  - React: functional components, hooks, Tailwind/CSS Modules
  - JSDoc/TSDoc for exported items
- Workflow (`workflow.mdc`):
  - Branch naming: `feat/*`, `fix/*`, `chore/*`
  - Conventional Commits; PRs link PRD/issue with checklist
  - Tests for new logic, data access (happy+failure), and key UI flows

### Project structure (from `Docs/Project_Structure.md`)
- `/src` — app code
- `/tests` — unit/integration tests; mirror source paths
- `/scripts` — CLIs/one-off tasks
- `/infra` — IaC, Docker, CI configs
- `/docs` — additional guides

### Implementation workflow
1) Create a branch (see Workflow rules)
2) Implement in small, reviewable edits; include rationale for non-trivial changes
3) Update docs when adding public APIs or meaningful behaviors
4) Ensure lint/tests pass; include screenshots for UI changes in PR

### Bug tracking (lightweight)
Use `Docs/Bug_Tracking.md` template for consistency: Title, Environment, Steps, Expected, Actual, Logs/Screens, Severity, Owner.

### Context engineering principles
See `context_eng.md` for process expectations: favor working code with tests, small diffs, explicit trade-offs, and typed outputs. If rules conflict, follow: `PRD.md` > `arch.mdc` > `style.mdc`.

### Environment variables
- Store secrets outside code; use `.env` locally and Netlify environment variables in production.
- This repo includes `.env` in `.gitignore`. Provide a safe `/.env.example` when you add variables.

### What you should customize now
- PRD in `PRD.md`: define scope, success metrics, constraints
- Choose stack: framework, package manager, test runner, formatter configs
- Netlify: set build command, publish directory, environment variables; add `netlify.toml`
- Lint/format: add ESLint/Prettier config and enable TS Strict if using TS
- CI: add GitHub Actions or Netlify CI settings for lint/build/test
- Project structure: scaffold `/src`, `/tests`, and initial modules
- UI/UX doc: define flows, states, and accessibility goals in `Docs/UI_UX_doc.md`
- Implementation notes: record decisions/risks in `Docs/Implementation.md`

### Conventional commit examples
- feat: add auth service with typed DTOs
- fix: correct error mapping in user API
- chore: configure Netlify build and env vars
- docs: document API usage in README

### License
Add your license of choice (MIT, Apache-2.0, etc.).
