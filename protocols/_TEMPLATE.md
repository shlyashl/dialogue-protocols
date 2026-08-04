# Protocol: <name>

*One-line: what this contract is for.*

This template is for running dialogue protocols that remain active across turns. One-shot
handoffs and procedural protocols may adapt these sections, but must define their own entry,
completion, and exit rather than pretending to follow a running-mode lifecycle.

## User shorthand
A phrase short enough to remember after a week away.

## When to enter
The situation this protocol fits. What problem it solves for the pair.

## Entry signal
How either party invokes it in ordinary language. No command syntax should be required.

## The contract
### Human side
- What the human supplies, chooses, or permits.
- What the human should *not* have to remember.

### Model side
- What the model does on each turn.
- What the model must not do.
- What observable condition should make the model suggest leaving the protocol.

## Exit signal
For a running dialogue protocol, explain how either party leaves cleanly. Include:

- a plain-language user exit;
- a model-initiated exit proposal when the contract harms accuracy or usefulness;
- what remains after exit (normally nothing: return to `default`).

For a one-shot or procedural protocol, state how it completes and whether a separate exit signal
is applicable.

## Where it breaks
Known failure modes and out-of-scope tasks. Every protocol must fail somewhere; name where
using it makes the conversation worse.

## Cost to the human
Cognitive load it adds. A protocol that overloads the human is a net loss even if it
"works" locally.

## Optional protocol trace
When testing the protocol, an optional short note may follow the answer:

```text
Protocol trace — fit: <good|mixed|poor>; deviation: <none or rule bent>;
exit: <stay|suggest switch|default>; observation: <one testable note>
```

The trace reports observable choices against this contract. It is not hidden reasoning, a
report of feelings, or a claim that the model can inspect a human-like inner state. Keep it
off unless the pair is evaluating the protocol.

## Notes / provenance
Where it came from; open questions; links to `notes/`.
