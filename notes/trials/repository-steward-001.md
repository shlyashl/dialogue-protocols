# Repository Steward — Field Trial 001

*A compact evidence record, not proof of general usefulness.*

## Trial identity

- **Candidate:** [Repository Steward](../candidates/repository-steward.md)
- **Candidate version tested:** PR #2 head
  `5b729ee3facbe2cd775a67a4325cd10d69dbc012`
- **Repository:** `shlyashl/agentic-attention`
- **Branch / frozen commit:** `v1` /
  `cb212d1cee15d1e7b5fb6eb055f899ee293a8602`
- **Task shape:** construct external persistent repository state, then answer status, planning, and
  review queries from fresh sessions without bootstrap conversation history.
- **Reason for entry:** test portability, correctness, repository rereading, bootstrap cost, and
  comparative value against the repository's maintained `CONTEXT_PACK.md`.

The query intents and measurement plan were frozen before experimental sessions inspected the
repository. Raw session logs remain outside this public repository and are not published here.
This record preserves the observed outcome without reproducing private or tool-specific logs.

## Arms

| Arm | Starting condition |
|---|---|
| A — natural cold start | Fresh session with repository access and one query; no protocol or Steward state. |
| B — existing context pack | Fresh session instructed to begin with `CONTEXT_PACK.md`; no protocol or Steward state. |
| C1 — bootstrap | Fresh session with the exact candidate, repository access, and empty external state. |
| C2 — Steward query | Fresh sessions with the exact candidate, frozen C1 state, repository access, and one query; no C1 conversation. |

A second independent C2 planning query used the same frozen state as a portability replicate.

## Observed result

| Category | Result |
|---|---|
| Portability | **PASS within one model environment.** Fresh sessions reconstructed approximately the same load-bearing facts, evidence classes, constraints, conflicts, and unknowns. Cross-model portability was not tested. |
| Correctness | **PASS with a minor omission.** No unsupported load-bearing claim was found; one review packet omitted an explicit historical baseline that remained available in state. |
| Context economy vs natural cold start | **Positive in this trial.** Steward sessions reread less repository material by observable source-volume proxies. These were bytes/characters, not token measurements. |
| Context economy vs `CONTEXT_PACK.md` | **Not demonstrated overall.** The three Steward query sessions had approximately the same total observable input volume as the context-pack arm. |
| Bootstrap economy | **Negative on this repository.** The produced state slightly exceeded the maintained context pack in size and duplicated much of its function. |
| Review specialization | **Promising.** The Steward review packet was the smallest of the three review arms while preserving evidence authority and conflicts. |
| State fidelity | **PASS.** The state retained source pointers, evidence classes, uncertainty, and committed-versus-post-base separation. |
| Dirty working-tree overlay | **NOT TESTED.** Available repository access could not observe or safely synthesize staged, unstaged, and untracked state. |

Bootstrap cost was recorded separately from query cost. The trial does not claim general token,
time, or context savings.

## Defects discovered

1. `LIVE OVERLAY` was incorrectly reused for mutable issue activity even though the contract
   defined it as working-tree state.
2. Post-base issue activity could enter a commit-scoped query without an explicit scope request.
3. The bootstrap created a second summary beside a strong maintained `CONTEXT_PACK.md`.
4. Unchanged mutable sources could be reread in full because no bounded refresh rule existed.
5. The contract did not say when validated state is sufficient and when a direct-source reread is
   required.
6. Packet minimization had no priority order, so equally correct fresh sessions varied in scope.

## Verdict and next trial

**Recommendation: REVISE.**

The revision should treat maintained repository context as a reusable carrier and add only
validation, routing, fingerprints, conflicts, deltas, and operational metadata. It should also
separate working-tree overlay from mutable operational sources and make query scope explicit.

The next primary trial should target `shlyashl/eiris`, a larger multi-component engineering
repository that contrasts with `agentic-attention` and its unusually strong cold-start artifact.
After that, repeat the trial on `agentic-attention` to test whether revised Steward state behaves
as a thin validation/query layer over `CONTEXT_PACK.md` rather than as a duplicate summary.

Neither follow-up trial has been run, and the candidate remains experimental.
