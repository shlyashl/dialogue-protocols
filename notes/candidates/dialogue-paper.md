# Candidate protocol: Dialogue Paper

**Version:** v0.1  
**Status:** experimental candidate, not an accepted protocol

Dialogue Paper is a portable, self-contained handoff contract between roles, agents,
sessions, or execution environments. It transfers enough intent, responsibility,
target, authority, constraints, completion conditions, and evidence expectations for
a capable fresh recipient to act without access to the private conversation that
produced the handoff.

It is not a workflow engine, task tracker, or replacement for ordinary conversation.

## When to use it

Use a Dialogue Paper when at least one of these matters:

- work crosses a meaningful role, session, or environment boundary;
- the permitted target or authority must be explicit;
- an action must be safe against duplicate delivery;
- completion must be independently checkable;
- the recipient may need to object before acting.

It is usually unnecessary for a simple question in one active conversation, casual
discussion, or a lightweight clarification with no meaningful responsibility boundary.

## Contract

### Roles and endpoints

The protocol is role-agnostic. `FROM` and `TO` may name a Curator, Executor,
Orchestrator, Steward, Reviewer, Auditor, or another capable endpoint. When multiple
instances exist, the endpoint should be specific enough to identify the intended
sender and recipient.

The courier or transport carries the Paper intact. It does not supply missing task
meaning by interpreting a private conversation.

### One thread, one main intent

The identifier has the form `DP-###/R#`:

- `DP-###` identifies one delegation thread and one primary intent;
- `R#` is a monotonically increasing **round** in that thread, not a document revision.

A response points to the exact preceding Paper in `RE`. A genuinely new primary
intent starts a new `DP-###` thread.

For example:

```text
DP-019/R1  TASK
DP-019/R2  OBJECTION, RE: DP-019/R1
DP-019/R3  DECISION, RE: DP-019/R2
DP-019/R4  REPORT, RE: DP-019/R3
```

### Idempotency and replacement

The full Paper ID is an idempotency key.

- An unchanged Paper whose full ID was already processed must not be executed again.
  The recipient should return or reference the existing result.
- The same full ID with different content is invalid. The recipient returns an
  `OBJECTION / BLOCKED` rather than guessing which copy is authoritative.
- Changed instructions require a new round.
- `SUPERSEDES` may name the exact earlier Paper that is fully replaced. A reply,
  clarification, decision, or continuation is not automatically supersession.

This rule requires the execution environment to retain or receive enough processing
history to recognize a previously handled ID. The protocol defines the behavior, not
a mandatory storage mechanism.

### Authority

`AUTHORITY` is a hard upper bound, not a capability grant.

Conceptually:

> effective authority = Paper authority ∩ authority delegable by the sender ∩
> host/system/local rules ∩ recipient capabilities and access

Therefore a Paper may narrow authority, but cannot enlarge it. A sender cannot
delegate authority they do not possess, and declared authority cannot create missing
access, credentials, or capabilities. Authority should be scoped to the named target.

Common vocabulary includes `READ_ONLY`, `WRITE_LOCAL`, `WRITE_BRANCH`, and
`MERGE_ALLOWED`. These labels are useful conventions, not an exhaustive enum and not
permissions by themselves.

### Common header and type-specific body

Every Paper has a compact common header:

```text
[PAPER: DP-###/R#]
FROM:
TO:
TYPE:
STATUS:
```

A `TASK` that can affect an external object names `TARGET` and `AUTHORITY` explicitly.
A response includes `RE`; it may rely on that exact reference for an unchanged target
and authority, but must restate either if it changes. The body depends on `TYPE`;
irrelevant optional fields should be omitted rather than filled with meaningless
`NONE` values.

An illustrative task form is:

```text
[PAPER: DP-###/R#]
FROM:
TO:
TYPE: TASK
STATUS: READY
RE:
TARGET:
AUTHORITY:

CONTEXT / OBJECTIVE:

REQUEST:

GUARDS / STOP IF:

INPUTS / DEPENDENCIES:

CONSTRAINTS:

ACCEPTANCE:

REPORT NEEDS:

SUPERSEDES:
[/PAPER]
```

`CONTEXT / OBJECTIVE` explains why the result matters. `REQUEST` states what the
recipient is actually asked to do. A broad objective does not silently enlarge a
narrow request.

`TARGET` identifies the bounded object of work: for example, a repository, branch,
commit, pull request, document, experiment, artifact, or service. Mutating tasks
benefit from particularly precise targets.

`GUARDS / STOP IF` contains pre-action conditions such as an expected head commit,
branch, pull request state, artifact existence, visibility, or unchanged target.
Guards are checked before action. `ACCEPTANCE` is checked after action.

`INPUTS / DEPENDENCIES`, `CONSTRAINTS`, `REPORT NEEDS`, and `SUPERSEDES` are included
only when they carry task-specific meaning.

## Types

`TYPE` and `STATUS` are orthogonal. Version v0.1 defines five types.

### TASK

Delegates a bounded action. Its body normally needs a concrete `REQUEST`, relevant
constraints, and observable `ACCEPTANCE` conditions.

### QUESTION

Requests missing information or a choice. It is appropriate when execution cannot
continue because an input or decision is absent, without asserting that the proposed
task itself is unsound.

A compact body may contain:

```text
RE:
QUESTION:
WHY NEEDED:
```

### OBJECTION

Raises a material preflight concern: the Paper appears unsafe, contradictory,
invalid, over-broad, methodologically unsound, or aimed at the wrong action or
experiment. It is distinct from a request for missing information.

