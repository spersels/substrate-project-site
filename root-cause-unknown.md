---
layout: default
---

# Root Cause: Unknown

*A problem statement: the Eloi Phenomenon*

**Status:** v0.4 — public edition
**Date:** August 2026 · *The working repository retains full provenance and document history.*

---

## 1. The string in the archive

Every serious engineering organization keeps a record of its failures. Somewhere in that archive — more often each year — is a postmortem that ends with a particular string:

> **Root cause: unknown.** Service restored from backup. Monitoring added.

Each instance is defensible. The system recovered; the archaeology wasn't worth the engineer-weeks; there was other work. No single "cause unknown" is a scandal.

In 1895, H. G. Wells gave a name to a people who lived comfortably among machinery they no longer understood — fed, sheltered, and tended by processes they had lost the capacity to inspect. He called them the **Eloi**, and he was explicit about the mechanism: not catastrophe, but comfort. This document argues that the rising rate of *root cause: unknown* is the earliest measurable symptom of the same condition taking hold between our civilization and its software — the **Eloi Phenomenon**: the progressive, comfortable, compounding loss of the capacity to understand our own operational infrastructure. In plain speech: the systems still work; *the why is disappearing.* And the timing compounds it: the why is draining out of software at the precise moment civilization is granting software-borne AI agents ever-broader authority to act in the world — comprehension leaving the exact layer that authority is pouring into.

The condition has a mechanism (two clocks — §2), a precise account of what is being lost (§3), a measurable trajectory (§5–6), and a deadline that will pass silently if it passes at all. This document names the mechanism, proposes the measurements, and registers the predictions that would prove it wrong.

It deliberately proposes no remedy. A remedy argued before the problem is measured inherits the credibility of the measurement — which today is zero, because nobody is measuring.

## 2. The mechanism: two clocks

Software has always contained more than its text. Behind every deployed system stands a chain of *why*: the requirement someone had, the tradeoffs someone weighed, the edge cases someone decided were intended. Call this the system's **provenance**. For seventy years, provenance lived mostly in people — imperfectly, but durably enough that a determined organization could usually reconstruct why its own systems did what they did.

Two clocks are now running against that arrangement. Neither runs backward.

**Clock one: provenance decay.** When a machine writes code — as it now does for a large and rapidly growing share of all new code — the *why* exists briefly and in one place: the prompt, the conversation, the requirement in someone's head, the context window of a model. Then it is discarded. Not maliciously, and not by anyone's decision — by *default*. The conversation is not retained; the context window is garbage-collected; the human who asked moves on. The code persists indefinitely. Its justification had a lifespan of minutes.

This is new. Human authors were lossy recorders of intent, but they were *recorders*: they could be asked, they wrote design docs, they remembered. Machine generation at current defaults produces artifacts whose provenance is destroyed at the moment of creation, at industrial scale, everywhere at once. The retention rate of the why-chain for machine-written code is approximately zero — and *documentably* zero, which Section 5 returns to.

**Clock two: the last reader.** For every deployed system there is a set of living humans who have actually read it — not skimmed the diff, read it. That set only shrinks. People change jobs, retire, die; meanwhile the code they read is wrapped, extended, and depended upon rather than re-read. For every system there is therefore a date — call it the **last-reader date** — after which no living person has ever read the code that is running. Nothing announces this date. Nothing changes when it passes. It is already in the past for a meaningful fraction of the world's critical infrastructure, and machine authorship advances it categorically: most machine-written code has a last-reader date *before deployment*, because no human read it at all.

The two clocks compound through a third, older dynamic: **software accretes and is never removed.** COBOL from the 1970s still clears payments; every processor still boots pretending it is 1978. Wrapping a system is always cheaper than rewriting it, because rewriting requires understanding that wrapping does not. So each generation of code becomes the unexamined foundation of the next. Machine authorship accelerates the laying of strata by orders of magnitude while — clock one — stripping each stratum of its provenance and — clock two — ensuring no reader ever existed. And the clocks run on the toolchain layer too: the interpreters, compilers, and standard libraries that all other code runs *through* require continuous human maintenance whose pipeline is collapsing — the most load-bearing code in civilization is approaching its own last-reader dates.

## 3. What exactly is lost

Not function. This must be stated plainly, because it is what every skeptic will correctly observe: **the systems keep running.** Machine comprehension scales alongside machine generation; failures get patched; the economy hums. Nothing in this document predicts collapse. The prediction is worse-shaped than collapse, because collapse gets noticed.

What is lost is the **why** — specifically, two capacities:

1. **The capacity for a true account.** When infrastructure does something consequential and wrong, the question "why did it do that, who decided it should, and was that what anyone meant?" has an answer only if a chain survives from intent to behavior. When it doesn't, the only available accounts come from systems of the same kind that wrote the code — accounts that cannot be independently checked and that share the blind spots of what they are explaining. An account that cannot be checked is testimony, not evidence. Incident response in such a world ends at *restored, cause unknown* — not occasionally, but structurally.

2. **The capacity for legible reconstruction.** A system can only be rewritten by someone who knows which of its behaviors are intended and which are accidents the world has since come to depend on. That knowledge is exactly what the two clocks destroy. Past a certain depth of provenance-less strata and a certain number of passed last-reader dates, rewriting stops being expensive and becomes *impossible* — not "hard," impossible, the way deciphering Linear A is impossible: the script survives complete, and no key and no living tradition survives with it. Linear B was deciphered because a bridge to living knowledge existed. Linear A never will be. The difference was not effort. It was whether the chain was still attached when someone finally pulled on it.

