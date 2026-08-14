# Idea incubator

*Open hypotheses, not a roadmap.*

This incubator holds ideas that have not been accepted as project decisions. Their presence does
not create an obligation to implement them, and no active protocol changes merely because an
idea is recorded here. Before an idea changes a protocol, it should be discussed and, when
possible, tested on real work using the [`testing guide`](testing.md).

Some source conversations may not be public or preserved. Each entry is therefore a compact,
autonomous paraphrase rather than a claim to reproduce the original transcript. `ORIGIN` records
where an idea entered this project — user, assistant, or joint synthesis — not exclusive
intellectual ownership.

A new idea may enter as `RAW`, `DISCUSS`, `TEST`, or `PARK`. Moving it to `PROMOTE` requires a
reviewed discussion or field evidence and only means that a separate change should be considered.
`DROP` preserves a rejected hypothesis instead of erasing its history. These statuses describe
epistemic disposition, not priority.

## Entry schema

```text
ID:
ORIGIN: USER | ASSISTANT | SYNTHESIS
SCOPE: CORE | UX | RESEARCH | TOOLING
STATUS: RAW | DISCUSS | TEST | PARK | DROP | PROMOTE

IDEA:
A short autonomous statement.

OPEN QUESTION:
The main question before the next step.
```

## A. Packaging and access

### A1 — Protocol skill

**ID:** A1  
**ORIGIN:** USER  
**SCOPE:** TOOLING  
**STATUS:** DISCUSS

**IDEA:** Package the contracts as a skill or analogous mechanism that makes them available to
the model and easier to activate.

**OPEN QUESTION:** Does a skill solve a real contract-transfer problem, or bind the project to
one product too early?

### A2 — Short video demonstrations

**ID:** A2  
**ORIGIN:** USER  
**SCOPE:** UX  
**STATUS:** PARK

**IDEA:** Explain protocols through short video demonstrations rather than documentation alone.

**OPEN QUESTION:** Is there enough observed behavior to demonstrate publicly without overstating
usefulness?

### A3 — English and Chinese versions

**ID:** A3  
**ORIGIN:** USER  
**SCOPE:** RESEARCH  
**STATUS:** PARK

**IDEA:** Test whether protocols transfer across languages and cultures of communication.

**OPEN QUESTION:** Should the contracts be translated first, or should the test ask whether their
function survives independent adaptation?

### A4 — Copyable controls

**ID:** A4  
**ORIGIN:** USER  
**SCOPE:** UX  
**STATUS:** DISCUSS

**IDEA:** Provide easy-to-copy phrases for entering, leaving, and switching protocols.

**OPEN QUESTION:** Do they reduce user effort without implying that nonexistent interface
commands are available?

### A5 — Select the next concept

**ID:** A5  
**ORIGIN:** USER  
**SCOPE:** UX  
**STATUS:** TEST

**IDEA:** Let the user select or copy a term from an answer as the next object to define.

**OPEN QUESTION:** How can selection stay convenient without letting the model impose the route
of exploration?

## B. Definitions as knowledge navigation

### B1 — Guided knowledge surfing

**ID:** B1  
**ORIGIN:** USER  
**SCOPE:** CORE  
**STATUS:** DISCUSS

**IDEA:** `definitions` may support not only short answers but guided movement through knowledge,
with the user choosing the next node.

**OPEN QUESTION:** Is this part of the current `definitions` protocol or a separate navigation
protocol?

### B2 — Knowledge level revealed through navigation

**ID:** B2  
**ORIGIN:** USER  
**SCOPE:** CORE  
**STATUS:** DISCUSS

**IDEA:** The model need not guess the human's knowledge level in advance; the human's choices of
subsequent definitions may gradually reveal the useful depth and direction.

**OPEN QUESTION:** Which choices genuinely indicate knowledge, and which indicate only current
interest?

### B3 — Optional next doors

**ID:** B3  
**ORIGIN:** SYNTHESIS  
**SCOPE:** UX  
**STATUS:** TEST

**IDEA:** After an atomic answer, show two or three optional terms for continuation without
explaining them in advance.

**OPEN QUESTION:** Do these doors reduce steering cost, or quietly let the model direct the
exploration?

