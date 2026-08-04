# Observations & anti-patterns

Running log. Newest at top. Each entry: a thing noticed, ideally with the situation that
produced it. Anti-patterns are first-class — knowing what breaks is half the map.

---

## Observations

- **A protocol you can't exit is a cage.** Every mode needs a cheap, explicit exit signal.
  Modes that only enter accumulate into a rulebook the human can no longer hold.
- **Sequence beats mode.** The value of `resonator` is not resonance; it's *resonate then
  frisk*. Several protocols are really an ordered pair of moves, and naming only one half
  loses the point.
- **Stance may be shared, not transferred.** When a stance "carries" to a fresh session that
  never read the stance document, you can't tell whether it transferred or was already common.
  The second is not the weaker finding.
- **The implementer stopping itself is the load-bearing behavior.** In the `consilium`
  protocol, the moments that saved the most were the implementer *refusing to self-authorize*
  a fix it made after a failure — and returning the question instead.
- **Pre-registration is what makes "inconclusive" honest.** If criteria are fixed before
  results, an ugly result can't be re-read into a pass. Without it, every failure finds a story.

## Anti-patterns

- **Rule overload.** Piling protocols on the human until the meta-conversation costs more than
  the work. Protocols must be few, small, and disposable.
- **Flattery masquerading as resonance.** Agreement is not amplification. If the model only
  echoes, it's adding nothing and it feels like help.
- **Beautiful-but-unfalsifiable.** Ideas that resonate perfectly and can never be wrong. The
  fix is a control/placebo arm, not more discussion.
- **Echo reviewer.** Merging the adversarial reviewer into the implementer's context. Now it
  agrees instead of catching. Independence is the whole value.
- **Moving the goalposts after a failure.** Changing what a check measures because it failed.
  Sometimes legitimate (a measurement bug), but exactly where self-deception lives — so it
  should be escalated, never self-approved.

## Open questions

- Can "holds the bar" (stays honest, refuses overclaim, resists flattery) be turned into a
  blind-ratable metric? Without it, `chord` and stance-transfer stay anecdotes.
- Is there a minimal *set* of protocols that covers most collaboration, or is the space open?
- What does "exit" look like when neither party remembers they're in a mode?
