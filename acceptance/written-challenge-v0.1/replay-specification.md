# Written challenge source projection v0.1

This package materializes the already authored synthetic written-challenge
requirements for an explicit generic replay interface. The original
[specification](specification.md), [scenarios](scenarios.json),
[expectations](expectations.json) and [bindings](bindings.toml) remain unchanged
from source commit `2337d11ce9f50a8a075723254f1a38bf014cd84d`.

Conceptual direction and authorship: **R.A. Jacob Martone**. Source projection
and review with AI assistance. These are invented scenario inputs, with no
patient records or professional acceptance decision.

## Exact source mapping

| Artifact | Responsibility |
| --- | --- |
| [replay-vectors.json](replay-vectors.json) | Exact UTF-8 transcript strings, input IDs, source case/variant IDs, sizes, digests, and the declared mapping |
| [replay-corpus.json](replay-corpus.json) | Generic corpus envelope with copied authored event outcomes and state/projection checkpoints |
| [replay-bindings.toml](replay-bindings.toml) | Identities of the original four authored files and two replay input artifacts |

The mapping copies the fixed timing policy and every authored event. It copies
every expected event outcome, state field, projection field, text value, and
array order. The only expected-value translation changes the projection schema
tag from `grwtsk.medicine.written-challenge-visible-projection/1` to
`noe.written-challenge-visible-projection/1`. No expected state is calculated
from implementation behavior.

The generic envelope uses `noe.written-challenge-transcript/1`, and the corpus
uses `noe.written-challenge-corpus/1` with profile `noe.written-challenge/1`.
The materialized corpus has seven variant cases. The six original transcripts
contain 75 authored events and 31 authored checkpoints; instantiating their
variants produces 90 event outcomes and 39 checkpoints for comparison. Each
checkpoint compares both its entire authored state and its authored written
projection. The original requirements remain the authority for their medical
meaning.

## Context and disclosure boundary

Case titles, requirement IDs, participant-need metadata and offered-route
metadata do not become generic transition inputs. Variant `internal_context`
is also explicitly omitted. Its model text, counts, witness IDs, diagnostic
text and hidden note remain authored source material.

The two context variants therefore produce identical public transcript bytes.
Comparing their replay projections can establish agreement after that explicit
omission. It cannot establish information-flow security for a system that
actually consumes private context, enforcement of a deployed disclosure policy,
or the safety of exposing the complete audit result to a participant.

## Reading a comparison result

An implementation can compare all 90 event outcomes and both snapshots at each
of the 39 checkpoints. Separate shape and authority checks may cover all
events, but an uncheckpointed event has no complete authored state oracle in
this package. Every discrepancy must remain visible; a comparison must not
change an expected value to match an observed result.

The bindings describe source preparation, so their
`engine_execution_performed = false` field records the role of this artifact.
A later implementation run is separate evidence and does not rewrite that
source-preparation fact. Generic implementation and operational evidence belong
to `grwtsk/noeaaeue`; pure mathematical definitions and proofs belong to
`grwtsk/math`. Coordination remains in [issue #1](https://github.com/grwtsk/medicine/issues/1) and
medical acceptance work in [issue #2](https://github.com/grwtsk/medicine/issues/2).

The earlier communication case `c08` retains
`interaction_outcome = challenge_route_unusable` and
`overall_acceptance = not_established`. Agreement with this synthetic written
route does not erase that earlier observation. A headless transition model
does not establish that a person can use the route, that data survives process
loss, that an institution has accepted a challenge, or that care can change.

Accessible interaction, continuity and recovery, actual disclosure enforcement,
clinical interpretation, organizational review and permission to act each need
their own evidence. This source mapping supplies no legal or regulatory
compliance determination and no clinical deployment approval.
