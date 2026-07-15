# MA-MVP-001 — Misconception Atlas Build Week MVP

## Document control

- Project: Misconception Atlas
- Feature or change: OpenAI Build Week MVP
- Specification ID: `MA-MVP-001`
- Status: accepted
- Owner: Earl Adriano
- Date created: 2026-07-15
- Date accepted: 2026-07-15
- Competition category: Education
- Authoritative repository: `invicta-ctrl/Misconception-Atlas`
- Supersedes: none

## 1. Problem and intended outcome

Teachers commonly see final answers, scores, or piles of individual written solutions, but they do not receive a reliable class-wide view of where reasoning first failed, which students share the same root misconception, whether a mistake is conceptual, procedural, or arithmetic, and what teaching action would best address it.

The MVP must allow a teacher to analyze one prepared engineering assignment and a set of anonymized or synthetic student solutions, then receive an evidence-linked map of the class's major misconceptions and recommended next teaching actions.

The product is not a generic tutor or automated grader. Its defining output is a teacher-facing class misconception map rooted in the earliest supported reasoning error.

## 2. Current behavior

The repository currently contains only a minimal project description. No application, model integration, domain checker, fixture suite, evaluation harness, or deployment exists at acceptance time.

## 3. Scope

### Included

- One prepared Reinforced Concrete Design assignment.
- One deep problem family: two-way slab geometry and effective-span reasoning.
- Eight to twelve anonymized or synthetic student solution fixtures.
- Typed or clearly handwritten image inputs for the supported fixture set.
- Ordered reasoning-step extraction.
- Earliest-root-error identification.
- Evidence excerpts tied to the submitted work.
- Confidence and manual-review states.
- Deterministic checking for supported geometry, direction, span, unit, and slab-strip rules.
- Grouping submissions into class-level misconception clusters.
- Teacher confirmation, rejection, or reclassification of a diagnosis.
- Targeted teaching intervention and one diagnostic follow-up problem per main cluster.
- A polished, judge-testable desktop and tablet web experience.
- A documented Codex and GPT-5.6 development workflow.

### Excluded

- Support for every academic subject or engineering topic.
- Full Reinforced Concrete Design course coverage.
- Automatic final grading or gradebook export.
- Student ranking or high-stakes academic decisions.
- Plagiarism detection.
- Production LMS integration.
- School authentication or role administration.
- Persistent student records.
- Real student names, numbers, or personally identifiable information.
- Generic tutoring chat.
- Real-time classroom monitoring.
- Guaranteed interpretation of arbitrary handwriting.
- Custom model training or fine-tuning.
- Native mobile applications.
- Multi-school analytics.

### Off-limits behavior

- The system must not fabricate unreadable reasoning.
- The system must not assign a final grade.
- The system must not present model confidence as certainty.
- The system must not require or store real student identity data.
- The OpenAI API key must never be exposed to the client or committed to the repository.

## 4. Users and user flows

### Primary user

A college STEM or engineering instructor reviewing one class assignment.

### Primary flow

1. The teacher opens the prepared sample assignment.
2. The teacher selects the prepared fixture set or uploads supported anonymized solution images.
3. The system validates the submission files.
4. GPT-5.6 reconstructs ordered reasoning steps using a required structured schema.
5. The deterministic domain checker validates supported values, units, and rules.
6. The analysis engine identifies the earliest supported incorrect step or routes the work to manual review.
7. The system groups submissions into misconception clusters.
8. The teacher opens a cluster and reviews its description, affected submissions, evidence, confidence, downstream effects, intervention, and diagnostic follow-up.
9. The teacher confirms, rejects, or reclassifies a result.
10. The class map updates immediately.

### Failure and recovery flows

- Unsupported file: reject clearly and preserve previously completed results.
- Unreadable or incomplete solution: route to `MC-REV-00` manual review.
- Invalid model response: retry within a bounded policy, then return a recoverable error without inventing output.
- API failure: preserve existing state and allow retry.
- Deterministic/model conflict: flag the conflict for teacher review; deterministic results govern supported calculations.
- Duplicate upload: identify the duplicate rather than silently processing it twice.

## 5. Functional requirements

