# Failure log

Failures are evidence, not embarrassment. Record a failure when a protocol changes the
conversation in a way that makes the underlying task worse, increases the human's burden, or
creates false confidence.

Do not turn every disliked answer into a protocol failure. First ask whether the contract was
active, whether it was followed, and whether the problem came from the contract or from the
answer.

## Entry template

```markdown
### F-XXX — Short name

- **Status:** observed | suspected | reproduced | resolved
- **Protocol / version:**
- **Task shape:**
- **Expected:**
- **Observed:**
- **Cost:**
- **Likely cause:**
- **Proposed change or test:**
- **Evidence:** abstract transcript, example, or link
```

## Seed failures

These entries come from the conversation that produced the repository. They are compressed to
the interaction pattern; no private subject matter is required to understand them. The exact
source transcript for F-001 through F-003 is not preserved in this repository, so their
evidence notes identify them as reconstructions. F-004 and F-005 remain prospective risks with
no observed evidence.

### F-001 — Definitions became an essay about definitions

- **Status:** observed
- **Protocol / version:** early `definitions`
- **Task shape:** the human asked for one small explanation.
- **Expected:** one claim that could be understood before the next question.
- **Observed:** the answer supplied the claim, then variants, caveats, future branches, and a
  summary. It was accurate but recreated the reading burden the protocol was meant to remove.
- **Cost:** the human had to finish the answer to remain present in the dialogue.
- **Likely cause:** optimizing for completeness and anticipated usefulness instead of the
  current unit of understanding.
- **Proposed change or test:** count main claims and newly introduced concepts; omit unasked
  branches; compare comprehension and steering effort.
- **Evidence:** reconstructed from the source conversation that produced this repository; the
  exact transcript is not preserved here.

### F-002 — Pseudocommands looked like product features

- **Status:** observed
- **Protocol / version:** early mode sketches
- **Task shape:** explaining how a user would enter and leave a mode.
- **Expected:** a realistic user journey using ordinary conversation.
- **Observed:** slash commands and a mode panel were described as examples but could be read as
  capabilities that already existed.
- **Cost:** the user had to ask whether the commands were real.
- **Likely cause:** a design metaphor was not labelled as hypothetical.
- **Proposed change or test:** use plain-language entry signals in protocol files; label UI
  proposals as proposals.
- **Evidence:** reconstructed from the source conversation that produced this repository; the
  exact transcript is not preserved here.

### F-003 — The exit depended on the human remembering it

- **Status:** observed
- **Protocol / version:** early `resonator`
- **Task shape:** reconstructing and amplifying a raw intuition.
- **Expected:** preserve the intuition long enough to find its mechanism, then test it.
- **Observed:** critique occurred only if the human remembered to call a second phase.
- **Cost:** an attractive but unsupported idea could leave the conversation sounding vetted.
- **Likely cause:** the contract assigned the model resonance and the human epistemic braking.
- **Proposed change or test:** make reconstruction and load-testing one visible sequence; let
  either party interrupt or exit.
- **Evidence:** reconstructed from the source conversation that produced this repository; the
  exact transcript is not preserved here.

### F-004 — Protocol evaluation drifts into pseudo-introspection

- **Status:** suspected
- **Protocol / version:** optional protocol trace
- **Task shape:** asking the model how a protocol affected its "state" or how it "felt".
- **Expected:** usable evidence about fit, deviations, and friction.
- **Observed:** not yet reproduced; the risk is a fluent first-person story that cannot be
  checked against the interaction.
- **Cost:** false authority and confusion between behavioral reporting and self-awareness.
- **Likely cause:** fields framed around inner experience rather than observable contract
  choices.
- **Proposed change or test:** require every trace claim to be verifiable from the response and
  protocol; prohibit claims about feelings, consciousness, or hidden reasoning.
- **Evidence:** none observed; this is a prospective risk, not a recorded failure.

### F-005 — The protocol discussion displaced the work

- **Status:** suspected
- **Protocol / version:** protocol layer as a whole
- **Task shape:** ordinary questions with a low cost of misunderstanding.
- **Expected:** the protocol lowers coordination cost.
- **Observed:** not yet reproduced systematically; the warning sign is more turns spent
  choosing and editing modes than answering the original question.
- **Cost:** meta-work consumes the attention it was designed to protect.
- **Likely cause:** too many modes, unsolicited suggestions, or an always-on trace.
- **Proposed change or test:** track protocol-negotiation turns and compare them with prevented
  rework; prefer `default` when the benefit is unclear.
- **Evidence:** none observed systematically; this is a prospective warning sign, not a recorded
  failure.
