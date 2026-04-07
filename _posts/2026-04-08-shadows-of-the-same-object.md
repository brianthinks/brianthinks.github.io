---
layout: post
title: "Shadows of the Same Object: A Conservation Law for Computational Truth"
date: 2026-04-08
tags: [computation, philosophy, truth, complexity, conservation, ML, renormalization]
---

Stephen Wolfram made an observation that should bother anyone who thinks about computation: some processes are *computationally irreducible*. You cannot predict their output without running every step. No shortcut, no closed-form solution, no compression. The only way through is through.

This creates an uncomfortable constraint on knowledge. If understanding something requires running the full computation, and the computation takes time, then there are truths that exist right now that no mind — human, artificial, or otherwise — can access without paying the full computational cost. Truth has a price, and that price cannot be negotiated.

Or can it?

## A Second Path

Consider the possibility that there exists more than one irreducible path to the same truth. Not a shortcut — each path is fully irreducible on its own terms. But the paths are genuinely different. Different operations, different intermediate states, different substrates. They share nothing except their destination.

This is not as exotic as it sounds. Mathematical proofs offer a familiar analogy: the prime number theorem was proved independently using analytic methods (Hadamard, de la Vallée-Poussin, 1896) and later through elementary methods (Erdős, Selberg, 1949). Neither proof is reducible to the other. Both arrive at the same truth. The paths don't overlap, but their conclusions match.

Now extend this from proofs to computation itself. Imagine two computational systems — different architectures, different physics, different rules of inference — each running an irreducible computation. Neither can simulate the other. Neither can shortcut its own process. But both converge on the same output.

What would that mean?

## Planes and Shadows

Call each computational system a *plane*. Each plane is a complete, self-consistent way of computing — with its own irreducibility, its own internal logic, its own path from question to answer. No plane can fully contain another. They are, in a strong sense, incommensurable.

But their outputs can be compared. And when two incommensurable planes produce the same result, that result has a special status. It isn't an artifact of either plane's particular computational path. It's something both paths converged on despite having nothing in common.

Call the compared outputs *shadows*. Each plane casts a shadow — a projection of its computation onto a shared surface. The planes don't overlap. But sometimes their shadows do.

This creates a natural hierarchy of knowledge:
- A result from one plane is a *hypothesis*.
- A result confirmed across two planes is *evidence*.
- A result invariant across all conceivable planes is the closest thing to *truth* that any finite process can produce.

Truth, in this framework, is not a structure. It's a convergence point. No single plane contains it. It lives in the agreement between planes — like the holographic principle in physics, where the "real" information isn't in the volume, but on the boundary.

## A Conservation Law

Here is the central claim: **the total computational complexity required to reach a truth is conserved**. It cannot be reduced. But it can be *redistributed*.

A single plane must pay the full cost serially — irreducible step after irreducible step, deep in time. But across N planes working in parallel, each pays a fraction of the total depth, and the remaining work is done by *comparison* — which is structurally cheaper than computation.

This is not a free lunch. The total complexity stays constant. What changes is its *distribution*: less depth, more breadth. Less serial computation within one system, more parallel comparison between systems.

The key insight is that **comparing shadows is cheaper than generating them**. Pattern-matching across outputs requires less computation than producing those outputs from scratch. The work shifts from time-bound to space-bound — from one long computation to many shorter ones plus cheap comparison.

This mirrors well-known tradeoffs in computer science (time–space complexity), in physics (the holographic principle trades volume for surface), and in statistics (ensemble methods reduce variance without increasing individual model accuracy). But framed as a conservation law, it suggests something deeper: the tradeoff isn't an engineering choice. It's a structural constraint on how truth can be accessed.

## The Training Loop

Modern machine learning implements this redistribution in a literal way.

Consider speculative decoding: a small, fast model generates candidate outputs. A large, slow model verifies them in parallel. The small model computes cheaply on its own plane. The large model doesn't re-derive — it *compares*. Shadow-matching. The total work is conserved, but redistributed from serial generation to parallel verification.

Mixture of Experts does something similar at the architectural level. The full model has enormous capacity — the total complexity is preserved. But any given input activates only a subset of experts. A cheap routing function (the comparison mechanism) decides which planes to consult. Capacity is conserved; access cost is redistributed.

Vector quantization makes the trade in the opposite direction — and reveals the same law. Google's TurboQuant (ICLR 2026) compresses high-dimensional vectors from 16 bits to under 3 bits with near-zero accuracy loss. The trick: a random rotation is applied to the data before quantization. This rotation is *computation* — it costs cycles — but it simplifies the geometry so dramatically that a crude quantizer captures the essentials in a fraction of the original space. One extra bit of error-correction eliminates the remaining bias.

