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
primary evidence source, and persistent state is a compact index and map back to that evidence —
not a prose copy of the repository.

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
activates the procedure; it does not make this an accepted project protocol.

### 2. SNAPSHOT

Capture the starting repository state. At minimum record repository identity, branch where
relevant, committed base revision, and a working-tree fingerprint that covers staged, unstaged,
and relevant non-ignored untracked changes.

### 3a. BOOTSTRAP

When no usable persistent state exists, inspect the repository and construct the smallest state
that can support the expected query classes. Prefer maps, identifiers, and source pointers over
copied prose. Unknowns stay unknown.

### 3b. REFRESH

When usable state exists, update it from repository deltas since its indexed base revision and
from changes to the live working-tree overlay. Do not blindly rebuild everything when a bounded
delta is available. Fall back to bootstrap when history, identity, or state validation makes the
delta unreliable.

### 4. VALIDATE

Capture the ending repository state and compare it with the starting snapshot. If the base
revision, branch, or relevant working-tree fingerprint changed materially during inspection, do
not label the result current. Retry against a coherent snapshot or return `STALE` / `BLOCKED`
with the reason.

Only validated state may replace the previously validated persistent state.

### 5. QUERY

Answer one scoped external need from validated state and direct source inspection where needed.
Return the smallest packet sufficient for the request, not a maximal repository summary.

### 6. EXIT

The session may terminate after validated state and the query packet have been delivered. No
conversational memory is required for the next session; a fresh Steward begins again at
`ACCEPT`, reads the protocol and persistent state, and validates them against the repository.

## Persistent state contract

The storage format and mechanism are deliberately unspecified. Conceptually, persistent state
must contain at least:

- protocol version;
- repository identity;
- indexed commit or base revision;
- current branch where relevant;
- compact project purpose;
- architecture or component map;
- important entry points;
- local conventions and constraints;
- accepted architectural decisions with source pointers;
- important paths;
- recent relevant changes;
- known unresolved conflicts;
- freshness and validation information.

Each material claim should point to evidence at a known snapshot. Persistent state is a cache and
index; when it conflicts with current repository evidence, repository evidence wins and the state
must be refreshed or marked stale.

## Base state and live overlay

Committed knowledge and uncommitted work are separate truth layers.

### BASE STATE

Derived from the identified committed repository revision. It may describe project purpose,
architecture, rules, decisions, important paths, and other committed evidence.

### LIVE OVERLAY

Derived from staged changes, unstaged changes, and relevant non-ignored untracked files. It
describes current work and possible task overlap; it must not silently alter architectural facts
in the base state.

The Steward must:

- identify whether each overlay item is staged, unstaged, or untracked;
- surface overlap when a query concerns files or components already modified in the overlay;
- avoid ingesting ignored files and likely secrets into persistent context by default;
- discard or recompute the overlay when the working tree becomes clean;
- recompute the base and overlay when changes are committed;
- never promote an experimental uncommitted change into an accepted decision without committed
  evidence of that decision.

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
REQUEST:
STATUS: CURRENT | STALE | BLOCKED
SNAPSHOT: repository / base revision / branch / dirty fingerprint / validated at

RELEVANT FACTS:
APPLICABLE RULES AND DECISIONS:
AFFECTED AREAS:
LIVE OVERLAY / OVERLAP:
RISKS OR CONFLICTS:
SOURCE POINTERS:
UNKNOWNS:
```

Omit empty sections when their absence is unambiguous. Include enough source pointers for another
agent to verify load-bearing claims. If a query can be answered from three files, do not attach a
repository-wide summary.

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
surface the conflict wherever it can change the external decision.

## Portability hypothesis

This candidate makes a testable claim, not a demonstrated result:

> A fresh model session given the same protocol, repository, and persistent state should
> reconstruct approximately the same operational understanding without access to previous
> session history.

The comparison should evaluate source selection, evidence classes, identified constraints,
conflicts, and query usefulness — not identical wording.

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
protocol_version: repository-steward-candidate-v0.1
repository: example/repository
indexed_head: 4f2c1ab
branch: main
dirty_fingerprint: clean
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
```

## Where it breaks

- Very small or rarely revisited repositories may cost less to inspect directly.
- Generated, vendored, binary, or extremely large repositories may not yield a useful compact
  map without implementation-specific indexing choices.
- Weak source pointers turn the state into an unverifiable summary.
- An orchestrator may over-trust a fresh-looking packet and skip direct inspection for a
  high-consequence decision.
- Frequent repository churn may prevent a coherent refresh.
- Different models may classify evidence differently even when they share the same sources.

## Cost

Bootstrap consumes repository reads and produces persistent state that must be stored outside the
session. Every refresh adds snapshot, delta, and validation work. Query packets reduce repeated
context only if they stay narrow and the persistent map remains cheaper to validate than a fresh
full inspection. No token or time saving is claimed until field trials measure it.

## Open questions

- Which repository artifact should own persistent state without making the candidate dependent on
  one orchestration product?
- What counts as a material working-tree change for validation and retry?
- What observable threshold defines "approximately the same operational understanding" across
  fresh sessions?
- How should accepted decisions be recognized when repositories do not use explicit ADR states?
- When should a query force direct source rereading even after state validates as current?

## Notes / provenance

Formalized from an agentic multi-repository use case in which a global orchestrator repeatedly
rediscovered local repository context. The immediate next step is a real repository trial using
the project's [testing guide](../testing.md), not implementation or promotion.
