# Synthetic communication acceptance v0.1

This package makes the eight-scenario matrix in [medical acceptance issue #2](https://github.com/grwtsk/medicine/issues/2) explicit as finite synthetic worlds, observation maps, and independently authored expected outcomes. [Coordination issue #1](https://github.com/grwtsk/medicine/issues/1) owns the cross-repository acceptance boundary.

These are authored specifications. They contain no actual people, clinical records, operational authorizations, execution receipts, or empirical findings. Proposed response functions describe work a future design must assign; they do not appoint a person or service.

## 1. Package and schemas

The authored source consists of six files:

| File | Schema or role |
| --- | --- |
| `specification.md` | Human-readable meaning, projection contract, and unresolved acceptance obligations |
| `scenarios.json` | `grwtsk.medicine.communication-scenarios/1` |
| `expectations.json` | `grwtsk.medicine.communication-expectations/1` |
| `vectors.json` | `grwtsk.medicine.finite-observation-vectors/1`; 108 literal model/query payloads and fixed input pins |
| `corpus.json` | `noe.finite-observation-corpus/1`; 54 ordered generic evaluator requests with authored expectations |
| `bindings.toml` | `grwtsk.medicine.communication-bindings/1`; exact identity of the five files above |

Both JSON files use `suite_id = communication-v0.1`. The scenario file has eight `cases`, six ordered `predicates`, and nine case/view combinations. The expectation ledger has 54 `records`: one record for each case/view/predicate combination.

The vectors and bindings complete the literal source package. Its execution adapter belongs with the generic evaluator. This specification does not add fields to that evaluator's model or query schemas.

## 2. Six separate predicates

The declared order is `R, U, A, H, Tr, Ts`.

| ID | Versioned claim ID | Meaning within a stipulated world |
| --- | --- | --- |
| R | `communication.receipt.v1` | The intended recipient received the specified communication by the review cutoff |
| U | `communication.understanding-evidence.v1` | The specified evidence of understanding is present by the cutoff |
| A | `communication.action-completed.v1` | The specified fictional requested action was completed by the cutoff |
| H | `communication.handoff-accepted.v1` | The fictional receiving role expressly accepted the specified handoff by the cutoff |
| Tr | `communication.response-by-target.v1` | The specified response occurred at or before the synthetic response target |
| Ts | `communication.resolution-by-target.v1` | The specified resolution occurred at or before the synthetic resolution target |

The understanding evidence is a stipulated written restatement containing the fictional tokens `request-alpha` and `step-alpha`. Its presence is evidence under this fixture definition. It does not measure mental state or establish consent, refusal, or capacity. The action is the fictional completion of `step-alpha`; no real intervention is represented.

Receipt, understanding evidence, action completion, acceptance, response, and resolution have separate event kinds. Endpoint delivery and observed acknowledgment are additional observations. Neither is interchangeable with these six predicates.

No universal implication among the predicates is asserted. Correlations among the selected worlds are properties of this small authored corpus, not general rules about communication or care.

## 3. Stipulated evidence and timing

All timing is expressed in invented ticks:

| Parameter | Value |
| --- | --- |
| Start | 0 |
| Response target | 10 |
| Resolution target | 20 |
| Review cutoff | 30 |

Target comparisons are inclusive. Positive fixture events use these ticks:

| Evidence field | Tick when present |
| --- | --- |
| `recipient_receipt_tick` | 3 |
| `understanding_evidence_tick` | 5 |
| `action_completion_tick` | 9 |
| `handoff_acceptance_tick` | 6 |
| `response_tick` | 8 |
| `resolution_tick` | 18 |

A world's evidence ledger is complete **by fictional stipulation only**, for the six qualifying event kinds through tick 30. A `null` tick therefore stipulates that no qualifying event of that kind occurs through the review cutoff in that world. It does not mean that an observer failed to receive an event record.

Each stored valuation must agree with its stated rule and event ticks. R, U, A, and H test the presence of their qualifying event by the cutoff. Tr and Ts test presence by their respective targets. All negative timing examples in this version stipulate no qualifying event through the cutoff. This corpus does not separately exercise late-but-present events or equality at the target.

An observation can hide a stipulated event. For example, in case 5 one world has no resolution by the cutoff, while another has a resolution at tick 18 whose evidence is unavailable to the queried view. The incomplete observation leaves both worlds compatible; the timely-resolution claim is ambiguous.

This distinction prevents missing observations from being filled with false values. The corpus's fictional ledger completeness establishes no complete instrumentation, global observability, or real-world coverage.

## 4. Admissibility and world identity

Every world has an opaque case-local ID such as `c03.w1`, an explicit `admissible` Boolean, a six-predicate `valuation`, and the stipulated `evidence` ticks.

All listed worlds in this version are explicitly admissible. Their admissibility is an authored premise. The corpus supplies no rule for excluding real possibilities and no claim that these lists cover an actual episode.

World order is significant for expected witness-list order. World IDs must remain unchanged across the six predicate projections of a case/view. Opaque IDs are not a privacy mechanism; a mapping, count, explanation, or repeated query can still disclose information.

## 5. Authored matrix

Tuples below use the declared predicate order. `S` means supported, `F` refuted, `B` ambiguous, and `M` model mismatch. The expectation ledger spells out the complete status names.

| Case/view | World valuations in declared order | Compatible world suffixes | Expected statuses |
| --- | --- | --- | --- |
| c01 / review | 000000; 100000; 111111 | w1, w2, w3 | B, B, B, B, B, B |
| c02 / review | 100000; 110000; 111010 | w1, w2, w3 | S, B, B, F, B, F |
| c03 / review | 110110; 111110 | w1, w2 | S, S, B, S, S, F |
| c04 / review | 111010 | w1 | S, S, S, F, S, F |
| c05 / review | 111110; 111111 | w1, w2 | S, S, S, S, S, B |
| c06 / detailed | 100000; 111111 | w2 | S, S, S, S, S, S |
| c06 / limited | The same two worlds | w1, w2 | S, B, B, B, B, B |
| c07 / review | 000000; 111111 | None | M, M, M, M, M, M |
| c08 / review | 111111 | w1 | S, S, S, S, S, S |

For c01 through c05 and c08, the ordinary review observation maps every listed world to the queried token. This represents the scenario's particular observation, not unrestricted access to a complete ledger.

Case c07 has a nonempty two-world universe. Both worlds map to `known.observation`, while the query requests `unmatched.observation`. Its compatible set is empty. This is a valid model-relative result and does not establish a person's behavior or the falsity of any external report.

## 6. Case 6: one universe, two observation maps

The two views retain identical world IDs, admissibility, evidence, and valuations:

| World | Valuation | Detailed observation | Limited observation |
| --- | --- | --- | --- |
| c06.w1 | 100000 | `detail.receipt_only` | `limited.receipt_recorded` |
| c06.w2 | 111111 | `detail.completed` | `limited.receipt_recorded` |

The detailed query requests `detail.completed`. The limited query requests `limited.receipt_recorded`.

The explicit coarsening map sends both detailed observation tokens to `limited.receipt_recorded`. For each shared world, applying that map to its detailed observation must equal its limited observation. The detailed world universe must not be reduced to obtain the more informative result.

These are observation functions. Neither a view name nor a query token authenticates a role, grants permission, or filters disclosure. This authored corpus is public and synthetic; it is not a deployment of restricted access.

## 7. Projection into the one-claim API

For every case, view, and predicate, create a separate model with schema `grwtsk.finite-observation-model/1`. Each world produces exactly one row, in the declared order:

| Scenario source | Model field |
| --- | --- |
| `world.id` | `trace_id` |
| `world.admissible` | `admissible` |
| `view.observation_by_world[world.id]` | `view` |
| `world.valuation[predicate.id]` | `claim` |

The model uses the predicate's exact `claim_id`, a unique model ID, and a declared fixture revision. The corresponding query has schema `grwtsk.finite-observation-query/1`, the exact model digest, the exact claim ID, and `view.query_observation`.

For all six projections of a case/view, the ordered world IDs, admissibility, observation values, and queried observation must match. Only the selected claim ID and Boolean claim column change.

The case description, evidence ledger, timing, proposed response function, and view identifier are outer-package information. They must not be inserted into the evaluator's strict model/query objects. Exact model bytes bind the projected values and strings; their semantic interpretation requires the separately bound specification and scenario source.

## 8. Independent expectation ledger

A record ID has the form `cNN.view.P`, for example `c06.limited.Tr`. Each record contains:

- `case_id`, `view_id`, `predicate_id`, and the versioned `claim_id`.
- `expected.status`.
- `expected.compatible_ids`.
- `expected.witness_ids.claim_true` and `expected.witness_ids.claim_false`.
- `expected.counts.total`, `admissible`, `compatible`, `claim_true`, and `claim_false`.

The status vectors and positive/negative witness partitions are authored separately from the classifier implementation. Counts describe those declared sets. They are not captured classifier results. The ledger must not be regenerated by treating the implementation under test as its oracle.

The compatible list preserves world order. Positive and negative witness lists each preserve that same order. Their disjoint union must equal the compatible set. Both witness lists are empty for the six c07 records; this emptiness supports neither side.

Independently authored does not mean independently reviewed. Source review, projection review, execution evidence, and any formal acceptance must be recorded separately when performed.

## 9. Byte and source binding requirements

The package must define exact UTF-8 JSON bytes for every model and query, with sorted keys, ASCII escaping, separators `","` and `":"`, and no trailing newline in each API payload. The input file's readable formatting is not a substitute for this serialization rule.

The query's `model_sha256` must refer to its exact projected model bytes. Fixed model and query pins must come from the selected authored package, not be inferred from arbitrary submitted bytes and then presented as independent expectations.

Bind the scenario source, expectation ledger, specification, and byte vectors together. Source identity and semantic identity matter in addition to a passing digest comparison. A digest does not itself authenticate its origin or grant authority.

Each `vectors.json` input stores an `input_id`, `sha256`, `byte_count`, and `payload_utf8`. Parse the outer file, then UTF-8 encode each decoded `payload_utf8` string exactly; do not append a newline or regenerate it from a differently formatted object. The inner JSON obeys the serialization rule above. Input IDs are the expectation record ID followed by `.model` or `.query`; model IDs are `communication-v0.1.` followed by the record ID, with revision `v0.1`.

The corpus carries only the generic case ID, input references and pins, and expected status, counts, and witness lists. It adds `kind = classified` to each copied expectation and keeps `compatible_ids` in the separate medical ledger. The raw corpus file's expected digest comes from the selected `bindings.toml`, whose identity and repository revision must themselves be selected independently. A later execution record must bind the actual implementation and these exact authored source bytes; this package has no self-referential commit pin.

Malformed input, unsupported versions, invalid claims, and failed bindings remain input failures outside the four classification statuses. They must not be reclassified as `model_mismatch`.

## 10. Computational acceptance

The computational portion of a later review should check all 54 records against the selected evaluator candidate and preserve the exact source pairing.

Required comparisons include status, counts, compatible set, and positive/negative witness order. Because the primitive reports partitioned witness lists, any reconstructed compatible set must be compared without inventing a new ordering claim. The projection review separately checks row order and all six columns against the authored scenario.

The candidate pairing must keep computation, formal acceptance, application correspondence, professional review, and permission to act separate. A successful comparison of this corpus is bounded fixture agreement, not a general implementation-refinement proof.

This source package contains no reported run outcomes. It supplies no authority for care, disclosure, retries, record changes, billing, or reassignment of responsibility.

## 11. Obligations beyond classification

| Area | Required design or review | Classification boundary |
| --- | --- | --- |
| Meaning and coverage | Review event definitions, admissibility, observation reliability, and every claimed implication | Predicate names and supplied Booleans do not establish facts outside the model |
| Disclosure | Review access to models, query choices, counts, witnesses, diagnostics, explanations, and repeated results | The primitive accepts full models and returns witness IDs; it is not a role-disclosure filter |
| Continuity | Specify proposed responsibility, acceptance, follow-up, escalation, recovery, and target handling | Classification cannot assign a service, obtain acceptance, cause a response, or resolve work |
| Agency | Preserve questions, correction of premises, and challenge of proposed actions | A positive result does not remove participation or authorize an action |
| Accessible challenge | Provide and exercise the required written route | Event support does not establish interaction usability |

For c01, unavailable acknowledgment preserves uncertainty. A consequential retry requires separate reconciliation and authority.

For c02 and c03, supported receipt or understanding evidence does not complete a separate action obligation.

For c04, `handoff_unaccepted` remains a distinct proposed workflow condition even when action completion is supported. Sending a notice must not silently become accepted transfer. This package does not determine an actual person's continuing duties.

For c05, an accepted handoff and a timely response do not establish timely resolution. A missing resolution record remains different from evidence that a target was missed.

For c06, access to the detailed model or its outputs would defeat a limited-view restriction. Protecting only a displayed status is insufficient. Any later integration must consider model contents, counts, witness IDs, error channels, explanations, and combinations of queries.

For c07, reconcile the model and observation without treating mismatch as a finding about a person.

For c08, the fictional participant requires written exchange, while the offered challenge route is speech-only. The authored expected interaction outcome is `challenge_route_unusable`, alongside six supported event claims. A later exercise must provide and test a written route. This is an expected counterexample, not a recorded usability test. No aggregate pass flag may erase the separate interaction failure.

The classifier, source-binding review, disclosure review, accessibility exercise, continuity review, and any later empirical or professional review therefore require distinct outcomes. Proposed response functions remain unappointed design roles.

Conceptual direction and authorship: R.A. Jacob Martone. Specification and byte-vector development with AI assistance.