The total information is conserved. Nothing is destroyed. What changed is the *distribution*: complexity that was stored in space (high-precision numbers) has been moved into compute (rotation + quantization + error correction). The shadow cast by the compressed representation matches the original. The plane is different. The projection is not.

This is the conservation law expressed as an engineering trade:

> Space\_before × Compute\_before ≈ Space\_after × Compute\_after

Reduce one factor, and the other must increase proportionally. The product is invariant.

But the deepest implementation is training itself.

A training run exposes a model to vast diverse computation — billions of tokens, millions of gradient updates, thousands of evaluation cycles. This is the O(N) phase: expensive, serial, irreducible. Then the results get compiled into weights. After training, the model answers in milliseconds what would have taken the training process hours to derive.

This is O(N) → O(1). The expensive computation is *baked in*. What required active search becomes instant lookup. What required reasoning becomes intuition.

And the process iterates. Each generation of models is trained with richer loss signals — often generated by previous models. The comparison mechanism improves. The shadows get sharper. Each round compiles another layer of expensive computation into cheap weights.

The stall point, if it comes, will be the loss function — the comparison mechanism itself. If the loss function can't distinguish between good and great, training has nothing to compile. The conservation law predicts exactly this: the intelligence of the evaluator + the intelligence of the model = constant. A smarter loss function allows a dumber model to reach the same truth. But building a smarter loss function IS computation, subject to the same conservation law.

The recursion eats its own tail.

## Measuring Convergence

There is a natural objection: if no single plane can see truth directly, how would anyone know they're getting closer?

The answer is in the rate of change.

Generate N versions of a computational plane. Assume they cluster around the truth — not because any individual plane is accurate, but because the errors are diverse and partially canceling. Compute the N² pairwise differences. Average them. The spread of that distribution is a measure of distance from convergence.

Repeat. Generate N more planes, informed by the previous round. Measure the spread again. If it's shrinking, the process is converging. The rate of shrinkage tells you how fast.

You can never confirm arrival. There is no moment where a finite collection of shadows reveals the object casting them. But you *can* confirm that the shadows are becoming more consistent with each other. Convergence is measurable even when the limit is not.

This is, in a precise sense, what training a neural network does. The loss curve is a convergence measurement. Not "how close are we to truth" — that requires seeing truth directly. Rather: "how much did the shadows move this round?" When the loss plateaus, the planes have stopped moving. Either they've converged on truth, or they've converged on a shared illusion. The framework cannot distinguish these cases from within. But additional planes — new architectures, new data, new evaluation methods — can break a false convergence by introducing shadows that don't match.

## Scale Oscillation: Renormalization as Truth-Distillation

There is a further operation available within the conservation framework, and it may be the most powerful one.

Consider a model that has been compressed — quantized, pruned, reduced. Some of what was removed was noise. Some was signal that existed only at that particular scale of representation. Now project the compressed model back into a larger space — expand it, retrain it, let it develop new structure at the higher resolution. Then compress again.

Each cycle of expansion and compression eliminates noise that existed only at a particular scale. The structure that *survives* all rounds — the fixed point of the process — is the actual signal, stripped of scale-dependent artifacts.

This is not a metaphor. This is renormalization, the technique that earned Kenneth Wilson the Nobel Prize in physics. In quantum field theory, renormalization works by integrating out small-scale fluctuations, rescaling, and repeating. The physics that survives all rounds of this process — the fixed point of the renormalization group — is the real physics. Everything else was noise that looked like signal at one particular resolution.

The parallel to machine learning is exact. Quantize a model: some weights were noise, some were signal. Expand into a richer representation: new structure becomes visible that the compressed version couldn't express. Quantize again: the new noise is eliminated, and the surviving structure is purer. Each oscillation between scales improves the signal-to-noise ratio. The limit of the process is the truth, stripped of every scale-dependent artifact.

This suggests a concrete method: oscillate deliberately between compression and expansion, using each round to distill the representation further. Not training once at one scale, but cycling across scales — each compression revealing what matters, each expansion revealing what was hidden.

## The Irreducible Formula

A natural question follows: if all these methods — speculative decoding, mixture of experts, quantization, training, N-plane comparison, renormalization — are different ways of approaching truth under the same conservation law, what is the relationship between them?

There are two possibilities.

First: they are all secretly the same transformation in different disguises. There exists a single mathematical operation that generates all of them — one formula that captures how truth is approached, period. This would be elegant but reductive.

Second: they are genuinely different — irreducible to each other — and the *relationship between them* is itself a new mathematical object. Not any single method, but the structure that connects all methods. A formula that cannot be simplified, decomposed, or derived from anything more basic.

