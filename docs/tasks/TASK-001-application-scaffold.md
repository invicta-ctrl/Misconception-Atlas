# TASK-001 — Application Scaffold

## Document control

- Project: Misconception Atlas
- Task ID: `TASK-001`
- Status: accepted
- Accepted specification: `docs/specs/MA-MVP-001.md`
- Implementation branch: `feat/application-scaffold`
- Owner: Earl Adriano
- Date accepted: 2026-07-15

## INTENT

SOFTWARE_FEATURE

## OBJECTIVE

Create the smallest verified Next.js application foundation needed for later Misconception Atlas vertical slices, without implementing GPT-5.6 analysis, deterministic misconception logic, or production data handling.

## TARGET

The `invicta-ctrl/Misconception-Atlas` repository after the project-foundation documentation is reviewed and merged.

## AUTHORITATIVE SOURCES

1. `AGENTS.md`
2. `docs/specs/MA-MVP-001.md`
3. `PROJECT_STATUS.md`
4. `docs/WORK_CONTINUATION.md`
5. This accepted task brief

## IN SCOPE

- Scaffold a Next.js application using React and TypeScript.
- Configure Tailwind CSS.
- Configure ESLint and formatting behavior.
- Configure Vitest with one meaningful smoke test.
- Configure Playwright with one application-load smoke test.
- Add type-check, test, lint, build, and end-to-end scripts.
- Add `.env.example` containing variable names only and no secrets.
- Establish clear source folders for app UI, domain logic, OpenAI adapters, fixtures, schemas, and tests.
- Create a static teacher-facing landing/dashboard shell using sample text only.
- Display the project name, Build Week category, supported MVP domain, privacy boundary, and implementation-status notice.
- Update README setup and verification instructions to match the working scaffold.
- Update `PROJECT_STATUS.md` and `docs/WORK_CONTINUATION.md` with exact evidence after completion.

## OUT OF SCOPE

- Live OpenAI API calls.
- GPT-5.6 prompts or analysis schemas.
- Image upload processing.
- Deterministic slab calculations.
- Misconception clustering.
- Teacher override behavior.
- Production fixture images.
- Authentication.
- Database or persistent storage.
- Vercel deployment.
- Devpost media or video production.
- Any academic subject or problem family beyond the accepted description text.

## CONSTRAINTS

- Use the accepted stack and stable supported package versions available at implementation time.
- Do not expose or commit secrets.
- Do not add packages unrelated to the scaffold.
- Keep the visual shell accessible, responsive, and deliberately simple.
- Do not imply that analysis features already work.
- Do not modify the accepted specification except through a separately approved amendment.
- Do not merge or delete branches without explicit owner approval.

## EXPECTED FILES OR MODULES

Exact paths may follow current Next.js conventions, but the result must clearly separate:

- application routes and layout;
- reusable UI components;
- future domain logic boundary;
- future OpenAI adapter boundary;
- future fixture boundary;
- schemas;
- unit tests;
- end-to-end tests;
- configuration and environment example.

## DELIVERABLES

- Runnable local Next.js application.
- Static teacher-facing project shell.
- Verified quality scripts.
- Smoke tests.
- Updated README.
- Updated project status and continuation record.
- Completion report mapping evidence to the acceptance criteria below.

## VERIFICATION

Run and record the exact output of:

- dependency installation from a clean state;
- lint command;
- type-check command;
- focused unit test command;
- full unit test command;
- production build command;
- Playwright smoke test;
- secret and generated-file review;
- manual desktop and tablet viewport check.

## ACCEPTANCE CRITERIA

- TASK-AC-001: A clean checkout can install dependencies using the documented command.
- TASK-AC-002: The development application starts and renders the Misconception Atlas shell.
- TASK-AC-003: The shell accurately states that the project is an Education submission focused on two-way slab reasoning.
- TASK-AC-004: The shell clearly states that analysis features are not yet implemented.
- TASK-AC-005: The interface remains usable at desktop and tablet viewport widths.
- TASK-AC-006: The repository contains explicit future boundaries for domain logic, OpenAI integration, schemas, and fixtures without implementing them.
- TASK-AC-007: `.env.example` contains no secret values.
- TASK-AC-008: Linting passes.
- TASK-AC-009: Type checking passes.
- TASK-AC-010: Unit tests pass.
- TASK-AC-011: Production build passes.
- TASK-AC-012: The Playwright application-load workflow passes.
- TASK-AC-013: README setup and verification instructions work from a clean checkout.
- TASK-AC-014: Project status and continuation records contain exact commands, outcomes, changed files, limitations, and rollback checkpoint.

## STOP CONDITIONS

Stop and request an amendment or owner decision when:

- the scaffold requires a production database, authentication, or live model integration;
- a package or framework change would depart materially from `MA-MVP-001`;
- required verification fails for an unexplained reason;
- existing repository work conflicts with this task;
- a secret or real student record is discovered;
- the proposed implementation expands beyond the static application foundation.

## ACCEPTANCE RECORD

- Accepted by: Earl Adriano
- Acceptance date: 2026-07-15
- Conditions: Implement only after PR #1 is merged. Keep live GPT-5.6 integration, image analysis, deterministic slab logic, clustering, persistence, authentication, deployment, and Devpost media outside this task.