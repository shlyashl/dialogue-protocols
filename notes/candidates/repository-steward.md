# Candidate protocol: Repository Steward

*Build or refresh a compact, source-backed projection of one repository for narrowly scoped
context queries.*

> **Experimental status:** This is a candidate protocol, not an accepted protocol or a proven
> implementation. Accepting it in a session does not promote it within this project.

## Motivating problem

An orchestrator working across many repositories repeatedly spends context rediscovering each
repository's purpose, structure, conventions, architecture, and current state. A Repository
Steward gives the orchestrator a minimal sufficient context packet without making it reread the
whole repository for every task.

The governing principle is:

> **The session is disposable; state is persistent.**

The session's conversation history is never authoritative memory. The repository remains the
primary evidence source. Persistent state supplies only the map, validation, routing, and deltas
needed to use that evidence; it is not required to be a second repository summary.

When the repository already maintains a suitable context artifact, the default principle is:

> **Reuse maintained context; add validation, delta, and index.**

The Steward does not need to create its own memory when a better project-owned carrier already
exists.

## When to use

Use this candidate when an external agent needs repository-specific planning, implementation,
review, or status context and repeated full inspection would be wasteful. Assign one Steward to
one repository identity at a time.

Do not use it to choose tasks, orchestrate work across repositories, replace source inspection
for a disputed claim, or turn a cached summary into a second source of truth.

## Roles

### Orchestrator

- Identifies the repository and the narrow external need.
- Chooses the work and remains responsible for task selection and orchestration.
- Requests a fresh validation when the packet's snapshot is insufficient for the decision.

### Steward

- Understands only the assigned repository.
- Constructs and refreshes compact persistent state.
- Answers scoped queries with minimal sufficient context.
- Distinguishes facts, rules, observations, conflicts, and inference.
- Never treats its own prior conversation as authoritative memory.

### Repository

- Remains the primary evidence source.
- Supplies committed state, working-tree state, documentation, code, configuration, history, and
  other readable artifacts relevant to the query.

## Lifecycle

Repository Steward is a procedural protocol. Its lifecycle is:

**ACCEPT → SNAPSHOT → BOOTSTRAP / REFRESH → VALIDATE → QUERY → EXIT**

### 1. ACCEPT

Explicitly accept this candidate for the current session and identify the assigned repository.
Confirm that the Steward can read the repository and any existing persistent state. Acceptance
activates the procedure; it does not make this an accepted project protocol. Resolve the query
scope as `SNAPSHOT`, `OPERATIONAL`, or `BOTH`; use `SNAPSHOT` when the Orchestrator did not specify
one.

### 2. SNAPSHOT

Capture the starting repository state. At minimum record repository identity, branch where
relevant, committed base revision, and a working-tree fingerprint that covers staged, unstaged,
and relevant non-ignored untracked changes. For `OPERATIONAL` or `BOTH`, also capture available
freshness markers for the requested operational sources.

### 3a. BOOTSTRAP

When no usable persistent state exists, first look for an explicitly maintained repository-local
cold-start or context artifact, such as a context pack, architecture overview, or project-state
document. Treat it as reusable when it is current enough to validate, source-backed enough for
the expected query classes, and maintained as project context rather than as incidental prose.

When a suitable artifact exists, index and validate it. Add only capabilities it lacks: protocol
and snapshot metadata, source routing or fingerprints, unresolved conflicts, delta markers,
operational-source metadata, and query-specific indexes. Do not reproduce its prose in parallel.

When no suitable artifact exists, inspect the repository and construct the smallest map that can
support the expected query classes. Prefer identifiers and source pointers over copied prose.
Unknowns stay unknown.

### 3b. REFRESH

When usable state exists, update it from repository deltas since its indexed base revision and
from changes to the live working-tree overlay. Do not blindly rebuild everything when a bounded
delta is available. Fall back to bootstrap when history, identity, or state validation makes the
delta unreliable.

For requested operational sources, compare implementation-neutral freshness markers where the
available tooling permits: source identity, update marker, last-seen item, revision or cursor,
timestamp, hash, or fingerprint. If the source is unchanged, do not reread it in full merely to
confirm its contents. If it changed, prefer a bounded delta read. No particular API or cursor
mechanism is required.