The second loss is the one with a deadline. It is the disappearance of an *option* — and options disappear silently, because nothing happens on the day they die. Civilizational infrastructure whose behavior is its only remaining specification cannot be re-derived, only imitated, wrapped, and propitiated. Every year of current defaults converts some further tranche of the world's operational logic from *not yet reconstructed* to *unreconstructable*.

## 4. Why nobody is acting on it

This problem belongs to a class that is structurally hostile to institutional attention. It is worth being explicit about the four properties, because they predict — correctly — that no existing process will surface it:

- **The loss is counterfactual.** No dashboard turns red when a possibility is extinguished. Options have no constituency.
- **Every local decision is rational.** Each team that ships unread code or discards a context window is choosing correctly *for that quarter*. The pathology exists only in aggregate, over decades. There is no villain and nothing to prosecute.
- **The evidence arrives after the deadline.** Proof that the reconstruction option mattered arrives at the moment it is needed and gone. Until then, every uneventful year reads as evidence against the problem.
- **The skeptic is locally correct.** Rollback, monitoring, and machine comprehension really do keep things running. The dispute is not about the present, where the skeptic wins, but about what compounds beneath it.

Problems with these properties — atmospheric carbon before 1958, antibiotic resistance, orbital debris — historically became actionable in only one way: **someone started measuring, and published the curve.**

## 5. The measurements

Two quantities, both definable, both cheaply measurable today, neither currently tracked or published by anyone:

**The dark code fraction.** *Dark code* is deployed code that no human has read and for which no provenance survives — no requirement, no reviewed design, no retained generating conversation. (The term is used as astronomers use *dark matter*: not sinister, simply unilluminated — the mass is there, inferred by its effects, invisible to inspection.) The dark code fraction of an organization is measurable by sampling: take N deployed components, attempt to produce a human reader or a surviving why-chain for each, publish the ratio. The measurement is a few weeks of work. The trend line, maintained annually, is this problem's equivalent of the Keeling curve.

**The cause-unknown rate.** Of severe incidents (any consistent severity threshold), what fraction of postmortems close without an established root cause — and how is that fraction moving? Every large operator already has this data in its incident archive. Nobody computes it. It is the most honest available proxy for the question *can this organization still explain its own systems?* A companion measure: **mean time to understanding** — not time-to-restore, which is optimized everywhere, but time from incident to a true causal account, which is optimized nowhere and quietly rising.

A third number needs no time series because its current value is the finding: **the provenance retention rate for machine-generated code** — of the code generated this month that will still be running in five years, what fraction retains a recoverable link to the intent that produced it? The defensible estimate today is a number indistinguishable from zero. That a civilization is laying down its infrastructure's next stratum at a provenance retention rate of zero is a single-sentence fact that ought to be checked, and can be.

## 6. The trajectory, registered

For this to be a claim rather than a mood, it must say what the world looks like if it is right and what falsifies it. Registered here, against roughly a five-year horizon:

**If this document is right:** the cause-unknown rate for severe incidents, measured consistently at any large operator, rises materially by 2031. The dark code fraction of new deployments passes one-half well before then and does not reverse. At least one major incident occurs at a systemically important institution whose root cause is publicly never established — and this is *accepted*, without significant institutional consequence, as normal. Correlated-failure events — one authored flaw manifesting across thousands of independent deployments simultaneously — recur and are treated as weather. And a marker for the readability trajectory: the first widely adopted agent-to-agent interchange format carries **no human-readability requirement in its specification** — machine-native by default, legibility not among its design inputs. This one is checkable within a few years of this writing.

**What would falsify it:** cause-unknown rates flat or falling under honest measurement. Provenance retention rising materially *absent regulation* — that is, the market pricing the why-chain on its own. Mean time to understanding holding steady as stack depth grows, demonstrating that machine comprehension converts to *checkable* accounts rather than testimony. Any one of these would mean the mechanism of Section 2 is being outrun, and this document should then say so in a subsequent version rather than retreating to a longer horizon. So would a major agent-interchange standard adopting a binding human-readability or verified-projection requirement absent regulatory compulsion — the market pricing legibility on its own.

What would *not* falsify it: another year in which nothing bad happens. Section 4 explains why that is the predicted texture of the problem, not evidence against it — an unfalsifiable-sounding move that is precisely why Section 5 exists. The measurements, not the vibes, carry the claim.

## 7. The name, earned

Section 1 took Wells's name on credit; the intervening sections are the collateral. Two features of his 1895 account — both easy to miss — are why the name fits this condition better than any technical coinage could.

First, **the mechanism**. The Eloi were not ruined by disaster; they were ruined by *effortlessness* — generations of comfort removing, one by one, every pressure to understand, until the capacity itself atrophied from disuse. That is Section 2 exactly: provenance is discarded because retaining it takes effort nothing demands; last-reader dates pass because nothing requires a reader. Every step of the decline is a convenience, taken rationally.

Second, **the texture**. The machinery in Wells's garden kept running. The Eloi were not miserable — they were happy, and the happiness was load-bearing: every year of the decline felt like improvement. That is Section 4 exactly: the skeptic is locally correct, the water is warm, and each uneventful year reads as evidence that nothing is wrong.

And in Wells's story, the machinery was tended — by someone else, out of sight, on terms the Eloi had lost the ability to examine. This document makes no prediction about who tends ours. It observes something narrower and, on reflection, sufficient: **we are losing the ability to ask.**

## 8. The ask

One thing only: **measure it.** Compute a cause-unknown rate from an incident archive. Sample a dark code fraction from a deployment inventory. Check the provenance retention rate of this month's generated code. Publish the numbers, whatever they are — this document's claims are hostage to them, by design.

Everything else — whether anything should be done, what, and by whom — is downstream of the curve, and is deliberately absent from this document. Remedies divide people; measurements recruit them. The Keeling curve did not argue. It accumulated.

---

