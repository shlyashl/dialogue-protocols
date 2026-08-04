# dialogue-protocols

*Working title. A research journal, not a product. No promises, no roadmap, no marketing.*

## What this is

We kept inventing ways for a human and an LLM to think together: a "definitions" mode,
a "resonator" mode, a "lecture" mode — and kept running into the same questions. Where
does a mode break? How do you leave one? How do you agree on a way of talking without
burying the human under rules?

At some point it stopped looking like a pile of prompts and started looking like
something else:

> **What agreements let two different kinds of intelligence think together more
> effectively?**

That is not a question about ChatGPT, or even about LLMs specifically. It is a question
about the **design of joint cognition** — the temporary contracts two minds adopt so the
collaboration is better than either alone.

This repo collects those contracts, the observations behind them, and the failures — as
they actually happened, before they are lost in chat logs.

## What this is not

- Not a framework or a library you install.
- Not "prompt engineering tips."
- Not a claim that any of this is correct. Much of it will turn out empty. That is fine —
  a negative result is still a result.

## The core object: a *protocol*

A **protocol** is a short, explicit, **temporary** contract about *how* the two parties
communicate for a while — not *what* about. It says things like: what mode we're in, what
each turn should contain, how to signal "switch," how to leave, and what it costs the human.

The unit is deliberately small and disposable. You put one on like a glove, and take it off
when it stops fitting. See `protocols/_TEMPLATE.md`.

The default scope is the current conversation. A protocol does not silently become a permanent
preference, transfer to a new session, or stack with another protocol. Either party may propose
a switch; the human can always decline or say "back to default."

## Quick start

### How to use in two minutes

Ordinary conversation remains `default`. Choose a protocol only when you can name an observable
need — for example, unfamiliar concepts keep piling up, a rough intuition needs testing, or a
long explanation must work without a screen. If ordinary dialogue is working, do nothing.

1. **Share and accept the contract.** In a new conversation, paste, attach, or otherwise provide
   the full protocol in a form both parties can access, then explicitly agree to use it for the
   current conversation. A new session never inherits that agreement automatically.
2. **Then speak naturally.** The human does not need to memorize the detailed rules. Once the
   contract is available and accepted, its shorthand is a convenient reminder — not an
   installation mechanism. Without the shared contract, the same phrase is only an approximate
   natural-language request.
3. **Keep one running protocol active by default.** If the answer no longer fits it, the model
   should name the observable mismatch and may propose an exit or switch. It must not switch
   silently.
4. **Exit or switch explicitly.** Say "back to default" or name another available protocol and
   agree to the change. Returning to `default` removes the special interaction rules, not the
   subject or factual context.

Natural entry and exit examples:

| Protocol | Observable need | What a person might say |
|---|---|---|
| [`definitions`](protocols/definitions.md) | New concepts keep obscuring the current one. | "I keep losing the thread. Let's use definitions — one brick at a time. What is a query log?" |
| [`resonator`](protocols/resonator.md) | A rough intuition needs reconstruction and criticism. | "I have a rough intuition. Use resonator: reconstruct it, let me confirm it, then find the mechanism and load-test it." |
| [`lecture`](protocols/lecture.md) | A long explanation must be easy to follow by ear. | "I'm going for a walk. Use lecture: one coherent, audio-friendly explanation of attention, about 20 minutes." |
| [`default`](protocols/default.md) | The special rules no longer help. | "Back to default — just answer normally." |

No slash commands or product features are assumed, and variants of these phrases are valid.
Simply using a protocol does not require logging anything. To test one deliberately, use the
lightweight [`testing and improvement guide`](notes/testing.md).

## Shared lifecycle for running dialogue protocols

This lifecycle applies to protocols that remain active across multiple turns. One-shot handoffs
such as `chord` and procedural protocols such as `consilium` define their own entry,
completion, and exit in their files; they should not be forced into a running-mode lifecycle.

1. **Enter explicitly.** Agree on a protocol for the current stretch of work.
2. **Work under the contract.** The human remembers the shorthand; the protocol carries the
   details.
3. **Notice mismatch.** Either party can say the contract is getting in the way. The model
   should propose a switch rather than silently violate the contract or force the answer into
   the wrong shape.
4. **Exit cheaply.** "Back to default" removes the special rules, not the subject matter or the
   factual context of the conversation.

Regardless of lifecycle, every protocol names the responsibilities of both parties, its cost
to the human, and where it should fail. A protocol that claims to fit everything has not been
specified.

## Experimental protocol trace

During testing, a short trace may record protocol fit, a rule bent, an exit suggestion, and one
observable note. It is off by default. The trace describes choices visible in the answer; it
does not expose hidden reasoning or claim that a model has feelings, consciousness, or
human-like access to an inner state. See the template and
[`notes/design_questions.md`](notes/design_questions.md).

## Layout

```
protocols/   — the contracts themselves (one file each), + a template
notes/       — observations, anti-patterns, half-formed ideas
examples/    — concrete sketches / transcripts showing a protocol in use
```

Unaccepted proposals live in the [`idea incubator`](notes/incubator.md); it is a set of open
hypotheses, not a roadmap.

## Discipline of the journal

- Write things down when they happen, not later.
- Record failures and anti-patterns as first-class entries.
- Distinguish an observed failure from a suspected one; use
  [`notes/failures.md`](notes/failures.md) rather than repairing the story from memory.
- Keep entries abstract and portable — a protocol should apply to any capable model,
  independent of architecture. No secrets, no private data, no product specifics.
- Provenance matters: note where an idea came from. Intuitions are cheap to have and
  expensive to lose.

## Origin

This track split off, unplanned, from a separate ML experiment on model-internal memory.
That experiment studies mechanisms *inside* a model; this repo studies the *interface*
between a human and a model. They are kept apart on purpose — different levels, different
questions. If in a month this is empty, no harm done. If not, it stands on its own.