- FR-001: The application shall load one prepared two-way slab assignment and its reference reasoning structure.
- FR-002: The application shall support at least eight prepared anonymized or synthetic student submissions in the demonstration dataset.
- FR-003: Each successful analysis shall return ordered reasoning steps conforming to a runtime-validated schema.
- FR-004: Each diagnosis shall identify the earliest supported root misconception, not merely the final incorrect answer.
- FR-005: Each diagnosis shall include evidence linked to the corresponding submission or be marked insufficient for diagnosis.
- FR-006: The deterministic checker shall validate supported geometry, span-direction, effective-span, unit, and slab-strip-width rules.
- FR-007: The system shall classify the root issue as conceptual, procedural, arithmetic, correct, or manual review.
- FR-008: The dashboard shall group submissions by root misconception and show affected counts.
- FR-009: The system shall distinguish root misconceptions from downstream propagated errors.
- FR-010: The teacher shall be able to confirm, reject, or reclassify a diagnosis.
- FR-011: Cluster counts and displays shall update after a teacher override.
- FR-012: Each main misconception cluster shall provide a concise explanation, likely cause, targeted five-minute intervention, and one diagnostic follow-up problem.
- FR-013: The application shall provide a prepared judge demo path requiring no creation of sample data.
- FR-014: The application shall clearly disclose that results support teacher judgment and are not final grades.

## 6. Non-functional requirements

- NFR-001: The primary workflow must be usable on current desktop browsers and a tablet-sized viewport.
- NFR-002: Primary controls and result states must be keyboard accessible and use meaningful labels.
- NFR-003: The interface must include clear loading, empty, success, uncertain, and failure states.
- NFR-004: The model output schema must be runtime validated before display or persistence in session state.
- NFR-005: The API key and model calls must remain server-side.
- NFR-006: No real student PII may appear in fixtures, logs, screenshots, or demo media.
- NFR-007: Failed analysis of one submission must not erase completed analyses of other submissions.
- NFR-008: The repository must include setup, testing, sample-data, deployment, and judge-evaluation instructions.
- NFR-009: The deployed demonstration shown in the video must match the judge-accessible version.

## 7. Data model and invariants

### Core entities

- `Assignment`: id, title, subject, problemStatement, referenceSteps, supportedRules.
- `Submission`: id, anonymousLabel, sourceType, imageReference, processingStatus.
- `ReasoningStep`: id, sequence, extractedExpression, interpretation, evidenceReference, validationStatus.
- `Diagnosis`: submissionId, rootStepId, misconceptionCode, errorType, confidence, evidence, downstreamEffects, reviewStatus.
- `MisconceptionCluster`: code, label, description, memberSubmissionIds, priority, intervention, diagnosticPrompt.
- `TeacherReview`: diagnosisId, action, replacementCode, note, timestamp.

### Initial misconception taxonomy

- `MC-GEO-01`: incorrect clear-span boundary.
- `MC-DIR-01`: long and short directions reversed.
- `MC-SPAN-01`: incorrect effective-span rule.
- `MC-STRIP-01`: incorrect slab-strip width.
- `MC-UNIT-01`: unit inconsistency.
- `MC-ARITH-01`: arithmetic-only mistake.
- `MC-NONE-00`: no material misconception.
- `MC-REV-00`: manual review required.

### Invariants

1. Every displayed diagnosis has evidence or is explicitly marked uncertain/manual review.
2. Deterministic checks take precedence for supported calculations.
3. A downstream error is not counted as a separate root misconception without independent evidence.
4. Teacher overrides are preserved in session state and reflected in cluster counts.
5. The application never requires real student identity fields.
6. Model output is not trusted until schema validation succeeds.
7. Model failure does not erase already processed results.

## 8. Interfaces and integrations

### Recommended application stack

- Next.js
- React
- TypeScript
- Tailwind CSS
- Zod
- OpenAI Responses API
- GPT-5.6 with image input and structured output
- Vitest
- Playwright
- Vercel

### Integration boundaries

- The browser uploads or selects a solution.
- A server-side route validates the request and calls the OpenAI API.
- GPT-5.6 returns schema-constrained analysis.
- The deterministic checker evaluates supported domain rules.
- A reconciliation layer produces the final diagnosis or manual-review result.
- No production database is required for the Build Week MVP.

## 9. Error handling and edge cases

- Empty upload selection.
- Unsupported format or excessive file size.
- Duplicate submission.
- Unreadable handwriting.
- Incomplete solution.
- Correct method with arithmetic error only.
- Multiple errors where an earlier error causes later incorrect values.
- Model output that fails schema validation.
- Model/deterministic disagreement.
- OpenAI timeout or unavailable service.
- Partial batch completion.
- Teacher override after clustering.

## 10. Security and privacy review

- Authentication impact: none for the Build Week MVP.
- Authorization impact: none; the demonstration is a single-session teacher workflow.
- Sensitive data: student work can be educational data, so only synthetic or anonymized fixtures are permitted.
- Secret handling: the OpenAI API key is server-side and loaded from environment variables.
- Input validation: validate file type, size, required fields, and structured output.
- Logging and redaction: do not log image contents, real names, secrets, or full sensitive payloads.
- Abuse risk: clearly state that the tool cannot be used as the sole basis for grading or disciplinary decisions.

