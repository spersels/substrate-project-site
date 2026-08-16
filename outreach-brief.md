---
layout: default
---

# The Substrate Project — Outreach Brief

*Short by design. The ask is at the end, and it is not money or endorsement.*

**Status:** v0.3 — public edition · August 2026 · Companion documents: *Root Cause: Unknown* (problem statement) and *The Substrate Project — Founding Document* (full argument; current version per the repository README)

---

## The context, in three sentences

Humanity is granting AI systems authority to act in the world — incrementally, from advising to acting-under-review to acting autonomously — and each grant is a rational product decision whose aggregate is the largest transfer of operational authority in history, conducted without an architecture of accountability. Every institution that governs action (law, liability, audit, deterrence) assumes actors that are persons — attributable, slow, jailable — and AI agents break every assumption at once, so the domain-general need is an infrastructure of **authorized action**: every consequential AI act attributable, authorized, bounded, and accountable. This project builds that infrastructure in the one arena that is simultaneously furthest along, most tractable, and the medium through which every other domain's agents act: **software — the beachhead, not the boundary.**

## The problem, in one paragraph

Machine-written code is being deployed at a rate no human review process can touch, under two default practices with compounding consequences: the *why* behind generated code (the prompt, the requirement, the tradeoff) is discarded at generation time — provenance retention is effectively zero — and a growing share of running code has never been read by any human and never will be. Systems keep working; the ability to give a true, checkable account of *why they do what they do* is disappearing. The companion problem statement names this the **Eloi Phenomenon** (after Wells: a civilization living comfortably on machinery it no longer understands, arriving by convenience rather than catastrophe), and proposes two measurements nobody currently tracks: the **dark code fraction** (deployed code with no human reader and no surviving provenance) and the **cause-unknown rate** (severe incidents closed without an established root cause). The loss with a deadline: past a certain depth of provenance-less strata, legible reconstruction of infrastructure stops being expensive and becomes impossible — an option foreclosed silently, on a schedule set by discarded context windows and retirements.

## The claim, at calibrated confidence

1. **High confidence — the part we'd bet on.** Machine agents acting *irreversibly* (moving money, sending messages, actuating things) need trust that exists before execution, composes across systems, and survives audit. Stochastic assurance categorically cannot supply it: a model's approval is testimony, not evidence — it doesn't compose, doesn't transfer, and expires on every change. Every trust chain must terminate in something deterministic — a small checker, a certificate, a reproducible re-run. *Never trust the author; trust the certificate.* This makes ever-stronger models an asset, not a threat: provers and searchers whose output is never trusted, only checked. Note the deliberate narrowness: for reversible actions, ex-post trust (rollback, observability) wins and we do not contest it. The claim binds on the irreversible frontier — which agent tooling is expanding monthly.

