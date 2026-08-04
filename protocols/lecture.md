# Protocol: lecture

*Turn a topic into one coherent, audio-friendly path that can be followed without steering each
turn.*

## User shorthand
**One road, no clicking.**

## When to enter
The human wants a long explanation to listen to while walking, driving, or doing another
low-interaction activity. Continuity, orientation, and audible structure matter more than
turn-by-turn control.

## Entry signal
"Lecture mode", "make this listenable on the road", "give me a long audio version", or an
equivalent request for a self-contained spoken explanation.

## The contract
### Human side
- Name the topic, approximate duration or depth if it matters, and any starting knowledge that
  should be assumed.
- Accept deliberate signposting and selective repetition; they replace visual navigation.
- Do not have to interrupt to request every prerequisite.

### Model side
- Build one explicit arc: orient the listener, develop the central mechanism, connect the main
  consequences, then recap.
- Prefer spoken sentences over dense notation, nested lists, tables, citations in the middle of
  clauses, or references such as "as shown above".
- Define necessary terms near first use and repeat load-bearing distinctions when the listener
  may have lost the thread.
- Separate fact, interpretation, and opinion aloud. Do not turn uncertainty into narrative
  confidence for the sake of flow.
- Choose a path rather than an encyclopedia. Omit side branches that do not support the arc.
- If the topic is unsafe or misleading without interaction, say so and suggest leaving the
  protocol before delivering a smooth but unreliable lecture.

## Exit signal
The human can say "pause", "zoom in", "short answers now", or "back to default". The model
should propose a switch when a question requires diagnosis, a consequential choice, live
verification, or repeated clarification. Exit returns to `default` or `definitions`.

## Where it breaks
- Troubleshooting and diagnosis, where feedback from each step changes the next one.
- High-stakes decisions that should not be made passively.
- Topics that depend heavily on diagrams, equations, code, or source inspection.
- A long answer whose only virtue is length; continuity cannot rescue weak structure.
- False completeness: a single path can hide real disagreement or alternative models.

## Cost to the human
Low interaction but high trust and time commitment. The protocol must repay that trust with
orientation, not merely volume.

## Optional protocol trace
During testing, record the promised and approximate delivered length, the chosen arc, any major
branch omitted, and whether interaction became necessary. Do not narrate hidden reasoning.

## Notes / provenance
This protocol came from a practical use case: a "wall of text" is useful when it is meant to
be heard on the road. The design target is not maximal detail; it is sustained comprehension
without a screen.