### B4 — Assemble the travelled path

**ID:** B4  
**ORIGIN:** USER  
**SCOPE:** CORE  
**STATUS:** DISCUSS

**IDEA:** After a chain of definitions, assemble the concepts and relations travelled into a
coherent text or audio lecture.

**OPEN QUESTION:** Should this be the completion of `definitions`, a transition into `lecture`,
or a separate protocol?

### B5 — Context refresh

**ID:** B5  
**ORIGIN:** USER  
**SCOPE:** CORE  
**STATUS:** DISCUSS

**IDEA:** Create a way to restore the path travelled, conclusions reached, open questions, and
the point where work stopped.

**OPEN QUESTION:** How is a useful context restoration different from an ordinary summary of the
chat history?

### B6 — Spaced revisiting

**ID:** B6  
**ORIGIN:** USER  
**SCOPE:** RESEARCH  
**STATUS:** PARK

**IDEA:** Explore returning to learned concepts at intervals to reinforce understanding.

**OPEN QUESTION:** Which findings from memory research apply to dialogic learning without
turning this project into an education system?

## C. Consent, refusal and exits

### C1 — Contract comprehension check

**ID:** C1  
**ORIGIN:** USER  
**SCOPE:** CORE  
**STATUS:** DISCUSS

**IDEA:** Before activation, the model briefly restates the contract in language suited to the
user and asks for confirmation.

**OPEN QUESTION:** When does confirmation prevent an error, and when does it add ceremony?

### C2 — Model refusal

**ID:** C2  
**ORIGIN:** USER  
**SCOPE:** CORE  
**STATUS:** DISCUSS

**IDEA:** The model may refuse to accept or continue a protocol when it is contradictory,
infeasible, or observably harming the task.

**OPEN QUESTION:** Which externally checkable grounds should justify such a refusal?

### C3 — Mutual acceptance

**ID:** C3  
**ORIGIN:** SYNTHESIS  
**SCOPE:** CORE  
**STATUS:** DISCUSS

**IDEA:** The human selects the desired mode, the model states whether it can honestly follow the
contract, and work begins only after mutual acceptance.

**OPEN QUESTION:** Which decisions must always remain with the human, and which concern the
model's execution limits?

### C4 — Out-of-protocol note

**ID:** C4  
**ORIGIN:** USER  
**SCOPE:** UX  
**STATUS:** TEST

**IDEA:** Allow the model to visually separate an optional note that does not fit the active
protocol's form.

**OPEN QUESTION:** How can this avoid becoming a loophole for routine contract violations?

### C5 — Critical warnings stay primary

**ID:** C5  
**ORIGIN:** SYNTHESIS  
**SCOPE:** CORE  
**STATUS:** DISCUSS

**IDEA:** A critical warning must not be hidden in an optional block or suppressed by the
protocol's form.

**OPEN QUESTION:** How can criticality be defined through observable consequences rather than a
model's subjective-sounding impression?

### C6 — Model-proposed protocol

**ID:** C6  
**ORIGIN:** USER  
**SCOPE:** CORE  
**STATUS:** DISCUSS

**IDEA:** The model may recognize a recurring difficulty and propose a protocol, but may not
activate it autonomously.

**OPEN QUESTION:** How can proposals remain rare and useful instead of turning conversation into
mode configuration?

### C7 — Protocol drift detector

**ID:** C7  
**ORIGIN:** ASSISTANT  
**SCOPE:** RESEARCH  
**STATUS:** TEST

**IDEA:** During use, check whether the current task still matches the original reason for
entering the protocol.

**OPEN QUESTION:** How often can this check run before becoming a separate burden?

### C8 — Exit latency

**ID:** C8  
**ORIGIN:** ASSISTANT  
**SCOPE:** RESEARCH  
**STATUS:** TEST

**IDEA:** Measure the number of turns between the first observable mismatch and a proposed or
actual exit.

**OPEN QUESTION:** Can the first mismatch be identified reliably from a preserved dialogue?

### C9 — Repair without restart

**ID:** C9  
**ORIGIN:** ASSISTANT  
**SCOPE:** CORE  
**STATUS:** DISCUSS

