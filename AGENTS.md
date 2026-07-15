# AGENTS.md

## Project

Misconception Atlas is an OpenAI Build Week Education submission that turns student solution work into an evidence-linked class misconception map.

## Required entry sequence

1. Read this file.
2. Read `docs/specs/MA-MVP-001.md`.
3. Read `PROJECT_STATUS.md`.
4. Read `docs/WORK_CONTINUATION.md` before continuing an existing workstream.
5. Inspect the current branch, diff, and verification state before modifying files.

## Authority order

1. Earl's current explicit instruction.
2. Accepted specification and recorded amendments.
3. This repository's current status and continuation records.
4. Verified tests and implementation behavior.
5. Chat summaries and assumptions.

## Specification gate

- Do not implement non-trivial behavior outside an accepted specification.
- Implement only `MA-MVP-001` unless a written amendment is accepted first.
- Keep the Build Week MVP teacher-facing and limited to the accepted two-way reinforced-concrete slab reasoning vertical slice.
- Do not silently broaden support to other subjects, problem families, LMS integrations, grading, authentication, or persistent student records.

## Development discipline

- Work on one focused vertical slice at a time.
- Use dedicated branches and small descriptive commits.
- Do not push, merge, rewrite history, delete branches, or perform destructive actions without Earl's explicit authorization.
- Treat AI-generated code and analysis as untrusted until reviewed and verified.
- Do not commit secrets, API keys, real student identifiers, or confidential educational records.
- Use anonymized or synthetic fixtures only.
- Every model-generated diagnosis must be schema-valid, evidence-linked, and able to return manual review when evidence is insufficient.
- Deterministic domain checks take precedence for supported calculations.

## Required verification

For each completed implementation unit, run and report the applicable commands exactly:

- focused unit tests;
- full test suite;
- linting;
- type checking;
- production build;
- Playwright coverage for the primary teacher workflow;
- fixture evaluation against the gold-standard misconception labels;
- manual responsive and accessibility review when UI behavior changes.

No task is complete solely because the interface renders or generated output appears plausible.

## Completion report

Every completed task must record:

- accepted scope;
- files changed;
- behavior implemented;
- commands run and exact results;
- acceptance criteria supported by evidence;
- known risks and limitations;
- amendments, if any;
- rollback checkpoint;
- recommended next scoped task.