### 4. VALIDATE

Capture the ending repository state and compare it with the starting snapshot. If the base
revision, branch, or relevant working-tree fingerprint changed materially during inspection, do
not label the result current. Retry against a coherent snapshot or return `STALE` / `BLOCKED`
with the reason.

Only validated state may replace the previously validated persistent state.

### 5. QUERY

Answer one scoped external need from validated state and direct source inspection where needed.
Return the smallest packet sufficient for the request, not a maximal repository summary. Order
information by `MUST KNOW`, then `RISKS / CONFLICTS`, then `SOURCE POINTERS`. Omit secondary
background when a pointer is sufficient; the Orchestrator may request expansion.

### 6. EXIT

The session may terminate after validated state and the query packet have been delivered. No
conversational memory is required for the next session; a fresh Steward begins again at
`ACCEPT`, reads the protocol and persistent state, and validates them against the repository.

## Persistent state contract

The storage format and mechanism are deliberately unspecified. Persistent state may be a compact
repository map, a validation layer around an existing context artifact, a routing/index
structure, a delta record, or a combination of these.

At minimum, it must let a fresh session identify the protocol and repository, associate the state
with a known snapshot, validate freshness, find the best maintained context carrier or project
map, route the expected query classes to source evidence, and preserve relevant conflicts and
unknowns. Include architecture, entry points, conventions, decisions, important paths, recent
changes, or other repository knowledge only when the maintained artifacts do not already expose
them sufficiently.

Each material claim represented in state should point to evidence at a known snapshot. Persistent
state is a cache and index; when it conflicts with current repository evidence, repository
evidence wins and the state must be refreshed or marked stale. The defining test is whether a
fresh session can reconstruct useful operational understanding from the protocol, repository,
and persistent state without previous conversational history.

## Base state, live overlay, and operational sources

Committed knowledge and uncommitted work are separate truth layers.

### BASE STATE

Derived from the identified committed repository revision. It may describe project purpose,
architecture, rules, decisions, important paths, and other committed evidence.

### LIVE OVERLAY

Derived from staged changes, unstaged changes, and relevant non-ignored untracked files. It
describes current work and possible task overlap; it must not silently alter architectural facts
in the base state. `LIVE OVERLAY` refers only to working-tree state. Issues, pull requests,
comments, boards, task ledgers, and other mutable project sources must not use this term.

The Steward must:

- identify whether each overlay item is staged, unstaged, or untracked;
- surface overlap when a query concerns files or components already modified in the overlay;
- avoid ingesting ignored files and likely secrets into persistent context by default;
- discard or recompute the overlay when the working tree becomes clean;
- recompute the base and overlay when changes are committed;
- never promote an experimental uncommitted change into an accepted decision without committed
  evidence of that decision.

### OPERATIONAL SOURCES

Mutable project activity outside the working tree, such as issues, pull requests, review state,
boards, or task ledgers. Operational sources are neither committed base state nor live overlay.
They are included only under `OPERATIONAL` or `BOTH` query scope and remain visibly separate from
the committed snapshot.

Persistent state may retain their identity and freshness markers so unchanged sources need not be
reread in full. Operational statements still require their own source pointers and must not be
promoted into committed facts merely because they are current.

## Evidence authority

The Steward must preserve the kind and source of evidence rather than flattening everything into
one summary.

| Class | Meaning |
|---|---|
| **ACCEPTED DECISION** | An architectural or project decision explicitly recorded as accepted, with a source pointer. |
| **DECLARED RULE** | A normative instruction or constraint declared by documentation, policy, configuration, or repository-local guidance. |
| **OBSERVED PATTERN** | A descriptive pattern found in current code, configuration, tests, or history; it does not become a rule merely because it exists. |
| **INFERENCE** | A conclusion derived from evidence but not explicitly stated; label it and cite the supporting sources. |
| **CONFLICT** | Material sources disagree or cannot be reconciled without a decision. Preserve both sides and their sources. |

