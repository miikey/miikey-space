---
title: 'The Harness Is the Product'
description: 'Anthropic just published their most instructive engineering post yet — on how they build harnesses for long-running AI agents. The real insight is not the architecture. It is the methodology: every component encodes an assumption about what the model cannot do, and those assumptions expire. Here is what that means for anyone building production AI systems.'
heroImage: '/images/blog/ai-agents-01.jpg'
heroAlt: 'Multi-agent harness architecture for long-running AI applications'
location: 'Singapore'
pubDate: 'Mar 27 2026'
---

Anthropic's engineering team published a post this week on [harness design for long-running applications](https://www.anthropic.com/engineering/harness-design-long-running-apps) that is worth reading closely. Not because the specific architecture they describe is something you should copy — it is not. But because of a single principle buried toward the end that reframes how I think about every AI system I am building.

> *"Every component in a harness encodes an assumption about what the model can't do on its own, and those assumptions are worth stress testing — both because they may be incorrect, and because they can quickly go stale as models improve."*

That sentence is doing a lot of work. Let me unpack why.

## What They Actually Built

The Anthropic piece walks through an evolving three-agent architecture: a planner that expands a vague prompt into a full product spec, a generator that implements features in sprints, and an evaluator that uses Playwright to click through the live application the way a real user would, then grades the output against explicit criteria before feeding results back to the generator.

The inspiration is GANs — Generative Adversarial Networks — where a generator and discriminator push each other toward better outputs through structured competition. Applied to software: the generator writes code, the evaluator finds problems, the generator responds to the feedback, repeat. Simple in concept. The execution details are where it gets interesting.

Two problems motivated the design. First, **context anxiety**: models approaching their context limit start wrapping up work prematurely rather than continuing. The solution — context resets that completely clear the window and hand off state through structured artifacts — addresses the symptom at the cost of orchestration overhead. Second, **self-evaluation failure**: when asked to grade their own output, agents reliably praise work that a human observer would recognize as mediocre. Separating the generator from the evaluator breaks this dynamic. A standalone evaluator prompted toward skepticism is far easier to tune than a generator prompted toward self-criticism.

The evaluator tuning process they describe is what most engineering teams skip, and what makes or breaks production AI QA. The raw model is a poor QA agent. It identifies real issues, then convinces itself they are not significant. It tests superficially and misses edge cases. Their fix was to read the evaluator's logs, find cases where its judgment diverged from theirs, and update the prompt to solve for those cases — iterating until the evaluator graded in a way they found reasonable. That process took several rounds. It is the kind of work that does not feel like engineering but determines whether your system is useful.

![Three-agent pipeline: planner expanding prompt to spec, generator implementing features, evaluator running live application tests and grading against criteria](/images/blog/llm-stack-eval.jpg)
*The generator-evaluator separation is the structural insight. Tuning a standalone evaluator toward skepticism is tractable. Making a generator critical of its own work is not.*

## The Part That Changes Everything

Here is the methodological shift that I think matters more than the architecture.

They built the harness on Claude Opus 4.5, which exhibited context anxiety strongly enough that context resets were essential. When Opus 4.6 shipped — with better long-task coherence, improved long-context retrieval, and stronger self-correction — they went back to the harness and stripped out the sprint construct entirely. The model had improved past the point where the scaffolding was load-bearing. What had been a necessary architectural component became unnecessary overhead.

They ran the updated harness on a 4-hour, $124 DAW build. The builder ran continuously for over two hours without sprint decomposition. The evaluator still caught real issues at the end — feature stubs, missing interactions, API routing bugs — but the complexity of managing per-sprint context resets was gone.

The cost table in the piece is instructive: planner at $0.46, first build round at $71, QA at $3, second build at $37, total $124 for a functional browser-based DAW with an integrated AI agent. That is an entirely different cost structure than what I was seeing 18 months ago for comparable output quality.

> **The right framing is not "how do I build a harness?" but "what does my harness need to compensate for, and when does that compensation become unnecessary?"** Every piece of scaffolding is a bet against a specific model limitation. As models improve, those bets expire. The teams that revisit their harnesses when new models ship — stripping away what is no longer load-bearing — will consistently outperform the teams that treat their architecture as stable.

## What This Means for Production Systems in Fintech

I build payment infrastructure. The context here is slightly different from writing frontend applications — the error tolerance is lower, the compliance requirements are real, and the financial stakes mean that an evaluator that misses a bug is not an aesthetic failure but potentially a regulatory one.

But the structural lessons apply directly.

**The evaluator pattern is the missing piece in most financial AI workflows.** Most teams building AI into payment routing, fraud detection, or compliance analysis have a generator (the model making decisions) but no evaluator (a separate system grading the quality and reliability of those decisions). They rely on downstream metrics — transaction failures, dispute rates, compliance flags — as their feedback signal. That is slow and expensive feedback. A purpose-built evaluator that exercises the system the way an auditor would, before decisions reach production, is the missing architectural layer.

