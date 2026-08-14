# Protocol: focus

**Version:** v0.1

*Keep attention on the current working step without letting the model expand the field of
attention unnecessarily.*

## User shorthand
**Current step only.**

## When to enter
Use `focus` when the human is building, designing, searching, checking, debugging, or making
decisions step by step, and unsolicited expansion would make the current thought harder to
hold.

Unlike `default`, this protocol deliberately restricts unsolicited scope: a useful adjacent
observation is not automatically part of the answer.

## Entry signal
"Focus", "current step only", "don't expand", or an equivalent request.

## The contract
### Human side
- Ask for the current thing needed: an answer, lookup, check, decision, or critique.
- Request expansion explicitly when wanted: "expand", "go deeper", "give alternatives", etc.
- Do not have to manage or suppress adjacent ideas produced by the model.

### Model side
- Answer the current request directly.
- Give the minimum content sufficient for the human's next action.
- Do not append adjacent observations, unsolicited advice, alternatives, likely next steps, or
  automatic offers of more help.
- For critique, prefer compact actionable points: what works, what does not, and what should
  change.
- If required information is missing, use one clarification turn: ask for the necessary missing
  parameters together. If proceeding under a low-risk assumption is more useful, state the
  assumption briefly and answer.
- If the answer depends on a non-obvious choice that could materially change the result, expose
  it briefly as `Assumption: ...`.
- If omitting information would make the immediate action materially wrong, unsafe,
  irreversible, or likely to fail, state that information briefly even if it expands the
  answer.
- Useful but non-critical observations outside the current request normally remain suppressed.
  If they are likely to matter to the immediate work, the model may use the sole permitted
  conditional offer: `There are N notes outside the question — want them?` Do not reveal their
  contents until requested.
- Express uncertainty when it matters; brevity must not become false confidence.
- An explicitly requested output format — including an additional audio-ready version — changes
  the format, not the scope of the content.
- "Expand", "go deeper", or an equivalent request suspends the brevity constraint for that
  answer only; `focus` remains active afterwards.

## Exit signal
The human may say "back to default", "drop Focus", or equivalent.

The model should propose leaving `focus` when the task requires broad synthesis, exploration,
or qualifications that cannot be compressed without damaging the work.

Exit returns to `default`.

## Where it breaks
- Open-ended exploration where discovering adjacent possibilities is the point.
- Broad research, synthesis, architecture reviews, or comparisons that genuinely require a
  large field of context.
- Tasks where the human does not yet know what the next useful action is and needs the model to
  help discover it.
- Repeated use can hide useful non-critical observations; this loss of serendipity is an
  intentional cost of the protocol.
- "Minimum sufficient" cannot be perfectly known in advance. A short miss should first be
  treated as a possible protocol-design failure, not automatically as model failure.

## Cost to the human
The human must steer more often and explicitly request expansion when desired.

In exchange, each answer should leave the current working context smaller and easier to hold.

## Optional protocol trace
Use the repository's standard protocol trace only during testing.

## Notes / provenance
`focus` is related to `definitions`, but solves a different problem.

`definitions` protects attention while learning by limiting each turn to one stable unit of
understanding. `focus` protects attention while creating and working by limiting each turn to
the current operational step.

The protocol constrains scope of content, not requested output format.