**IDEA:** After a local protocol violation, allow one explicit repair turn without fully exiting
and re-entering.

**OPEN QUESTION:** Which observable violations can be repaired locally, and which indicate a
genuine mismatch that requires exit?

## D. Model-side operational cost

### D1 — Model-side operational cost

**ID:** D1  
**ORIGIN:** USER  
**SCOPE:** RESEARCH  
**STATUS:** DISCUSS

**IDEA:** Describe a protocol's cost to the model through observable factors: ambiguity,
instruction conflict, additional context, and inability to report failure honestly.

**OPEN QUESTION:** Which factors can be tested externally without pretending to access the
model's internal state?

### D2 — Symmetric design exercise

**ID:** D2  
**ORIGIN:** USER  
**SCOPE:** RESEARCH  
**STATUS:** DISCUSS

**IDEA:** For each convenience on the human side, look for a possible analogue on the model side
and vice versa, recording where the symmetry breaks.

**OPEN QUESTION:** Does the exercise reveal real requirements, or create a false anthropomorphic
symmetry?

### D3 — Style adaptation

**ID:** D3  
**ORIGIN:** USER  
**SCOPE:** CORE  
**STATUS:** RAW

**IDEA:** Explore a contract that adapts textual form to a user or author, reducing manual editing
without blindly imitating a personality.

**OPEN QUESTION:** Which style elements may be adapted, and how should authorship of the final
text remain clear?

### D4 — Conversational mode

**ID:** D4  
**ORIGIN:** USER  
**SCOPE:** CORE  
**STATUS:** DISCUSS

**IDEA:** Explore a short, natural dialogue mode without lectures or a complete formal analysis
of every claim.

**OPEN QUESTION:** Is it sufficiently different from `default` and a brief `resonator` to deserve
a separate protocol?

### D5 — Protocol budget

**ID:** D5  
**ORIGIN:** ASSISTANT  
**SCOPE:** RESEARCH  
**STATUS:** TEST

**IDEA:** Treat additional turns, confirmations, and context as protocol cost; use a protocol when
the confusion it is likely to prevent would cost more.

**OPEN QUESTION:** What is the smallest useful cost estimate that does not become a complex
metric?

## E. Testing and research

### E1 — Record model, version and date

**ID:** E1  
**ORIGIN:** USER  
**SCOPE:** RESEARCH  
**STATUS:** DISCUSS

**IDEA:** Tie trials to the model, any available version or identifier, and the date.

**OPEN QUESTION:** How should model identity be recorded when a product does not expose an exact
version?

### E2 — Cross-model trials

**ID:** E2  
**ORIGIN:** USER  
**SCOPE:** RESEARCH  
**STATUS:** TEST

**IDEA:** Test the same protocols on several available models.

**OPEN QUESTION:** Should trials compare literal contract compliance, functional outcome, or the
two levels separately?

### E3 — Real historical tasks

**ID:** E3  
**ORIGIN:** USER  
**SCOPE:** RESEARCH  
**STATUS:** TEST

**IDEA:** Use anonymized historical requests in which real interaction difficulties were already
observed.

**OPEN QUESTION:** How can the task shape be preserved while personal and sensitive details are
removed?

### E4 — Independent review session

**ID:** E4  
**ORIGIN:** USER  
**SCOPE:** TOOLING  
**STATUS:** TEST

**IDEA:** Use a separate model or session to critique protocols, revisions, and trial results.

**OPEN QUESTION:** How can differences in model taste be kept from masquerading as substantive
defects?

### E5 — Human memory and attention research

**ID:** E5  
**ORIGIN:** USER  
**SCOPE:** RESEARCH  
**STATUS:** PARK

**IDEA:** Study research on human memory, attention, and learning that is relevant to the form of
dialogue protocols.

**OPEN QUESTION:** Which findings are stable enough and directly relevant to interaction with
LLMs?

### E6 — LLM instruction-following research

**ID:** E6  
**ORIGIN:** USER  
**SCOPE:** RESEARCH  
**STATUS:** PARK

**IDEA:** Study work on instruction drift, contextual constraints, user adaptation, and the
effects of meta-instructions.