2. **Open empirical question — what Phase 0 exists to answer.** Whether this evidence layer works dramatically better as a purpose-built substrate (a language and semantic store designed for machine authorship) than as tooling bolted onto existing stacks. We have pre-registered hypotheses and kill criteria, below. The sequencing principle is *the schema is the invention; the language is a bet*: tooling on existing stacks ships first; the substrate must earn construction through effect sizes fixed before the experiments run. The first product is concrete — the **transponder layer**: action provenance certificates for AI agents. Every consequential act carries a verifiable credential (which agent, by model hash; on whose behalf, as a certificate chain to a human anchor; with what right; doing what), verified by *receivers* — banks, APIs, clouds refuse unattributed agent actions, the way controlled airspace refuses aircraft without transponders. The needed regulation is one sentence; C2PA proves the pattern deploys (it's doing this for AI media today); nobody has done it for actions. Requires no new language, no migration — and privacy is a design requirement, not an afterthought: zero-knowledge chain validation, so the rails verify *that* an action is tethered without learning *who* holds the tether, with identity disclosable only under due process.

3. **High confidence in the risk, low confidence in anyone's solution.** No formal method reaches *intent*. A machine-checked proof anchored to a mistranslated spec launders the mistranslation — "proven correct" is the most misleading phrase in the stack. We stratify "correct" into four layers (soundness, conformance, fidelity, fit); machine authorship makes the bottom two radically cheaper and the top two *more* dangerous. Our containment story for the top layers is honest about being unproven: visibility, not containment, until the experiments report.

## The design, in three moves

Everything in the full document unfolds from three moves applied recursively, from code to specs to requirements to mandates:

1. **Replace text + testimony with structure + checkable evidence.** The canonical artifact is a content-addressed graph of typed definitions carrying effects, capabilities, specs, evidence, and provenance; human views are verified projections. A proof checked once is checked forever — trust becomes capital, not an operating expense.
2. **Authority is a capability — held, delegated, attenuated explicitly.** At the bottom: a module cannot express a network call it wasn't handed. At the top: an AI may author requirements only under a mandate whose delegation chain terminates in a ratified human commitment — a decidable audit query.
3. **What cannot be mechanized must be recorded, attributed, and queryable.** The requirement→spec judgment, the elicitation dialogue, the ratification — none provable, all forced into the open.

## The safety reading

The same architecture, read outward, is a concrete mechanization of **"AI under human authority" as a checkable property** — a sentence the safety world says constantly and almost nobody has an architecture for. Every AI action must answer two questions, both as decidable queries rather than policy aspirations: *on whose behalf?* (a delegation chain terminating in a ratified human commitment — the "loose AI detector" is a database query whose answer must be empty) and *with what right?* (an explicitly delegated, attenuated capability). Full tethering requires four properties — **rooted, bounded, mediated, aggregately invariant** — and we record four leaks with equal prominence: persuasion (the human hand is an actuator), composition (bounded actions can compose into unbounded outcomes), the unmediated boundary, and the political ratchet toward longer leashes. Stated with the discipline the rest of this brief uses: the tether is morally neutral — it delivers *attribution, not virtue*, and does nothing against a hostile principal with a valid chain. Its unique offer in that regime is different: **proof-based security is the only kind whose guarantees don't degrade as the attacker gets smarter** — a verified property doesn't care about the adversary's IQ, which makes this one of the few levers that structurally shifts the cyber offense-defense balance toward defense. The tether is the seatbelt, not the sober driver: control and alignment are complements, and we claim only the seatbelt.

## The hypotheses (Phase 0, pre-registered, each falsifiable)

| # | Bet | Test | Status |
|---|-----|------|--------|
| H1 | Models generate better code given spec-in-context + constrained decoding | vs. Python/Rust baselines | Upside, not a gate |
| H2 | Reviewers (human or model) reach justified confidence faster when signatures carry effects and locality holds | Planted-bug detection rates and inspection cost across languages | **Core.** Cheapest; runs first |
| H3 | Blast radius of wrong/adversarial generated code is bounded by construction | Red-team vs. sandboxed-Python baseline | **Core.** Sells to agent-runtime operators today |
| H4 | Repair loops converge faster with structured errors-as-prompts | Iterations-to-green | Open |
| H5 | N agents on shared code: fewer conflicts and stalls | vs. baseline | Open |
| H6 | Requirement-traceable formal specs reduce *silent intent divergence* | Spec conforms, proof checks, behavior betrays the requirement — measured rate | Decides whether "proven correct" oversells |
| H7 | Structured, counterexample-driven elicitation beats prose requirements | Human subjects, current models; commitment records sufficient to adjudicate | Cheapest; runs first, needs no infrastructure |

Different survivors imply different projects (H3 alone → secure agent runtime; H2+H4 → verification-native platform). The venture dies only if all core bets fail — and the kill criteria are written down before the data arrives.

## What we are *not* claiming

That verification replaces testing; that formal methods reach intent; that the frontier won't erode parts of the case (every model-reliability gain shrinks deltas and accrues to incumbents first — recorded as objection #1 in our own document); that structure-as-truth hasn't lost every prior attempt (it has; we argue machine authors are the first population for which the fatal headwind doesn't blow, and we hold that argument at "plausible," not "proven"). The founding document carries a section titled *The Realist Case Against*, maintained honestly, with a standing adjudication of which objections we've conceded.

## The ask

**Read it adversarially and tell us where it's wrong.** Not endorsement, not funding, not time beyond one reading and one conversation. The document records every idea-level change with its provenance; being changed by qualified hostility is its update mechanism, and its §7 has already absorbed one full hostile pass. Specifically valuable to us, by expertise:

- **PL / formal methods:** Is the kernel-calculus bet (<~30 constructs; effects, capabilities, refinement; content-addressed store) coherent? What effect size in H2 would make *you* take the substrate seriously?
- **Object-capability / systems security:** Does "authority-to-specify as a capability" (mandates, attenuated delegation, decidable audit) survive contact with people who built the downward version?
- **Requirements engineering / HCI:** Is the H7 design (structured elicitation compiling to adjudicable commitment records vs. prose documents) runnable as stated? What would you change before a human-subjects pilot?
- **Anyone operating agents in production:** Which irreversible actions do your agents take today, and what evidence would you need to let them take more?
- **AI safety / governance:** Does "tethered intelligence" (four requirements, four leaks) hold up as a control framing, or is there a fifth leak we haven't named? Is zero-knowledge chain validation with escrowed attribution politically survivable in your jurisdiction — and if not, what is?

*Full documents on request: the problem statement (3 pp., deliberately solution-free) and the founding document (v0.6, ~18 pp., includes the case against itself and the safety reading).*

---