The challenge in financial contexts is that the evaluation criteria need to be explicit, gradable, and auditable in ways that "does this design look polished?" does not. But that is actually an advantage. The Anthropic team spent real effort turning subjective aesthetic judgments into concrete grading criteria. In payments and compliance, many of the relevant criteria are already explicit — regulatory requirements, transaction rules, risk thresholds. Turning those into evaluator scoring criteria is more tractable than the design case.

**Context resets are an underappreciated pattern for long-running financial workflows.** A multi-hour autonomous agent processing a compliance review, a transaction reconciliation, or a multi-step settlement operation will hit context limits. The choice between compaction (summarizing earlier context in place) and reset (fresh agent with structured handoff) is not obvious. The Anthropic finding — that compaction preserves continuity but does not eliminate context anxiety, while reset provides a clean slate at the cost of handoff quality — maps directly to financial workflow design. For tasks where agent coherence matters more than continuity, structured resets are worth the orchestration overhead.

**The planner step is undervalued.** The Anthropic architecture includes a planner that takes a short prompt and expands it into a detailed spec before any implementation begins. They note that without the planner, the generator under-scoped by default. In financial contexts, the equivalent is the difference between an agent that starts executing on an underspecified task and one that first produces a verifiable plan that a human can review before work begins. The planner step is where human oversight can be meaningfully inserted without creating the bottleneck of approving every individual action.

![Agent workflow for financial systems showing planner-generator-evaluator pipeline with human oversight checkpoint at plan review stage](/images/blog/llm-stack-fintech.jpg)
*The planner step is where human oversight integrates cleanly. Review the plan before execution rather than each individual action — better leverage, same level of control.*

## The Simplification Imperative

The piece ends with a principle I want to call out directly because it is violated in almost every production AI system I have reviewed.

> *"Find the simplest solution possible, and only increase complexity when needed."*

Most teams do the opposite. They add scaffolding to address model failures, then keep the scaffolding when the model improves past the failure. They treat complexity as safety. The result is systems that are simultaneously expensive to run and fragile to maintain — over-engineered for the current model, misaligned with the current capability envelope.

The Anthropic team's iterative simplification process — removing one component at a time, reviewing the impact on output quality, keeping what is load-bearing and stripping what is not — is the right methodology. It requires actually shipping with a new model and reviewing outputs before drawing conclusions. You cannot simplify a harness by reasoning about it; you have to run it and read the traces.

For teams shipping financial AI systems, this has a specific implication: the architecture you designed against Sonnet 3.5 may be over-complex for Sonnet 4.5. The compaction strategy you built for 4.5's context anxiety may be unnecessary overhead on Opus 4.6. The prompting work you did to get reliable extraction from a weaker model may be working against you on a stronger one that handles ambiguity better without explicit scaffolding.

The economics have shifted. The capability envelope has shifted. The right harness for the current model is not the same as the right harness for the model you built against.

## The Durable Investment

If the harness components are all potentially temporary — encoding assumptions about model limitations that will expire — what is worth investing in?

The answer from this post is the same one I have been arriving at from the infrastructure side: **the evaluation criteria are the durable asset.**

The Anthropic team spent significant effort developing the four design criteria that drove their frontend evaluator. Those criteria — design quality, originality, craft, functionality, with explicit definitions and calibrated weightings — are reusable across model generations. They encode domain judgment in a form that can drive an evaluator regardless of which model is doing the evaluation.

In financial contexts, the equivalent investments are: explicit evaluation rubrics for compliance decisions, verifiable test suites for transaction routing logic, auditable criteria for risk assessment workflows. These compound. They are not model-specific. When the next model ships, you update the generator and keep the evaluator criteria. The work you did to build reliable evaluation logic does not expire.

The harness scaffolding around models will keep evolving. The criteria for what good looks like in your domain will stay stable far longer.

> **The models are the fast-moving layer. The evaluation criteria are the durable investment.** Build the criteria carefully. Treat the scaffolding around them as an implementation detail that will need to change.

## What I Am Watching

A few specific things from the Anthropic piece that I expect to become standard practice over the next 12 months:

**Playwright-based evaluators** — using browser automation to exercise AI-built applications the way a real user would, rather than scoring static screenshots — will become the default QA layer for any application built by an AI coding agent. The pattern is too high-leverage not to generalize.

**Sprint contracts** — the pre-implementation negotiation between generator and evaluator about what "done" looks like for a given chunk of work — are the right primitive for inserting verifiability into autonomous coding. I expect this pattern to show up widely in production agent systems, including in financial contexts where "done" needs to be auditable.

**Model-specific harness tuning** is going to become a competitive differentiator. Teams that have invested in the evaluation infrastructure to quickly characterize a new model's capabilities and failure modes — and can update their harnesses accordingly — will compound advantages that teams waiting for benchmarks will not. The Anthropic team's ability to ship Opus 4.6 support quickly, stripping the sprint construct because the model had improved past the need, is the pattern to emulate.

The pace of model improvement is not slowing down. The harness design surface is expanding with it.

---

*The harness design patterns described here apply directly to production financial AI systems — payment routing, compliance workflows, autonomous settlement operations. If you are building in this space and working through the same architectural questions, I want to compare notes.*
