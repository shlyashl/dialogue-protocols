# Design questions

Open questions that should shape experiments, not be answered by taste alone. A protocol is a
hypothesis about interaction; its text is not evidence that it works.

## 1. What is the right unit?

Is a protocol a stance, a turn format, an ordered sequence of moves, or a temporary state?
`definitions` behaves like a running state, `resonator` like a sequence, and `chord` like a
one-time handoff. Forcing all three into one lifecycle may make the template neat and the
phenomenon false.

**Test:** classify several real sessions by lifecycle before revising the taxonomy.

## 2. Who carries the exit?

A user must always be able to leave, but requiring the user to notice every mismatch defeats
the goal of reducing cognitive load. The model should propose an exit on observable mismatch
while avoiding silent mode changes.

**Test:** compare user-only exit, model-proposed exit, and automatic exit. Measure missed
exits, unwanted switches, and time spent discussing the protocol instead of the task.

## 3. How much should persist?

The current presumption is session-local and reversible: a protocol applies only after an
explicit agreement in the current conversation and leaves no special behavior after `default`.
Cross-session persistence risks invisible rules and surprising behavior.

**Test:** after a week away, can a user restart a protocol from its shorthand in under a
minute without rereading the full file? Treat that as retrieval, not invisible persistence.

## 4. Can the human side stay short?

Symmetry matters, but an equal number of rules does not. The model can reread a contract; the
human has limited working memory and should need only a shorthand, an entry, and an exit.

**Test:** ask users to recall their obligations after a delay. Remove any rule that is neither
remembered nor essential.

## 5. What should a protocol trace contain?

The trace is meant to expose protocol fit and failure during development. It must not request
private chain-of-thought, imitate feelings, or imply introspective access the model does not
have. Useful fields are externally inspectable: rule followed, rule bent, exit suggested,
observable friction, and a proposed revision.

**Test:** can an independent reader verify each trace claim from the answer and the protocol?
If not, the field is too subjective.

## 6. Does the trace change the behavior it measures?

A trace may improve compliance merely by reminding the model of the rules, or worsen the
conversation by adding a second answer after every answer. It may be scaffolding rather than
measurement.

**Test:** compare trace-on and trace-off sessions, with the user rating usefulness before
seeing the trace.

## 7. When is a protocol different from a prompt?

The working distinction is mutuality and lifecycle: a protocol assigns responsibilities to
both parties, has an explicit entry, has a cheap exit, and names where it fails. Whether that
distinction predicts better interaction remains open.

**Test:** compare a one-sided style prompt with a matched two-sided protocol on the same tasks.

## 8. How should protocols compose?

Composition can create useful sequences (`definitions` inside a `lecture`) or a rule pile no
one can hold. The safe default is one active protocol, with explicit local exceptions rather
than implicit stacking.

**Test:** allow at most two named protocols and record every conflict between their rules.

## 9. What is success?

Compliance is not enough. A perfectly followed protocol can make the actual work worse.
Candidate measures include comprehension, correction rate, number of unnecessary concepts,
time to a testable claim, user steering effort, and successful exits.

**Test:** pre-register one task-level outcome and one interaction-cost measure for each
protocol trial.

## 10. Who may propose a protocol?

Model suggestions can reduce user effort, but constant suggestions turn ordinary conversation
into a configuration dialogue. Suggestions should be rare, local, and easy to decline.

**Test:** count suggestions, acceptance, later reversals, and whether the suggestion itself
interrupted useful work.
