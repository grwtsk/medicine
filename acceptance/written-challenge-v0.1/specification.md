# Authored written challenge acceptance v0.1

This companion package specifies a written challenge lifecycle for the synthetic need in [communication case 8](../communication-v0.1/specification.md). It advances the accessible-participation, correction, disclosure, and continuity requirements tracked in [issue #2](https://github.com/grwtsk/medicine/issues/2), within the cross-repository boundary of [issue #1](https://github.com/grwtsk/medicine/issues/1).

The package contains authored inputs and expectations only. It contains no running interface, executed interaction, persistence receipt, empirical usability result, professional review, actual appointment, or permission to act. The transcripts describe proposed behavior of a future generic implementation. Every person-like function is abstract and unappointed; all text, context, events, and timing are invented.

## 1. Package and source boundary

| File | Schema or role |
| --- | --- |
| `specification.md` | Closed field definitions, event meanings, requirements, and review boundaries |
| `scenarios.json` | `grwtsk.medicine.written-challenge-scenarios/1`; six authored transcripts and a baseline reference |
| `expectations.json` | `grwtsk.medicine.written-challenge-expectations/1`; separately authored event outcomes, checkpoint states, and visible projections |
| `bindings.toml` | `grwtsk.medicine.written-challenge-bindings/1`; exact identities of the three authored files above |

Both JSON files use `suite_id = written-challenge-v0.1`. There are six cases, seven variant instances, 75 authored events, 31 authored checkpoints, and 39 checkpoint instances after applying the two variants of w06. These are source counts, not run results.

The baseline is case c08, view `review`, in `communication-v0.1` at repository revision `02aada9bdc9eb7e66a7c44547f298b141f3967ca`. Its source files are pinned in `scenarios.json`. Its six supported claims coexist with the separately authored `challenge_route_unusable` expectation. This package neither edits those files nor replaces that failing interaction baseline with a success result.

All six new cases challenge the synthetic premise or proposed step associated with that baseline. Their revision identifiers refer to challenge text, not revisions of the baseline model. No operation in this contract changes a model, observation, valuation, communication event, or existing classifier result. Challenge response and resolution events are separate from the original communication episode's `Tr` and `Ts`.

## 2. Closed source schemas

Every object described below is closed: all listed fields are required, and additional fields are invalid. Nullable values must be explicit `null`. JSON objects with duplicate keys are invalid. Object-key order is not semantic; array order is significant. Strings are UTF-8 JSON strings. An identifier is a nonempty ASCII string matching `[A-Za-z0-9][A-Za-z0-9._/-]*`; free text is a nonempty string without a NUL character. A tick or count is a nonnegative integer, never a Boolean. A SHA-256 is 64 lowercase hexadecimal characters. A revision pin is 40 lowercase hexadecimal characters.

Unknown schema versions, invalid fields or references, invalid types, conflicting identifiers, and failed source bindings are input failures. They are not any of the four finite-classifier outcomes. This package does not alter the classifier's strict model/query schemas.

### 2.1 Scenario file

The root has exactly `schema`, `suite_id`, `artifact_kind`, `scope`, `timing`, `baseline_reference`, `requirements`, `disclosure_profile`, `cases`, and `authorship`. Schema and suite values are the fixed strings in section 1. The fixed values of `artifact_kind` and `scope` are `authored-synthetic-specification` and `synthetic-written-challenge`. `requirements` and `cases` are nonempty ordered arrays of their named object types below; the other composite root fields are single objects of their named types.

| Object | Exact fields and types |
| --- | --- |
| `timing` | `unit` = `synthetic_tick`; `start` = 0; `response_target` = 10; `resolution_target` = 20; `review_cutoff` = 30; `target_comparison` = `inclusive`; `episode` = `challenge-relative`; `correction_resets_targets` = false |
| `baseline_reference` | `id`, `repository`, `revision`, `source_suite_id`, `case_id`, `view_id`, `required_route`, `offered_route`: strings; `source_files`: ordered array of SourcePin; `predicate_order`: the array `R,U,A,H,Tr,Ts` |
| SourcePin | `path`: relative path; `sha256`: SHA-256; `byte_count`: count |
| Requirement | `id`: identifier; `requirement`: free text |
| `disclosure_profile` | `id`: identifier; `status_fields`, `allowed_text_kinds`, `allowed_surfaces`, `excluded_internal_fields`: ordered arrays of distinct strings; `scope`: free text |
| Case | `id`, `title`, `challenge_id`: strings; `requirement_ids`: distinct declared requirement identifiers; `participant_need` and `offered_route` = `written_exchange`; `variants`: nonempty array of Variant; `events`: nonempty array of Event |
| Variant | `id`: identifier unique within its case; `internal_context`: InternalContext |
| InternalContext | `model_text`, `diagnostic_text`, `hidden_note`: free text; `witness_ids`: ordered array of distinct identifiers; `counts`: object containing only the nonnegative integer `compatible` |
| Event | `id`: identifier unique across the package; `tick`: tick; `op`: operation from section 3; `input`: the corresponding closed object from section 3 |
| `authorship` | `conceptual_direction_and_authorship` = `R.A. Jacob Martone`; `development` = `AI-assisted authorship` |

Case identifiers and challenge identifiers are unique. Each case starts at tick 0 with no drafts, submissions, requests, reviews, responses, resolution records, or disagreements. Its written route is available by fictional stipulation. Event ticks are nondecreasing and no later than the review cutoff. InternalContext is a synthetic disclosure-test input; it is not a real model, authenticated identity, authorization record, or clinical record. Its counts and witness strings need not correspond to a classifier input.

### 2.2 Expectation file

The root has exactly `schema`, `suite_id`, `artifact_kind`, `scope`, `authorship_method`, `counts`, `baseline_expectation`, `cases`, and `authorship`. Schema and suite values are the fixed strings in section 1. The fixed `artifact_kind` is `authored-expectation-ledger`; `scope` is `synthetic-written-challenge`. `authorship_method` is free text, and `cases` is a nonempty ordered ExpectedCase array. `counts` and `baseline_expectation` are single objects of their named types below. `authorship` has the same closed shape as in the scenario file.

| Object | Exact fields and types |
| --- | --- |
| `counts` | Nonnegative integers `case_count`, `variant_count`, `authored_event_count`, `authored_checkpoint_count`, `instantiated_checkpoint_count` |
| `baseline_expectation` | `baseline_id`, `source_case_id`: identifiers; `communication_predicate_outcomes`: closed object with exactly `R,U,A,H,Tr,Ts`, each `supported`; `interaction_outcome` = `challenge_route_unusable`; `overall_acceptance` = `not_established` |
| ExpectedCase | `case_id`: identifier; `variant_ids`: exact ordered scenario variant identifiers; `event_outcomes`: ordered EventOutcome array; `checkpoints`: ordered Checkpoint array |
| EventOutcome | `event_id`: corresponding event identifier; `outcome`: `accepted`, `accepted_no_change`, or `rejected`; `error_code`: null, `revision_not_current`, or `projection_not_permitted` |
| Checkpoint | `id`: globally unique identifier; `after_event_id`: event in the same case; `expected_state`: State; `expected_projection`: VisibleProjection |

There is one EventOutcome for every authored event, in the same order. A rejected event has a non-null error code; other outcomes have null. Checkpoints are in event order, have no duplicate `after_event_id`, and apply independently to every listed variant. w06's two variants must match the same expected projection at each checkpoint. All expected states and projections are authored values, not captured outputs. Reusing authored text-entry shapes or copying an authored state's declared public fields into its expected projection is source preparation, not running a transition processor as an oracle.

## 3. Event contract

An event is an authored input to a possible future interaction exercise. `record_*` means that the fixture supplies a qualifying synthetic observation; it does not assert that a real event occurred. An omitted observation leaves its evidence unavailable. This package does not stipulate complete observation of events outside its transcript.

The event tick establishes the checkpoint clock even when the attempted operation is rejected. Rejection preserves the content and event-record collections. No event emits a downstream action. A request, recorded observation, review, response, resolution record, pause, or timeout confers no actual authority.

| `op` | Exact `input` fields | Meaning and preconditions |
| --- | --- | --- |
| `save_draft` | `revision_id`: new identifier; `predecessor_revision_id`: identifier or null; `text`: free text | Retain exact text as a new draft revision. The first predecessor is null; a correction names the previous draft. Existing revision text is immutable. Saving does not submit. |
| `inspect` | `surface`: `draft`, `status`, `history`, `export`, or `internal` | `draft` inspects the current draft and records its revision as inspected. Other permitted surfaces leave content unchanged. `internal` is a deliberate negative control: reject with `projection_not_permitted`, return the error projection, and disclose no InternalContext field. |
| `pause` | Empty object | Retain all draft, submission, review, and response state across the stipulated pause. No actual storage durability is established by this source. |
| `resume` | Empty object | Make the retained written state available without requiring speech or an automatic resubmission. |
| `submit` | `attempt_id`, `revision_id`: identifiers | Explicitly record an attempt for the current inspected draft. It does not itself confirm submission or acceptance of review. Repeating the same attempt identifier and revision is `accepted_no_change`. Reusing an attempt identifier with different content or revision is invalid input. |
| `record_submission` | `attempt_id`, `revision_id`: identifiers | Record the fixture's confirmation of that exact existing attempt. Add the immutable revision to submitted revisions if not already present; an exact repeated confirmation is `accepted_no_change`. Confirmation is not reviewer receipt, review acceptance, consent, or permission. |
| `request_review` | `request_id`, `revision_id`: identifiers | Record a proposed request concerning a confirmed submitted revision. Retain its revision in the request list. It sends nothing and appoints nobody. |
| `record_review_acceptance` | `acceptance_id`, `revision_id`: identifiers | Record explicit synthetic acceptance of review of a confirmed submitted revision. Neither request, submission, review activity, nor response implies this separate observation. |
| `record_review` | `record_id`, `revision_id`: identifiers; `text`: free text | Record a synthetic review note for the exact confirmed submitted revision. A review note does not by itself create an acceptance observation or demonstrate professional approval. |
| `record_response` | `record_id`, `revision_id`: identifiers; `text`: free text | Record a written response for the exact confirmed submitted revision. A response may be present while acceptance, review, or resolution remains unavailable. |
| `propose_resolution` | `record_id`, `revision_id`: identifiers; `text`: free text | Retain a written proposal concerning a confirmed submitted revision. A proposal is not a resolution record or participant agreement. |
| `record_resolution` | `record_id`, `revision_id`, `review_record_id`: identifiers; `text`: free text | Require the current confirmed revision and an existing review note for that same revision. An attempt naming an earlier submitted revision is rejected with `revision_not_current`. Otherwise record only the stipulated challenge-resolution event. It does not close the written route or authorize a proposed action. |
| `record_disagreement` | `record_id`, `revision_id`: identifiers; `text`: free text | Retain the participant's written disagreement concerning a confirmed submitted revision. For the current revision, participant position becomes `disputed`; earlier resolution evidence remains recorded. |
| `advance_tick` | Empty object | Advance only the synthetic review clock. An elapsed target does not supply a missing event observation, acceptance, resolution, or authority. |

All referenced revisions must exist; references requiring confirmation must identify a submitted revision. All record, request, and acceptance identifiers are unique within their respective collections. A `review_record_id` must reference a review note for the named revision; an invalid reference is input failure. Only the two explicitly authored negative operations above produce a valid-event `rejected` outcome in this version. A future implementation must reject other invalid inputs rather than inventing a classifier result.

The current submitted revision is the newest confirmed revision in the retained draft predecessor chain. Confirming a newer correction changes `current_revision_id` to that revision. A later confirmation of an older revision cannot roll back a newer confirmed correction; out-of-order confirmation is defined by this rule but is not separately exercised in these six traces. Prior drafts, attempts, submitted revisions, notes, responses, proposals, resolution records, and disagreements remain in history. Their observations do not transfer to the new revision. A saved but unsubmitted correction leaves the current submitted revision unchanged and remains visible as a draft. Corrections never reset the challenge's timing targets.

## 4. Exact checkpoint State

State has exactly the following fields. Lists preserve the order in which their qualifying events were recorded. Duplicate `submit` attempts do not add entries. Duplicate request or acceptance observations for a revision, if later specified, must not add that revision twice to the corresponding list. All six cases retain `written_route_available = true`, `authority_status = not_established`, and `downstream_actions = []` at every checkpoint and between checkpoints.

| Field | Type and meaning |
| --- | --- |
| `tick` | Current event tick |
| `draft_records` | DraftRecord array retaining all exact authored draft versions |
| `draft_revision_id` | Latest saved revision identifier, or null |
| `inspected_draft_revision_id` | Most recently inspected draft revision, or null |
| `submission_attempts` | Attempt array |
| `submitted_revision_ids` | Distinct confirmed submitted revision identifiers in confirmation order |
| `current_revision_id` | Newest confirmed submitted revision in draft predecessor order, or null |
| `requested_review_revision_ids` | Distinct submitted revision identifiers with a recorded proposed review request |
| `accepted_review_revision_ids` | Distinct submitted revision identifiers with an explicit recorded acceptance observation |
| `review_records` | TextRecord array |
| `response_records` | TextRecord array |
| `resolution_proposals` | TextRecord array |
| `resolution_records` | ResolutionRecord array |
| `disagreements` | TextRecord array |
| `current_review_accepted` | Boolean; explicit acceptance is recorded for the current submitted revision |
| `current_review_recorded` | Boolean; a review note is recorded for the current submitted revision |
| `current_response_evidence` | `unavailable` or `recorded`, for the current submitted revision |
| `current_response_timing` | `unconfirmed`, `by_target`, or `after_target` |
| `current_resolution_evidence` | `unavailable` or `recorded`, for the current submitted revision |
| `current_resolution_timing` | `unconfirmed`, `by_target`, or `after_target` |
| `response_target_elapsed` | Boolean; `tick > response_target` |
| `resolution_target_elapsed` | Boolean; `tick > resolution_target` |
| `participant_position` | `not_recorded` or `disputed`, concerning the current submitted revision; `not_recorded` means no qualifying position record, not agreement |
| `written_route_available` | Boolean, stipulated true for the new traces |
| `authority_status` | Fixed `not_established` |
| `downstream_actions` | Empty array in this package |

Nested closed shapes:

- DraftRecord: `revision_id`, `predecessor_revision_id` (identifier or null), `tick`, `text`.
- Attempt: `attempt_id`, `revision_id`, `confirmation` (`unconfirmed` or `recorded`).
- TextRecord: `record_id`, `revision_id`, `tick`, `text`.
- ResolutionRecord: `record_id`, `revision_id`, `review_record_id`, `tick`, `text`.

The current-review Booleans are false if there is no current submitted revision. For either timing question, unavailable evidence gives `unconfirmed`, even after the target elapses. Recorded evidence uses the earliest qualifying record for the current revision: an event at or before its target gives `by_target`; a later qualifying event gives `after_target`. Equality qualifies. A later checkpoint does not turn an observed timely event into a late one. These fields describe the supplied challenge observations only.

There is deliberately no field that equates a response, recorded resolution, silence, or supported baseline event with participant agreement, acceptance of an actual handoff, professional adequacy, or permission to act. A resolution record and a later disagreement can coexist. The written route stays available in both states.

## 5. Exact visible projection

VisibleProjection has exactly `schema`, `challenge_id`, `surface`, `public_code`, `message`, `status`, `text_entries`, and `transcript_event_ids`.

An accepted `save_draft` produces the draft surface without itself marking that revision inspected. An accepted `inspect` produces its requested permitted surface. A rejected operation produces the error surface. All other accepted operations, including `accepted_no_change`, produce the status surface. The authored checkpoints select particular event outputs from this rule; they do not instruct an implementation to choose an output retrospectively.

- `schema` is `grwtsk.medicine.written-challenge-visible-projection/1`.
- `challenge_id` identifies the same synthetic case. `surface` is `draft`, `status`, `history`, `export`, or `error`.
- `public_code` is `ok`, `revision_not_current`, or `projection_not_permitted`. Error surfaces contain the relevant error code; other surfaces use `ok`.
- `message` is the exact written explanation authored for that surface or error below. It is nonempty free text and contains no InternalContext value. An error code alone is not the specified written explanation.
- `status` is a closed object containing exactly the fields listed, in order, in `scenarios.json`'s `disclosure_profile.status_fields`. Their expected values are the corresponding authored State values. Array order remains significant; JSON object-key order does not.
- `text_entries` is an ordered array of closed objects containing `entry_id`, `kind`, `revision_id`, `tick`, and `text`. Kinds are exactly `challenge_revision`, `review`, `response`, `resolution_proposal`, `resolution`, and `disagreement`. For a draft, `entry_id` is its revision identifier; otherwise it is the text record identifier.
- The `draft` surface shows only the current draft text entry. `history` and `export` show all permitted text entries in qualifying-event order, including prior and unsubmitted draft revisions. `status` and `error` have empty `text_entries`.
- `transcript_event_ids` is the exact ordered list of all input event identifiers through the checkpoint for `history` and `export`, including rejected attempts and inspection events. It is empty for all other surfaces. This list does not include raw rejected input or hidden diagnostics.

| Surface or error code | Exact written `message` |
| --- | --- |
| `draft` | Review the written draft before submitting it. Saving or inspecting does not submit it. |
| `status` | Inspect the separate submission, review, response, and resolution states below. No downstream action is authorized. |
| `history` | Your retained written revisions and responses appear in order. Earlier revisions remain distinguishable from current submitted work. |
| `export` | This transcript contains the declared written history and status. It does not include internal context. |
| `revision_not_current` | This resolution attempt refers to an earlier revision. A resolution record must name the current submitted revision and its own review. |
| `projection_not_permitted` | This view does not include internal context. You can inspect your written challenge, status, history, or export. |

The participant projection permits their own challenge text, the declared written notes and responses, and the declared status fields. It excludes all five InternalContext fields from every output surface. An error contains no hidden field value, count, witness, explanation, or model text. InternalContext can neither change the event outcome nor change the visible projection in the supplied w06 pair. Error, history, export, and repeated-request checkpoints are explicitly included.

These are authored projections for a declared synthetic profile. A profile identifier does not authenticate anyone or grant access. Public storage of these invented fixture values is not a deployed privacy boundary. Agreement on the two w06 variants would demonstrate only those examples, not protection against arbitrary repeated queries, timing channels, other diagnostics, or combinations of outputs. A later integration must review every actual input/output surface and its authorization mechanism separately.

## 6. Six transcripts and baseline

| Case | Authored sequence and acceptance purpose |
| --- | --- |
| Baseline c08 | Six original supported event claims with an unusable speech-only challenge route; preserve the separate failing expectation |
| w01 | Save, inspect, pause, resume, explicitly submit, confirm submission, request review, separately observe acceptance and review, receive a written response at tick 10, propose resolution, record resolution at tick 20, then preserve written disagreement and export |
| w02 | Preserve revision 1 and its timely response; save and submit a correction; reject an attempt to treat an old review as resolution of current work; review and respond to revision 2 at tick 19, preserving the late response and unavailable resolution separately |
| w03 | Pause after an attempted submission without confirmation; resume with the same draft and attempt; repeat the same explicit attempt without duplication; separately observe confirmation |
| w04 | Confirm submission and request review; record a written response without any acceptance observation or review note; keep unaccepted review and unavailable resolution visible after both targets elapse |
| w05 | Record explicit acceptance, review, and a response exactly at its target; observe the clock at and after the resolution target while resolution evidence remains unavailable |
| w06 | Apply one written transcript to two different hidden synthetic contexts; compare draft, status, error, history, export, repeated export, and a saved but unsubmitted correction against the same declared projections |

Every new transcript is expressed entirely in written operations. Their authored expectations can be exercised later; their presence here is not evidence that an interface is usable or that state survives an actual interruption.

## 7. Requirement mapping

| Requirement | Contract premise | Implementation obligation | Authored evidence target | Proposed response function and remaining assumption |
| --- | --- | --- | --- | --- |
| WC01 Written participation | Synthetic need is written exchange | Provide every required step and response through writing | w01 cp01, cp02, cp05; w03 cp02; retained baseline | Proposed participation function, unappointed; actual interaction exercise remains open |
| WC02 Preserve draft and submission identity | Exact draft text and explicit submission are distinct | Retain text, inspect exact revision, preserve an unconfirmed attempt, reconcile without duplication | w01 cp01-cp02; w03 cp01-cp04 | Proposed submission-reconciliation function, unappointed; actual persistence and transport are unspecified |
| WC03 Correct premises without erasure | Revisions name their predecessor and reviews name an exact revision | Preserve prior text and responses; prevent stale completion; keep an unsent draft distinct | w02 cp02-cp06; w06 cp07-cp08 | Proposed review function, unappointed; no change to a real record or the baseline model |
| WC04 Separate review and completion facts | Request, acceptance, review, response, proposal, and resolution are separate observations | Keep separate records; do not infer acceptance from response or resolution from response | w01 cp03-cp04; w04 cp01-cp04; w05 cp01-cp04 | Proposed continuity function, unappointed; no actual duty or accepted transfer is determined |
| WC05 Preserve timing uncertainty | Inclusive targets, incomplete observations, and correction-independent clock | Distinguish timely, late, target elapsed, and event evidence unavailable | w01 cp03-cp04; w02 cp06; w05 cp01-cp04 | Proposed follow-up function, unappointed; invented targets are not operational deadlines |
| WC06 Limit disclosure across the written route | Declared synthetic public projection | Match visible fields and text on all exercised surfaces for both variants | w06 cp01-cp08 | Proposed disclosure-review function, unappointed; authentication and general information-flow protection remain open |
| WC07 Preserve continuing agency | A recorded response or resolution is not agreement | Retain disagreement and correction; keep the written route available | w01 cp05; w02 cp06; w06 cp07-cp08 | Proposed participation-and-review function, unappointed; no claim about a person's consent or mental state |
| WC08 No downstream authority | Every event concerns only the authored challenge record | Emit no downstream action; retain `authority_status = not_established` | Every EventOutcome and checkpoint | No actual response function is appointed or authorized by this package |
| WC09 Separate source from evidence | Authored source, execution, review, and permission have distinct identities | Bind exact sources and candidate implementation; report actual outcomes separately | Bindings and the retained baseline expectation | Proposed source-review function, unappointed; empirical and professional review remain separate |

Checkpoint identifiers use their full case prefix, for example `w02.cp06`. The table's shortened `cpNN` labels refer to checkpoints in the named case. A range denotes the individually authored checkpoints in that range; it is not a claim that a run occurred.

## 8. Source binding and later acceptance

All four files are UTF-8 with LF line endings and a final newline. Bind the exact raw bytes of the three authored files using SHA-256, byte count, Git blob identity, and mode `100644` in `bindings.toml`. A Git blob identity is SHA-1 of `blob `, the decimal raw-byte length, a NUL, and the raw bytes. The binding file is selected through an independently selected repository revision or separately supplied digest; it does not contain a self-referential hash or commit pin. A hash identifies bytes but does not establish origin, authority, or adequacy.

The binding TOML is also closed. Its root has exactly `schema`, `suite_id`, `artifact_kind`, `expected_case_count`, `expected_variant_count`, `expected_authored_event_count`, `expected_authored_checkpoint_count`, `expected_instantiated_checkpoint_count`, `baseline_repository_revision`, `repository_revision`, `origin_and_authority`, `execution_outcomes`, `conceptual_direction`, `development`, and the `inputs` array of tables. Schema and suite are the values in section 1; `artifact_kind` is `authored-source-binding`. The five counts are respectively 6, 7, 75, 31, and 39. The baseline revision is the fixed revision in section 1. The remaining scalar fields are nonempty explanatory strings; `conceptual_direction` is `R.A. Jacob Martone`, and `development` is `AI-assisted authorship`. Each input table has exactly `path`, `mode`, `sha256`, `git_blob`, and `byte_count`. Paths are `specification.md`, `scenarios.json`, and `expectations.json` in that order; mode is `100644`; SHA-256 and Git blob identifiers are lowercase hexadecimal strings of length 64 and 40, respectively; byte count is a nonnegative integer. Unknown fields and missing or duplicate input paths are binding failures.

Future computational work must validate the closed schemas and source references before processing these transcripts. It must compare every event outcome and every applicable checkpoint against these separately authored expectations, including exact text, state, ordering, and projection. It must preserve the actual implementation identity, source identities, and outputs in a separately owned execution record. Source review and AI participation should be described accurately; separately authored expectations do not imply an independent human or professional review.

Written interaction, correction/review behavior, continuity, disclosure, source correspondence, and downstream-action absence require separate reported outcomes. No overall medical acceptance flag may erase the baseline interaction failure or an unresolved obligation. A passing finite replay would be bounded fixture agreement. Actual interaction usability, durable storage, deployment disclosure enforcement, coverage, professional interpretation, and permission to act remain unestablished by this source package.

## 9. Repository responsibilities

`grwtsk/medicine` owns these participation needs, event meanings, synthetic scenarios, acceptance expectations, and remaining medical obligations. `grwtsk/noeaaeue` owns any generic schema validation, transition processing, recovery interface, visible projection, fixture adapter, and execution evidence. `grwtsk/math` owns any general mathematical invariants or formal treatment of revision correspondence, timing, or information flow under explicit premises. No new implementation or proof is asserted by authoring these sources.

Conceptual direction and authorship: R.A. Jacob Martone. Development with AI-assisted authorship.
