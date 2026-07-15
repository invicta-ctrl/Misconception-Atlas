# Misconception Atlas

> Turn student work into an evidence-linked map of class-wide misconceptions, pinpoint the first wrong reasoning step, and generate targeted interventions teachers can act on.

Misconception Atlas is an **Education** submission for OpenAI Build Week. The Build Week MVP is a teacher-facing web application focused deeply on one Civil Engineering problem family: two-way reinforced-concrete slab geometry and effective-span reasoning.

## Current status

The project is in specification and repository-foundation setup. Product implementation has not started.

- Accepted specification: [`docs/specs/MA-MVP-001.md`](docs/specs/MA-MVP-001.md)
- Current status: [`PROJECT_STATUS.md`](PROJECT_STATUS.md)
- Continuation record: [`docs/WORK_CONTINUATION.md`](docs/WORK_CONTINUATION.md)
- Build Week requirements: [`docs/BUILD_WEEK_REQUIREMENTS.md`](docs/BUILD_WEEK_REQUIREMENTS.md)
- Repository rules: [`AGENTS.md`](AGENTS.md)

## Intended MVP

A teacher will be able to analyze anonymized or synthetic student solution images and receive:

- ordered reasoning-step reconstruction;
- the earliest supported root misconception;
- evidence tied to the submitted work;
- deterministic checks for supported engineering calculations;
- class-level misconception clusters;
- teacher confirmation or reclassification;
- a targeted teaching intervention; and
- one diagnostic follow-up problem per main cluster.

The MVP is not an automatic grader, plagiarism detector, generic tutor, or production student-record system.

## Initial misconception taxonomy

- incorrect clear-span boundary;
- long and short directions reversed;
- incorrect effective-span rule;
- incorrect slab-strip width;
- unit inconsistency;
- arithmetic-only mistake;
- no material misconception; and
- manual review required.

## Proposed Build Week stack

- Next.js
- React
- TypeScript
- Tailwind CSS
- Zod
- OpenAI Responses API
- GPT-5.6 multimodal structured analysis
- Vitest
- Playwright
- Vercel

## Privacy boundary

Only synthetic or anonymized student work may be used. Do not commit or upload real student names, student numbers, confidential records, API keys, or other secrets.

## Development workflow

Development is specification-driven:

1. Read `AGENTS.md` and the accepted specification.
2. Work from one accepted scoped task brief.
3. Implement only the accepted scope.
4. Review the complete diff.
5. Run and record exact verification evidence.
6. Record material scope changes as amendments before implementation.

Setup, execution, testing, deployment, sample-data instructions, measured evaluation results, and the Codex/GPT-5.6 workflow will be added as the corresponding implementation is completed and verified.