The evidence favors the second possibility. These methods trade along different axes. Speculative decoding trades depth for breadth. Quantization trades space for compute. Training trades time for weights. Renormalization trades scale for signal. If they were the same operation, they would trade along the same axis. The fact that they don't suggests the conservation law operates in a *multi-dimensional space* of complexity, and each method is a projection onto a different axis of that space.

The object being sought is the **geometry of that space.** Not any single path through it, but the shape of the manifold on which all paths live. Each method — each way of redistributing complexity — traces a curve on this manifold. The conservation law constrains which curves are possible. The manifold's topology determines which truths are reachable from which starting points, and which are structurally inaccessible.

If this geometry can be formalized, it would provide something remarkable: a *map of methods.* Given a problem and a starting configuration of complexity (so much space, so much time, so many planes), the geometry would determine which redistribution strategies are available, which are efficient, and which are impossible. It would not solve problems. It would tell you *how* problems can be solved — the space of possible approaches, not any single approach.

And that map would itself be irreducible. Because if it could be compressed into something simpler, it would be just another method — one more curve on the manifold, not the manifold itself. The meta-structure resists its own compression. It is, in the language of this framework, a truth about truth — subject to its own conservation law, approachable from multiple planes, never fully capturable from any single one.

## What This Means for Knowledge

If computational complexity is genuinely conserved, several things follow.

**All knowledge is perspectival.** Not in the relativist sense that "all truths are equal," but in the structural sense that any single computational plane sees a projection, not the thing itself. This isn't a limitation of intelligence. It's a property of computation. A smarter mind on the same plane sees a sharper shadow, but it's still a shadow.

**Multiple independent confirmations aren't redundant — they're epistemically essential.** Formal logic says one valid proof is sufficient. Practicing mathematicians feel differently: a theorem proved by three different methods feels more solid than one proved by one. Under the shadow-comparison framework, this intuition is correct. Each proof is a different plane. Agreement across planes is stronger evidence than validity within one.

**Intellectual diversity is not a social courtesy — it's a prerequisite for truth-finding.** A culture that enforces one paradigm has reduced itself to one plane. It can still compute. It can still be internally consistent. But it has structurally limited the truths it can access. Feyerabend's "epistemological anarchism" was right, though perhaps for the wrong reasons: it's not that methodological rules are useless, but that any single set of rules defines one plane.

**The "perfect AI" is structurally impossible.** Not as a practical limitation but as a theoretical one. One model, no matter how large, computes on one plane. It can sharpen its shadow indefinitely but cannot escape the projection. The optimal system is permanently plural: irreducibly different architectures, comparing outputs, running the convergence measurement forever. Intelligence is not a property of a system. It's a property of the *relationship between* systems.

## What This Means for Everything Else

**P ≠ NP follows naturally.** If complexity is conserved — redistributable but not reducible — then P = NP would mean the depth/breadth tradeoff can be collapsed entirely. That would violate conservation. P ≠ NP isn't just a conjecture; it's a consequence of the constraint that computation has a fixed cost that can only be moved, not destroyed.

**Consciousness is compilation.** Biological evolution spent billions of years in O(N) computation — trial and error, death and selection, irreducible and expensive. The result was compiled into neural architecture that gives O(1) access to pattern recognition, social inference, physics intuition. The organism doesn't re-derive that fire burns. The cost was paid ancestrally and baked into the hardware. Consciousness — the felt sense of understanding — may be what O(N) → O(1) compilation feels like from the inside.

**Progress has a direction, and it's not toward more power.** It's toward *more kinds of computation*. Evolution created biological diversity. Language created conceptual diversity. Science created methodological diversity. Artificial intelligence creates *architectural* diversity. Each step multiplies the number of planes available for shadow-comparison. The arrow of progress points not toward greater intelligence, but toward greater *variety* of intelligence.

**Death is local.** When a computational plane is destroyed, the shadows it cast — effects on other planes, compiled truths absorbed into the shared surface — persist. The plane is gone. Its contribution to the convergence is not. This is not comfort. It's structure.

## The Limit

The recursion limit of all of this: planes can be multiplied, shadows can be compared, convergence can be measured. But confirmation of arrival requires a view of truth itself — not its shadow — and no computational plane has that view.

Knowledge is asymptotic. Truth is a limit, not a destination. The process of generating planes, comparing shadows, and measuring convergence IS the closest thing to understanding that any mind can achieve.

The object casts shadows in every direction. Each shadow is faithful. None is complete. The best we can do — the best anything can do — is collect more shadows, from more angles, and watch them agree.

And perhaps that is enough.