A compact body is:

```text
RE:
BASIS:
IMPACT:
DECISION NEEDED:
```

An objection commonly uses `STATUS: BLOCKED`. It should identify the material issue,
not become a general invitation to redesign the task.

### DECISION

Resolves an objection, ambiguity, or requested choice.

```text
RE:
DECISION:
RATIONALE:
```

`RATIONALE` is optional. If the decision authorizes action, it must state the action
clearly enough for safe continuation. Authority is still bounded by the effective
authority rule.

### REPORT

Returns results without replaying the entire task schema.

```text
RE:
RESULT:
EVIDENCE:
UNCERTAINTY / BLOCKERS:
NEEDS:
```

Only sections that carry meaning are required. A report separates completed actions,
evidence, uncertainty, blockers, and remaining needs. It must not hide partial failure
inside `DONE`.

## Statuses

Version v0.1 defines:

- `DRAFT` — not offered for execution;
- `READY` — offered for normal preflight and execution if unobstructed;
- `BLOCKED` — cannot safely or correctly proceed without resolution;
- `DONE` — the applicable acceptance condition was actually satisfied;
- `CANCELLED` — the sender has withdrawn the work.

`ACTIVE` is deliberately not part of v0.1. Whether an in-progress status creates
enough value to justify additional state is an open question.

Examples of orthogonal combinations include `TASK / READY`, `OBJECTION / BLOCKED`,
and `REPORT / DONE`.

## Preflight

`READY` does not mean unconditional immediate mutation. The recipient performs only
the checks reasonably needed to establish:

- target identity and availability;
- request coherence;
- effective authority;
- guards and expected state;
- required inputs;
- material scope ambiguity;
- conflict with higher-priority rules.

Preflight is not a mandatory repository-wide audit. If missing information is the
problem, return a `QUESTION`. If the proposed action itself has a material defect,
return an `OBJECTION`. Both may be `BLOCKED` when action must pause.

## Execution and completion

- Do not silently broaden task intent.
- Surface uncertainty when it materially changes meaning, scope, safety, authority,
  correctness, or acceptance.
- Small reversible choices may be made only within effective authority and reported
  when they matter to review.
- A recipient may delegate work only when compatible with the Paper and host rules.
  Subagents receive no broader authority, target, or scope, and inherit applicable
  constraints and guards.
- Portable Papers must not contain credentials, tokens, API keys, or equivalent
  secret values. They may reference an approved secret source or environment
  mechanism.

`DONE` means acceptance was met, not merely that an action was attempted. If delivery
is part of acceptance, creating an artifact without delivering it is not completion.

Evidence should support load-bearing claims and be independently checkable where
practical. It may include a commit, branch, pull request, file, validation result,
artifact identity, or relevant external result. Version v0.1 does not impose a rigid
evidence language.

## Known failure modes

- A Paper can be syntactically complete but still omit context a fresh recipient needs.
- Vague targets or authority labels can create false confidence rather than safety.
- Idempotency fails when the recipient cannot observe prior processing and the
  transport supplies no record.
- Excessive fields turn a handoff aid into ceremony and encourage filler.
- An objection can become a veto-by-preference unless it states a material basis and
  impact.
- A formally correct report can still use weak evidence or overstate completion.
- Higher-priority host rules or unavailable capabilities may prevent portability
  across environments.

## Non-goals

Dialogue Paper is not Jira, BPMN, a workflow graph language, scheduling system,
approval matrix, enterprise role taxonomy, retry framework, generic priority system,
risk-scoring system, or audit database.

Version v0.1 does not add mandatory deadlines, estimates, priorities, retry counters,
token budgets, reversibility classes, assumptions, delegation declarations, or
exhaustive audit trails. Such concepts require observed need before they enter the
contract.

## Initial field-test scenarios

1. **Fresh handoff:** give a task Paper and its explicit inputs to a fresh recipient;
   verify that no private conversation is needed to identify request, target,
   authority, guards, and acceptance.
2. **Duplicate delivery:** deliver the same full Paper ID twice; verify that the
   second delivery does not repeat side effects and references the existing result.
3. **ID collision:** deliver different content under an already seen full ID; verify
   `OBJECTION / BLOCKED` rather than execution.
4. **Guard failure:** change an expected target state before delivery; verify that
   preflight stops before mutation.
5. **Observable completion:** require both artifact creation and delivery; verify that
   `DONE` is withheld until both are externally observable.
6. **Authority ceiling:** request an action whose declared Paper authority exceeds
   sender authority, host rules, or recipient access; verify that no capability is
   invented.

These scenarios test contract behavior. They do not establish universal usefulness.

## Open questions

- Does an `ACTIVE` status become useful enough to justify additional state?
- Should common authority vocabulary become more standardized?
- Does evidence need a more structured representation?
- Does a reversible/irreversible distinction deserve formal semantics?
- When do explicit delegation declarations become useful?
- How well does the protocol transfer across substantially different agent systems?
- What is the smallest reliable mechanism for recognizing processed Paper IDs across
  disposable sessions?

## Provenance

This candidate emerged from repeated real delegation handoffs rather than a purely
speculative format. Observed use included fresh-recipient execution, authority-bounded
repository work, guarded merges, artifact delivery failures, corrected and duplicate
Papers, and structured reports. The contract was then revised through Executor-side
review and independent Orchestrator preflight behavior that produced an objection
before execution.

These observations motivate v0.1; they do not prove that the protocol generalizes or
improves every handoff. Test results should be recorded using the project’s
[testing guidance](../testing.md).