## 11. Migration, compatibility, and rollback

- Forward migration: none; this is a new repository and MVP.
- Backward compatibility: preserve fixture schema and public demo behavior after they are established.
- Data conversion: none.
- Rollback: use dedicated branches and revert to the last verified commit.
- Irreversible steps: none are authorized.

## 12. Implementation boundaries

### Expected modules

- application shell and teacher workflow;
- assignment and fixture data;
- analysis schema;
- OpenAI adapter;
- deterministic slab-rule checker;
- reconciliation and clustering logic;
- teacher review state;
- evaluation harness;
- unit and end-to-end tests;
- README and Build Week documentation.

### Allowed dependencies

Dependencies necessary for the accepted stack, schema validation, testing, accessibility, and deployment may be proposed in a scoped task brief.

### Prohibited changes

- Do not introduce authentication, a production database, an LMS SDK, background queues, fine-tuning infrastructure, or unrelated subject support without an accepted amendment.

## 13. Verification plan

- Focused unit tests for each deterministic misconception rule.
- Schema-validation tests for valid and malformed model outputs.
- Clustering and teacher-override tests.
- Gold-standard fixture evaluation.
- Full test suite.
- Linting and formatting checks.
- Type checking.
- Production build.
- Playwright primary teacher workflow.
- Manual desktop and tablet review.
- Manual verification that no secrets or real student PII are present.
- Clean judge setup using only the README.

## 14. Acceptance criteria

- AC-001: A teacher can load one assignment and analyze at least eight prepared submissions.
- AC-002: Every successful analysis returns schema-valid ordered reasoning steps.
- AC-003: At least 10 of 12 gold-standard fixtures receive the expected earliest-root classification.
- AC-004: Every classification displays evidence from the corresponding submission.
- AC-005: Ambiguous or unreadable work is routed to manual review rather than assigned a fabricated diagnosis.
- AC-006: The deterministic checker correctly validates supported slab geometry, span, direction, unit, and strip-width rules.
- AC-007: The dashboard groups submissions by misconception and distinguishes root from downstream errors.
- AC-008: The teacher can override a classification and see cluster counts update.
- AC-009: Each main cluster can produce a targeted intervention and diagnostic follow-up problem.
- AC-010: No student name, student number, or sensitive educational record is required.
- AC-011: The complete demonstration works on desktop and remains usable on a tablet.
- AC-012: Unit tests, integration tests, linting, type checking, production build, and the principal Playwright workflow pass.
- AC-013: A judge can run the sample project using only the README and included sample data.
- AC-014: The repository clearly documents where GPT-5.6 and Codex were used.
- AC-015: The deployed experience shown in the final video matches the judge-accessible build.

## 15. Assumptions and unresolved decisions

### Confirmed assumptions

- The official category name is `Education`.
- Earl is the project owner and entrant.
- The demonstration uses synthetic or anonymized work only.
- The first problem family is two-way slab geometry and effective-span reasoning.
- The proposed default stack is accepted.
- The repository is public.

### Unresolved decisions

No unresolved decision currently blocks foundation setup. Exact visual identity, assignment numbers, fixture images, and deployment URL may be selected during scoped implementation without broadening the accepted behavior.

## 16. Risks and mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
|---|---:|---:|---|---|
| Handwriting is misread | High | High | Use clear fixtures, evidence links, confidence, and manual review | Project owner |
| AI invents a rationale | Medium | High | Structured output, deterministic checks, and evidence requirement | Project owner |
| Scope becomes too broad | High | High | Enforce one problem family and written amendment gate | Project owner |
| Demo depends on unstable live calls | Medium | High | Include prepared fixtures, bounded retries, and recoverable states | Project owner |
| Evaluation claims are weak | Medium | High | Build a 12-case gold-standard fixture suite | Project owner |
| Real educational data is exposed | Low | Critical | Use synthetic/anonymized fixtures only and review all media | Project owner |
| Build Week deadline is missed | Medium | Critical | Prioritize one complete vertical slice and internal cutoff | Project owner |

## 17. Amendments

| Amendment | Date | Reason | Approved by | Affected requirements or criteria |
|---|---|---|---|---|
| None | — | — | — | — |

## 18. Acceptance record

- Accepted by: Earl Adriano
- Acceptance date: 2026-07-15
- Accepted scope summary: Teacher-facing misconception analysis for one two-way reinforced-concrete slab reasoning problem family, using GPT-5.6 structured multimodal analysis, deterministic domain checks, class clustering, teacher review, and a judge-testable web demonstration.
- Conditions of acceptance: Use the proposed defaults, remain in the exact `Education` category, follow the repository specification gate, and record material scope changes as amendments before implementation.