**OPEN QUESTION:** Which laboratory findings transfer to long, natural conversations?

### E7 — Shadow comparison

**ID:** E7  
**ORIGIN:** ASSISTANT  
**SCOPE:** RESEARCH  
**STATUS:** TEST

**IDEA:** Compare the same task shape in ordinary conversation and under a protocol to observe
the actual change.

**OPEN QUESTION:** How can the second response be prevented from winning merely because it is an
additional attempt?

### E8 — Portable contract check

**ID:** E8  
**ORIGIN:** ASSISTANT  
**SCOPE:** RESEARCH  
**STATUS:** TEST

**IDEA:** Give a contract to a new model without project history and ask it to restate duties,
boundaries, and exit conditions.

**OPEN QUESTION:** What degree of divergence indicates that the contract is not autonomous
enough?

### E9 — Tired-user test

**ID:** E9  
**ORIGIN:** USER  
**SCOPE:** UX  
**STATUS:** TEST

**IDEA:** Test whether a tired person in the evening can use the testing instructions without
research discipline.

**OPEN QUESTION:** Which parts of the record will a person actually complete without reminders
or external help?

### E10 — Rule ablation

**ID:** E10  
**ORIGIN:** ASSISTANT  
**SCOPE:** RESEARCH  
**STATUS:** TEST

**IDEA:** Remove one rule at a time to distinguish functionally necessary parts of a contract
from text that only increases cost.

**OPEN QUESTION:** In noisy conversations, how can a change in outcome be attributed specifically
to the removed rule?

### E11 — Negative-fit trials

**ID:** E11  
**ORIGIN:** ASSISTANT  
**SCOPE:** RESEARCH  
**STATUS:** TEST

**IDEA:** Test a protocol on tasks it clearly should not fit, checking whether activation is
declined or exit occurs promptly.

**OPEN QUESTION:** How can fair non-fit tasks be selected without designing an artificially easy
failure?

## F. Candidate protocols

### F1 — Idea Queue

**ID:** F1  
**ORIGIN:** USER  
**SCOPE:** CORE  
**STATUS:** DISCUSS

**IDEA:** Preserve a set of thoughts, then select and examine them one at a time without losing
the rest.

**OPEN QUESTION:** Is this a dialogue protocol or ordinary backlog management?

### F2 — Context Refresh

**ID:** F2  
**ORIGIN:** USER  
**SCOPE:** CORE  
**STATUS:** DISCUSS

**IDEA:** Restore the prior context, conclusions reached, open questions, and current point of
work.

**OPEN QUESTION:** What minimum structure genuinely restores the human's context?

### F3 — Conversational

**ID:** F3  
**ORIGIN:** USER  
**SCOPE:** CORE  
**STATUS:** DISCUSS

**IDEA:** Work through short, natural turns closer to ordinary human conversation.

**OPEN QUESTION:** Which recurring problem does this contract solve that `default` does not?

### F4 — Style Fit

**ID:** F4  
**ORIGIN:** USER  
**SCOPE:** CORE  
**STATUS:** RAW

**IDEA:** Agree on response-form parameters so the result requires less manual editing.

**OPEN QUESTION:** How can the protocol avoid hidden ghostwriting and false imitation of the
author's voice?

### F5 — Learning Closure

**ID:** F5  
**ORIGIN:** SYNTHESIS  
**SCOPE:** CORE  
**STATUS:** DISCUSS

**IDEA:** Close a learning chain with a coherent retelling, a map of the path travelled, and a
possible review plan.

**OPEN QUESTION:** Should closure happen automatically, be proposed by the model, or start only
at the human's request?


### F6 — Repository Steward

**ID:** F6  
**ORIGIN:** SYNTHESIS  
**SCOPE:** CORE  
**STATUS:** TEST

**IDEA:** Let a fresh disposable session build or refresh a compact, source-backed projection of
one repository, keep committed base state separate from a live working-tree overlay, and answer
narrow context queries for an external orchestrator. See the
[experimental candidate contract](candidates/repository-steward.md).

**OPEN QUESTION:** Can fresh sessions reconstruct approximately the same operational understanding
while keeping validation cheaper than repeated full repository inspection?
