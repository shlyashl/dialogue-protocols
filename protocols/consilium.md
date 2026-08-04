# Protocol: consilium

*Split a hard decision across several roles so no single voice can rationalize.*

## When to enter
A decision is high-stakes, easy to fool yourself on, and tempting to rush — the classic case
where one mind (human or model) quietly talks itself into the convenient answer. You want
structural friction, not more willpower.

## Entry signal
Naming distinct roles and a single written decision log everyone shares.

## The contract
Assign separate roles, each with a narrow remit, and route decisions through them in a fixed
order. A working set that emerged in practice:

- **Designer / architect** — proposes the plan and the exact criteria, up front.
- **Auditor** — rules on the plan and the results against *pre-registered* criteria; can say
  "inconclusive"; refuses beautiful results with regret, not indifference.
- **Implementer** — builds and runs exactly what was frozen; when it hits an underspecified
  or sensitive choice, it **stops and escalates instead of improvising**.
- **Adversarial reviewer** — an independent, cold read of the artifact whose only job is to
  find the flaw before it runs. Kept context-isolated on purpose: its value is *not* being an
  echo of the implementer.
- **Courier / owner** — carries messages between roles, decides "why" and "when to stop,"
  and reconciles the rest when they disagree.

Two rules make it work:
1. **Pre-registration.** Criteria and numbers are frozen *before* seeing results, so a
   failure can't be re-read into a pass.
2. **Escalation over improvisation.** The implementer never silently resolves a choice that
   belongs to design or that it made after a failure. It returns the question.

## Exit signal
The decision is logged with the role and date of each verdict. The log — not the chat — is
the source of truth.

## Where it breaks
- Role capture: if the same voice plays two roles, the friction is theater. Real independence
  (separate sessions / separate models) is what catches things.
- Ceremony without stakes: on a low-stakes call, the overhead isn't worth it.
- The adversarial reviewer being merged into the implementer's context — then it stops
  catching things and starts agreeing.

## Cost to the human
High coordination cost (the courier does real work). Justified only when being wrong is
expensive and the temptation to self-approve is high.

## Notes / provenance
The single most useful move is the implementer *stopping itself* exactly where
self-authorization is forbidden — after a failure, or on a choice that isn't its to make.
Every such stop is an escalation, and escalations beat improvisations.