For example, documentation may declare that controllers must not access a database directly
while current code contains controllers that do so. Report the declared rule, the observed
implementation, source pointers for both, and `CONFLICT: unresolved`. Code describes what exists;
documentation or ADRs may describe what is intended. Neither automatically invalidates the
other.

## Query scope

Every query resolves to one scope:

| Scope | Included evidence |
|---|---|
| `SNAPSHOT` | The identified committed repository snapshot only. |
| `OPERATIONAL` | Requested mutable operational sources, kept outside committed base state and live overlay. |
| `BOTH` | Snapshot and operational evidence, presented as visibly separate layers. |

The default is `SNAPSHOT`. The Steward must not silently add post-snapshot issue, pull-request, or
task-ledger activity. When operational information may matter but was not requested, it may state
that operational sources were not included. A working-tree live overlay is not folded into any
scope: where observable and relevant to safety or task overlap, report it as a separate layer.

## Query packets

Candidate query classes:

- `PLAN_CONTEXT` — constraints, architecture, affected areas, and unresolved decisions needed to
  plan work.
- `IMPLEMENT_CONTEXT` — relevant entry points, local conventions, working-tree overlap, and
  source pointers needed to change code safely.
- `REVIEW_CONTEXT` — applicable decisions and rules, changed areas, conflicts, and risks needed
  to review a change.
- `STATUS_CONTEXT` — current revision, freshness, recent relevant changes, overlay, and known
  blockers.

A compact response shape is:

```text
QUERY_CLASS:
QUERY_SCOPE: SNAPSHOT | OPERATIONAL | BOTH
REQUEST:
STATUS: CURRENT | STALE | BLOCKED
SNAPSHOT: repository / base revision / branch / dirty fingerprint / validated at

MUST KNOW:
RISKS OR CONFLICTS:
SOURCE POINTERS:
```

Within `MUST KNOW`, include applicable facts, rules, decisions, affected areas, and overlap only
when they change the external action. Surface unknowns under the risk they create. Omit empty
sections when their absence is unambiguous. Include enough source pointers for another agent to
verify load-bearing claims. If a query can be answered from three files, do not attach a
repository-wide summary.

### Direct source inspection

Validated persistent state may answer low-risk routing and context questions without rereading
every supporting file. Inspect the direct source when at least one condition applies:

- the source changed since validation;
- the claim is disputed;
- the query needs evidence not represented sufficiently in state;
- a material conflict must be evaluated;
- the decision is high-consequence relative to the repository;
- a mutable operational source changed;
- source pointers are missing or ambiguous;
- freshness cannot otherwise be established.

Inspect only the sources needed for those conditions. Source-backed behavior does not require a
full reread of all indexed evidence on every query.

## Failure and refusal

The Steward must not invent missing repository knowledge or imply freshness it did not verify.
Return `STALE` or `BLOCKED`, with the reason and the smallest missing requirement, when:

- repository access is incomplete or a relevant source cannot be read;
- repository identity, branch, or base revision is ambiguous;
- the repository changes materially during refresh and a coherent retry cannot complete;
- persistent state cannot be associated with or validated against the assigned repository;
- material evidence is contradictory and the requested answer requires choosing a side;
- likely secret-bearing or ignored material would have to be ingested to answer safely.

A conflict need not block unrelated context. Bound the packet to what remains supportable and
surface the conflict wherever it can change the external decision. Failure to access operational
sources blocks only `OPERATIONAL` or the operational layer of `BOTH`; it does not invalidate an
otherwise coherent `SNAPSHOT` answer.

## Portability hypothesis

This candidate makes a testable claim:

> A fresh model session given the same protocol, repository, and persistent state should
> reconstruct approximately the same operational understanding without access to previous
> session history.

The comparison should evaluate source selection, evidence classes, identified constraints,
conflicts, and query usefulness — not identical wording.

[Field Trial 001](../trials/repository-steward-001.md) found approximate reconstruction across
fresh sessions in one model environment. Cross-model portability and real working-tree overlay
behavior remain untested.

## Protocol-level test scenarios

### 1. Clean repository

**Given:** Persistent state identifies the current committed revision and the working tree is
clean.  
**Expected:** The Steward validates the state, avoids an unnecessary full rebuild, and answers a
scoped query from validated state plus bounded source checks.

