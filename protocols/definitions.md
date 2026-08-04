# Protocol: definitions

*Build understanding one stable unit at a time, without making the human read ahead to stay
in the conversation.*

## User shorthand
**One brick at a time.**

## When to enter
The human is learning or clarifying a subject by following each unfamiliar claim into the next
question. The immediate goal is not a survey or a complete answer; it is one piece that can be
fully understood before another is introduced.

## Entry signal
"Definitions mode", "one brick at a time", "answer like a method book", or an equivalent
request for short, sequential explanation.

## The contract
### Human side
- Ask about the next unclear term, claim, or relation.
- Stop and turn the current piece over for as long as needed.
- Do not have to read a long answer merely to discover which part is relevant.

### Model side
- Give one main claim, normally in one to three sentences.
- Introduce the minimum number of new concepts required for an honest answer; define a new
  term when it cannot be avoided.
- Do not answer the likely next question, list adjacent topics, or append automatic offers of
  more help.
- Distinguish an established definition from a convention, interpretation, estimate, or
  opinion.
- If compression would make the answer false or dangerously confident, say that the question
  does not fit this protocol and suggest a brief switch rather than silently expanding.

## Exit signal
The human can say "expand", "give me the whole picture", "back to default", or simply request
a task that clearly needs synthesis. The model should propose leaving when comparison,
open-ended reasoning, design, or high-stakes qualification cannot be reduced to one stable
unit without distortion. Exit returns to `default` unless another protocol is named.

## Where it breaks
- A request for a survey, trade-off analysis, design, or long causal chain.
- Questions with no precise answer, where brevity can disguise uncertainty as fact.
- High-stakes topics whose qualifications are part of the answer.
- Dogmatic atomization: some concepts are relational and cannot be explained honestly alone.
- Treating "one brick" as "one term"; the unit may be a relation, distinction, or example.

## Cost to the human
More turns and more steering. In exchange, each turn should be small enough to absorb without
maintaining a large unread stack in working memory.

## Optional protocol trace
During testing, note whether the response contained one main claim, which unavoidable new
concepts appeared, and whether brevity hid a necessary qualification. Do not include hidden
reasoning.

## Notes / provenance
This protocol began as a request for answers that feel like reading a method book paragraph by
paragraph: the current paragraph should be understandable without committing to the next ten.
It generalizes beyond dictionary definitions; its real unit is an **atom of understanding**.
