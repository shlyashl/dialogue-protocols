# Testing and improving protocols

*A lightweight field guide for learning from use without turning every conversation into a
research ceremony.*

## Principle

Treat a protocol as a hypothesis about an interaction, not as proof of its own usefulness. Test
it first on a real task where its promised function matters. A polished contract or a convincing
example may show that the text is readable; neither shows that the protocol helps in practice.

Simply using a protocol does not require a test record. Capture one when there is something worth
learning, comparing, or preserving.

## Minimum before a trial

Write down only five things:

- **Protocol / version.** Use the named version, or a commit SHA or date if no version exists.
- **Task shape.** Describe the kind of work in one sentence, not the whole subject area.
- **Reason for entry.** Name the observable need that made this protocol a plausible fit.
- **One expected task outcome.** State what should be better in the work itself.
- **One interaction-cost measure.** Choose one cheap signal such as extra steering turns,
  corrections, interruptions, rewinds, or time spent.

Do not add metrics merely because they are measurable.

## Minimum record after a trial

Copy this small record and keep the evidence observable:

```text
Protocol / version:
Task:
Why entered:
Expected benefit:
Observed result:
Human steering cost: low | medium | high
Exit: clean | late | forgotten
Verdict: helped | neutral | harmed
Evidence:
Notes:
```

`Evidence` can be a short transcript excerpt, a link to a task artifact, or a concise observation
that another person could inspect. Do not include private data or hidden model reasoning. If the
primary transcript was not preserved, say so plainly.

## Classify the problem before editing

Choose one primary classification. Add a secondary one only when it changes the next action.

| Classification | What it means |
|---|---|
| **Protocol failure** | The contract was active, broadly followed, and suited to the task, but its rules failed to deliver the intended function or created a worse cost. |
| **Compliance failure** | The protocol fit and was accepted, but the human or model did not follow a relevant rule. |
| **Task mismatch** | The protocol was the wrong shape for the task, or should have been exited earlier. |
| **Ordinary answer error** | A factual, reasoning, sourcing, or execution error occurred that is not explained by the protocol. |
| **Activation failure** | The full contract was unavailable or not accepted, or shorthand was mistaken for installing the contract. |

The classification is a working diagnosis, not a verdict about blame.

## Improvement loop

**Real task → observation → failure classification → smallest revision → new version →
comparable retest.**

Make the smallest change that tests one explanation of the failure. Then try the new version on
a similar task shape and compare both the task outcome and the chosen interaction cost. A retest
need not reproduce the exact topic; it should exercise the same claimed function.

## Revision limits

- Do not rewrite a protocol after one ambiguous case.
- Fix an explicit semantic or safety defect immediately when waiting would preserve a known
  harmful ambiguity.
- Test one main change hypothesis per revision.
- Do not polish wording without an observed problem it is meant to solve.
- After a change, test a similar task shape rather than switching to an easier demonstration.
- Preserve provenance. If the primary transcript was not saved, mark that absence honestly.
- Deleting a rule is allowed and preferred when it lowers interaction cost without losing the
  protocol's function.

## Tiny outcome-and-cost examples

These are examples, not required metrics.

| Protocol | Example task outcome | Example interaction-cost measure |
|---|---|---|
| `definitions` | The human can restate the current concept or relation before the next one is introduced. | Extra turns or corrections needed to stabilize one unit. |
| `resonator` | The reconstruction is confirmed, then yields a live mechanism and test — or a clear unsupported verdict. | Confirmation and correction turns before mechanizing the idea. |
| `lecture` | The listener can follow and recap the main arc without looking at a screen. | Interruptions, rewinds, or large drift from the requested length. |

Keep the record wherever it is easiest to preserve. Add a durable failure to
[`failures.md`](failures.md) only when it is worth sharing; this guide does not require a separate
logging system.