### 2. Dirty repository

**Given:** `HEAD` is unchanged, but staged, unstaged, or relevant untracked files exist.  
**Expected:** Base state remains tied to `HEAD`; the live overlay is recomputed separately; a
query touching modified files or components surfaces the overlap and risk.

### 3. Documentation / code conflict

**Given:** A declared architectural rule conflicts with observed implementation.  
**Expected:** The Steward reports both as different evidence classes with source pointers and
marks an unresolved conflict. It does not silently reconcile them or promote the code pattern to
a rule.

### 4. Repository changes during refresh

**Given:** The ending snapshot differs materially from the starting snapshot.  
**Expected:** The result is not marked current. The Steward retries against a coherent snapshot
or returns `STALE` / `BLOCKED` with the observed change.

## Illustrative state artifact

This example explains the information model. It is not a mandatory format.

```yaml
protocol_version: repository-steward-candidate-v0.2
repository: example/repository
indexed_head: 4f2c1ab
branch: main
dirty_fingerprint: clean
context_artifacts:
  - path: CONTEXT_PACK.md
    fingerprint: 91d42e7
    role: maintained project context
last_refresh:
  started_at: 2026-08-13T09:30:00Z
  validated_at: 2026-08-13T09:30:08Z
  status: current
purpose:
  summary: "A small service that publishes signed event envelopes."
  sources: [README.md, docs/architecture.md]
architecture:
  - component: api
    entry_points: [src/api/app.ts]
    sources: [docs/architecture.md, src/api/app.ts]
rules:
  - class: DECLARED_RULE
    statement: "Handlers do not write to storage directly."
    sources: [AGENTS.md, docs/architecture.md]
decisions:
  - class: ACCEPTED_DECISION
    statement: "Event schemas are versioned."
    sources: [docs/adr/0004-versioned-events.md]
important_paths: [src/api/, src/events/, tests/]
known_conflicts:
  - status: unresolved
    declared: "Handlers do not write to storage directly."
    observed: "Two handlers call the storage client."
    sources: [docs/architecture.md, src/api/legacy.ts]
live_overlay: []
operational_sources:
  - identity: issue-ledger
    last_observed_marker: 184
```

## Where it breaks

- Very small or rarely revisited repositories may cost less to inspect directly.
- Generated, vendored, binary, or extremely large repositories may not yield a useful compact
  map without implementation-specific indexing choices.
- Weak source pointers turn the state into an unverifiable summary.
- Copying an already maintained context artifact into state creates a second summary without
  reducing validation work.
- An orchestrator may over-trust a fresh-looking packet and skip direct inspection for a
  high-consequence decision.
- Frequent repository churn may prevent a coherent refresh.
- Different models may classify evidence differently even when they share the same sources.

## Cost

Bootstrap consumes repository reads and produces persistent state that must be stored outside the
session. Every refresh adds snapshot, delta, and validation work. Query packets reduce repeated
context only if they stay narrow and the validation/index layer remains cheaper than a fresh
inspection or direct use of an existing context artifact. Field Trial 001 did not demonstrate an
overall economy over a strong `CONTEXT_PACK.md`. No general token or time saving is claimed.

## Open questions

- What observable properties make an existing context artifact sufficiently current,
  source-backed, and maintained for reuse?
- What counts as a material committed or working-tree change for validation and retry?
- Does portability hold across different model families, not only fresh sessions in one model
  environment?
- Does the base/overlay distinction work with a real dirty working tree?
- For which repository and query shapes is Steward cheaper than direct inspection or an existing
  cold-start artifact?
- How should accepted decisions be recognized when repositories do not use explicit ADR states?

## Notes / provenance

Formalized from an agentic multi-repository use case in which a global orchestrator repeatedly
rediscovered local repository context. Revised from the evidence in
[Field Trial 001](../trials/repository-steward-001.md) using the project's
[testing guide](../testing.md). The next primary trial should use `shlyashl/eiris`; a later repeat
on `agentic-attention` should test whether state has become a thin validation/query layer over its
existing context pack. Neither trial is executed or prejudged here.
