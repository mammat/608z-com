---
title: "Recursive Self-Improvement: A Research Overview"
date: 2026-10-02
---

## Where the field stands

Fragments of the self-improvement loop are industrial practice; the closed loop is not. The search term is **recursive self-improvement (RSI)**, sometimes "seed AI" or "self-referential learning".

The best entry point is a July 2026 survey of 1,250 arXiv papers from 2024–2026, which organises the literature by what the system improves (its deployment behaviour, its policy through training, its evaluator, or the research process itself) and by how closed the loop is. Its central distinction is worth adopting ([Chen, Wang & Qu 2026](https://arxiv.org/abs/2607.07663)).

| Regime | Status | Binding limits |
| --- | --- | --- |
| Bounded self-refinement | Convergent, evaluable, already industrial practice | Ceiling set by the evaluator it optimises against |
| Open-ended RSI | Not demonstrated | Grounding requirements, collapse dynamics, compute — on every measured axis |

Anthropic's essay frames a five-stage continuum ending in "closing the loop": agents that design and train their successor models. Current systems sit far along on execution — as of May 2026 Claude reportedly writes over 80% of Anthropic's merged code — while remaining bottlenecked on research direction-setting, meaning the choice of which problems matter ([When AI builds itself](https://www.anthropic.com/research/recursive-self-improvement)).

The sharpest test of that bottleneck is the Princeton-led "shadow evaluation": an agent takes on the central open-ended research question of an unpublished paper, and the paper's original authors grade the result. On two unpublished NeurIPS 2026 submissions, agents given six days and thousands of dollars of compute completed all the engineering without human help but made no substantial progress on the research questions. They generated hypotheses close to those the humans had originally pursued, abandoned them on limited data, and could not pivot once an approach stalled ([Kirgis et al. 2026](https://arxiv.org/abs/2607.27191); [coverage](https://www.technologyreview.com/2026/08/18/1142188/ai-recursive-self-improvement/)).

## Evolution: fitting an environment vs guiding your own improvement

The distinction you are drawing is real, the literature treats it as central, and it has two names.

**Evolvability** is biology's term for evolution improving its own capacity to improve, through canalization and modularity. But the field insists on a caveat that settles your question for the classical case: the emergence of evolvability does not require the evolutionary process to have knowledge about future environmental changes — evolvability is not a form of "directed evolution" ([Huizinga, Mouret & Clune 2018](https://direct.mit.edu/artl/article/24/3/157/2904/)). Classical evolvability is still second-order fitting, not guidance.

**Open-endedness** is where your distinction gets formalised. The move is to define improvement without a fixed environment to fit. Hughes et al. define open-endedness as the intersection of novelty (outputs become increasingly hard for an observer to predict) and learnability (they are not random — an observer can improve their understanding by studying the system's history), and argue it is an essential property of any artificial superhuman intelligence ([ICML 2024](https://proceedings.mlr.press/v235/hughes24a.html)). Note that the definition is observer-relative: that is the honest admission that improvement without an environment still needs a reference point from somewhere.

The working system fusing both poles is the **Darwin Gödel Machine**. It relaxes the Gödel machine's requirement of *proving* a change beneficial, requiring empirical evidence instead, and keeps an archive of discovered solutions so exploration stays open-ended rather than evolving a single line. It modifies its own code, thereby also improving its ability to modify its own codebase: SWE-bench 20.0% → 50.0%, Polyglot 14.2% → 30.7% ([Zhang et al. 2025](https://arxiv.org/abs/2505.22954); [blog](https://sakana.ai/dgm)).

The deepest statement of your question is Lehman, Meyerson, El-Gaaly, Stanley & Ziyaee: ML overlooks robustness to a qualitatively unknown future — Knightian uncertainty, uncertainty that cannot be quantified, which is excluded from ML's key formalisms. They argue RL's assumptions of fixed environments, discounted rewards and episodic boundaries structurally blind it to this, while evolution's *lack* of explicit formalism plus diversification pressure is exactly what handles it ([arXiv:2501.13075](https://arxiv.org/abs/2501.13075)). That is the strongest claim that fitting an environment and improving open-endedly are different things, and that current ML only does the first.

## Other mechanisms researchers take seriously

Six lines of work, each a different answer to "what is the thing that improves?"

| Mechanism | What it changes | Known limit |
| --- | --- | --- |
| Gödel machines ([Schmidhuber](https://people.idsia.ch/~juergen/goedelmachine.html)) | Own source code, only on a proof of higher expected utility | Proving most changes net-beneficial is infeasible |
| Meta-learning / learned optimisers | The learning algorithm | First-order improvements; humans still design the search space |
| Evolutionary program search with LLM mutation ([AlphaEvolve](https://arxiv.org/abs/2506.13131)) | Code, scored by automated evaluators | Needs a machine-checkable evaluator per problem |
| Self-play, self-reward, self-generated curricula | Training data and policy | Signal quality; collapse when grounding is lost |
| Quality-diversity and archives (MAP-Elites, novelty search) | The population of stepping stones | No single objective to certify progress against |
| AI-GAs ([Clune 2019](https://arxiv.org/abs/1905.10985)) | Architectures, learning algorithms and training environments at once | Compute; no demonstrated closed loop |

AlphaEvolve is the one with a genuine, if narrow, closed loop: at Google it produced a better data-centre scheduling algorithm, a circuit simplification, and accelerated training of the LLM underpinning AlphaEvolve itself.

The survey's structural claim cuts across all six: every improvement loop is a claim that some signal can substitute for human judgment. Ordering those signals into a verification hierarchy — formal verifiers strongest, intrinsic self-assessment weakest — demonstrated self-improvement strength tracks the hierarchy, and the failure modes follow from its violations.

## Impossibility arguments, and how sound they are

No published argument establishes impossibility. Each establishes that a specific mechanism has a specific ceiling.

**1. The Löbian obstacle (logical).** Löb's theorem implies an agent cannot generally trust its own soundness, so it appears unable to trust a successor to prove actions safe without predicting specifically what action will be taken ([Yudkowsky & Herreshoff 2013](https://intelligence.org/files/TilingAgentsDraft.pdf)). *Soundness:* real but narrow. The authors themselves demonstrate technical methods for avoiding it, and critics note it arises only from the choice to focus on systems at least as strong as Peano Arithmetic. It blocks *provable* self-improvement, not empirical self-improvement — which is why the Darwin Gödel Machine abandoned proof.

**2. Diminishing returns.** A system may improve itself infinitely often while total intelligence stays bounded: if each generation improves by half the last, it never gets beyond doubling ([Walsh, arXiv:1602.06462](https://arxiv.org/abs/1602.06462)). *Soundness:* logically valid, empirically unsettled. It is a claim about a rate nobody has measured.

**3. Recalcitrance.** Modelling a Bayesian predictive agent, Benthall finds the barriers to RSI through algorithmic change prohibitively high — such a system would need faster hardware and better data foremost, and those costs depend on the environment, not just on the agent's intelligence ([arXiv:1702.08495](https://arxiv.org/abs/1702.08495)). *Soundness:* the strongest sceptical argument, but it is a result about one narrow capacity (prediction) generalised to all of them.

**4. Collapse dynamics.** Two failure modes are derived for increasingly self-generated training data: entropy decay, where finite sampling causes monotonic loss of diversity, and variance amplification, where losing external grounding makes the model's representation of truth drift as a random walk. These are argued to follow from distributional learning on finite samples rather than from architecture, with RL under imperfect verifiers suffering similar semantic collapse ([arXiv:2601.05280](https://arxiv.org/abs/2601.05280)). *Soundness:* the best-evidenced limit here, but it bites *pure* self-generation. Grounding, verifiers and fresh data are known mitigations.

**5. Compute bottleneck.** If compute and cognitive labour are gross complements, recursive improvement in cognitive labour fizzles once bottlenecked on research compute — but whether they are complements or substitutes is not obvious, and recent analyses conflict ([arXiv:2507.23181](https://arxiv.org/abs/2507.23181)). *Soundness:* an open empirical question, not a proof.

One counter worth knowing: you can prove that the Kolmogorov complexity of an isolated deterministic system grows only logarithmically in time, but the whole burden then rests on showing that doing impactful real-world things requires an isolated machine to increase its Kolmogorov complexity ([Yudkowsky, *Intelligence Explosion Microeconomics*](https://intelligence.org/files/IEM.pdf)).

## The strongest case each way

**For.** Chalmers' framing is still the cleanest statement of what the argument actually needs. You require only (i) a self-amplifying cognitive capacity G, where increases in G bring proportionate or greater increases in the ability to create systems with that capacity; (ii) that we can create systems whose G exceeds our own; and (iii) a correlated capacity H we care about, such that small increases in H can always be produced by large enough increases in G. Given those, absent defeaters, G explodes and H with it ([Chalmers 2010](https://consc.net/papers/singularity.pdf)).

The empirical support is the trend in autonomous task length. METR measures a "time horizon" — the human-task duration at which an agent succeeds 50% of the time — doubling roughly every seven months from 2019 to 2026, with 2024–2025 data suggesting closer to four months and no visible plateau ([metr.org/time-horizons](https://metr.org/time-horizons/)). Add AlphaEvolve already measurably speeding up its own substrate, and the mechanism is not hypothetical.

**Against.** Four premises have to hold jointly, and failing any one lets the mechanism run without producing an explosion:

1. **Non-diminishing returns** — each round keeps yielding gains of similar size, rather than shrinking as the system approaches the ceiling of its measure.
2. **No wall** — no data, compute or physical constraint caps the current approach.
3. **Generality** — gains transfer broadly, not just lifting one benchmark.
4. **Speed** — the loop outpaces human correction; a loop you can pause and inspect each round is not a runaway.

Held against the evidence: every published loop is still scored on a narrow, task-specific signal, and no published loop has demonstrated the compounding step the argument needs, where each round makes the next round faster. The Darwin Gödel Machine's 20% → 50% is one lift, not a compounding series. And premise 3 is where the shadow evaluations bite.

The honest crux, in Sayash Kapoor's own words, is whether AI systems need open-ended creative ability to achieve recursive self-improvement, or whether steady gains on narrower measurable tasks could get them there instead — "that's frankly the trillion-dollar question right now".

## Can intelligent behaviour be defined generally enough to train for?

Definable, yes. Trainable against, only through an approximation that someone chose — which relocates the direction-setting problem rather than solving it.

Two serious attempts, both Kolmogorov-flavoured:

**Legg & Hutter** take around 70 expert definitions, extract their essential features, and formalise a general measure for arbitrary machines: intelligence as the ability to achieve goals across a wide range of environments, weighted by environment simplicity ([arXiv:0712.3329](https://arxiv.org/abs/0712.3329)). The catch is that the measure is only asymptotically computable, so building a practical test from it is not straightforward ([Legg & Veness](https://arxiv.org/abs/1109.5951)).

**Chollet** defines intelligence as skill-acquisition efficiency, emphasising scope, generalisation difficulty and priors rather than raw performance — a direct challenge to benchmarks that reward capability accumulation without regard for data efficiency ([arXiv:1911.01547](https://arxiv.org/abs/1911.01547), operationalised as ARC-AGI).

The standing objection applies to both. They use Kolmogorov complexity, equate simplicity with generality, and treat intelligence as a property of software interacting with the world through an interpreter — so if you build an AI for some purpose, you decide whether it fulfilled that purpose, and you are part of the agent's environment.

Chalmers conceded the related weakness himself: there may be many ways of evaluating cognitive agents, none deserving canonical status as "intelligence", and the correlations that hold between capacities within humans need not hold across arbitrary non-human systems.

## Questions you should also be asking

- **Who evaluates the evaluator?** Open-ended RSI means closed loops that also modify their own evaluators. The direction-setting bottleneck splits into a verification problem the hierarchy indexes, and a prior one — choosing what deserves evaluation at all — that it does not. The second half has almost no literature.
- **Is intelligence even scalar?** If it is not, "improving its own intelligence" may not name one thing, and the explosion argument loses its subject.
- **How would we measure a loop in progress?** The survey names governance-grade measurement of self-improvement as the field's most underpopulated niche.
- **Does open-endedness require an external world?** The artificial-life tradition on semantic closure and embodiment (Pattee, Bedau, Taylor) says the environment cannot be fully internalised.
- **Is this a major evolutionary transition?** Treating model variants as genetic material, with replication and selection over them, reframes the safety question as one about gating replication rather than about a single agent ([Evolvable AI](https://www.researchgate.net/publication/404014125_Evolvable_AI_Threats_of_a_new_major_transition_in_evolution)).

## Sources, in reading order

1. [Recursive Self-Improvement in AI: From Bounded Self-Refinement to Autonomous Research Loops](https://arxiv.org/abs/2607.07663) — Chen, Wang & Qu, 2026. The map of the territory.
2. [Position: Open-Endedness is Essential for Artificial Superhuman Intelligence](https://arxiv.org/abs/2406.04268) — Hughes et al., ICML 2024. The formal definition.
3. [Darwin Gödel Machine: Open-Ended Evolution of Self-Improving Agents](https://arxiv.org/abs/2505.22954) — Zhang et al., 2025. The working system.
4. [Evolution and the Knightian Blindspot of Machine Learning](https://arxiv.org/abs/2501.13075) — Lehman, Meyerson, El-Gaaly, Stanley & Ziyaee, 2025. Why fitting ≠ open-ended improvement.
5. [Can AI agents conduct open-ended AI research?](https://arxiv.org/abs/2607.27191) — Kirgis et al., 2026. The negative result that matters most.
6. [The Singularity: A Philosophical Analysis](https://consc.net/papers/singularity.pdf) — Chalmers, 2010. The argument's logical skeleton.
7. [Don't Fear the Reaper: Refuting Bostrom's Superintelligence Argument](https://arxiv.org/abs/1702.08495) — Benthall, 2017. The best-argued scepticism.
8. [AlphaEvolve](https://arxiv.org/abs/2506.13131) — Novikov et al., 2025. A real, narrow closed loop.
9. [On the Measure of Intelligence](https://arxiv.org/abs/1911.01547) and [Universal Intelligence](https://arxiv.org/abs/0712.3329) — the two definitions.
10. [awesome-open-ended](https://github.com/jennyzzt/awesome-open-ended) — Jenny Zhang's live bibliography for the open-endedness thread.
