---
title: 'The Pace of AI Changed. So Did the Game.'
description: 'In 18 months, we moved from asking whether AI would be useful to treating it as production infrastructure. The rate of change did not just accelerate — it changed the nature of the problem for anyone building serious systems. Here is how I think about what actually shifted.'
heroImage: '/images/blog/ai-fintech-01.jpg'
heroAlt: 'AI infrastructure pace of change'
location: 'Singapore'
pubDate: 'Mar 18 2026'
---

Sometime in mid-2024, the question changed.

For a couple of years before that, the central question for anyone building with AI was: *is this actually useful?* Can these models do real work, reliably, in production? The honest answer was: sometimes, in narrow domains, with a lot of human supervision. Useful enough to justify experimentation. Not reliable enough to load-bear.

That question has been answered. The uncertainty now is different. It is not whether AI is useful — it manifestly is — but how to build when the substrate you are building on keeps changing underneath you. Every six months, the model that was frontier is now mid-tier. Every 12 months, what required expensive proprietary APIs is now running locally on commodity hardware. Every 18 months, a capability that seemed like science fiction is now a product feature in something you can get for free.

The pace did not just accelerate. The *nature* of the problem changed. And most of the frameworks people use for thinking about AI — when to adopt, what to build on, how much to invest — have not caught up to what is actually happening.

Here is how I see it from where I sit.

## The Cost Floor Collapsed

The single most important thing that happened in AI over the past 18 months is not a model release or a capability breakthrough. It is the cost collapse.

At the start of 2024, running a capable language model at production scale was genuinely expensive. GPT-4-level reasoning cost tens of dollars per million tokens. That price point made certain use cases economically viable — high-value, low-volume tasks where the AI output justified the cost — and made entire categories of applications non-starters. You could not build a product that made thousands of AI calls per user per day and make the unit economics work.

By early 2026, the same level of reasoning costs somewhere between 50 and 100 times less. The benchmark capabilities that defined GPT-4 in 2023 are now available in open models that run on a single consumer GPU. Frontier model costs have dropped correspondingly as competition intensified.

What a 100x cost reduction means is not just "the same things are cheaper." It means entire categories of applications that were previously uneconomical become viable. Continuous background AI analysis. Per-interaction reasoning across millions of users. Embedded intelligence in workflows that would never have justified the cost at 2023 pricing.

> **A 100x cost reduction does not make the same things cheaper. It makes a qualitatively different set of things possible.** The use cases that become viable at $0.50/million tokens are structurally different from the use cases that made sense at $30/million tokens. Most product teams have not fully recalibrated their thinking for what this unlocks.

The analogy I keep coming back to is cloud computing in 2007–2010. The cost of compute dropped enough that it changed what you could build, not just what it cost to build the same things. AI inference is undergoing the same transition right now. We are in the middle of it, and I do not think most teams have fully recalibrated what it means for their product decisions.

## The Capability Gap Closed in Ways That Matter

The other structural shift is the closing of the gap between frontier and accessible models.

For most of 2023 and into 2024, there was a meaningful capability cliff between what you could do with the best proprietary models and what you could do with open alternatives. GPT-4 and Claude 2 were in a different tier. If you needed real reasoning quality, you were using the expensive APIs, full stop.

That cliff has been significantly compressed. Not eliminated — frontier models still have an edge on the hardest reasoning tasks. But the gap on the *practical* tasks that most production applications actually need has closed enough that it changes the build decision.

This matters because model dependency was a real strategic risk. If your product's quality is tied to one API provider's model, you are exposed to pricing changes, policy changes, deprecations, and the possibility that a competitor gets better access to the same resource. The closing of the capability gap means you now have genuine choices. You can build on multiple models. You can run critical workloads locally. You can switch providers without rebuilding your core logic.

For the systems I work on — payment routing, compliance analysis, cross-border settlement decisions — the practical question has shifted from "is the model good enough?" to "what is the right model for this specific subtask?" That is a meaningfully better position to be in. It is also a more complex one.

![Dashboard showing AI model performance and cost comparison across providers, with routing logic between frontier and local models](/images/blog/llm-stack-fintech.jpg)
*The capability gap between frontier and accessible models has compressed. The real question is now which model is right for which task — not whether the open alternatives are viable.*

## Reasoning Became Infrastructure

The capability shift that got the most attention in 2025 was reasoning — models that do not just predict the next token but work through problems explicitly before producing an answer.

What I think got underappreciated is what this shift means architecturally.

When AI systems were fundamentally pattern-matching and synthesis tools, the right mental model was: AI as a smart autocomplete. You give it a well-structured prompt, it returns a well-structured output. The quality of your prompt engineering determined a lot of the output quality. The system was brittle under novel conditions.

Reasoning models changed this. A model that works through a problem step by step before answering — that can identify contradictions, check its own logic, recover from wrong assumptions — is not a smarter autocomplete. It is a different kind of system. It behaves more like a collaborator than a tool.

The implications for how you build are real. Brittle prompt engineering becomes less important as models get better at handling ambiguous or underspecified inputs. Multi-step reasoning chains that used to require careful scaffolding in the application layer can now happen inside the model. The line between "orchestration logic" and "model intelligence" is moving.

For engineers, this means some of the complexity that lived in your code is moving into the model. For product teams, it means user experiences that required careful UX scaffolding to work can now be more open-ended. The cost of letting the model figure out the task structure is lower than it used to be.

> **Reasoning is not just a better answer quality. It is a different architecture.** The systems you build on top of a reasoning model are structurally different from the systems you built on top of a completion model. The failure modes are different. The best practices are different. Most teams are still applying 2023 patterns to 2026 models.*

## The Agentic Turn Completed

The other shift worth naming directly: agents went from demos to infrastructure.

In 2024, "AI agents" was still primarily a demo category. Impressive showcases of what was possible. Occasional production deployments in highly controlled settings. A lot of writing about the potential without much evidence of the reality.

That changed in 2025. Not all at once, and not uniformly across sectors — but the pattern shifted clearly enough that I stopped thinking of agents as a bet on the future and started thinking of them as a current infrastructure choice.

What drove this? Partly the model improvements — reasoning models are better agents because they handle unexpected states more gracefully. Partly the tooling maturity — frameworks for agent orchestration, memory, and tool use reached a level where building production systems was no longer primarily a research exercise. Partly just accumulated learning from teams who had been running early agent systems and had worked out enough of the failure modes to make them reliable.

The agentic workflows I am running today would not have been viable 18 months ago. Not because the core idea was wrong, but because the reliability, cost, and tooling were not there yet. All three have crossed thresholds that matter.

![Multi-agent orchestration system showing task delegation, parallel execution, and tool use across a complex workflow](/images/blog/ai-agents-01.jpg)
*Agent systems went from demos to production infrastructure in 2025. The capability and tooling crossed a threshold. The question is no longer "will agents work?" but "what are the right patterns for production agent systems?"*

The transition also revealed a new category of infrastructure problems. When agents are demos, you can tolerate unreliability. When agents are infrastructure — when they are running financial transactions, making commitments on behalf of users, operating autonomously for hours across complex tasks — the error handling, observability, and accountability requirements are different. Production agent infrastructure is an engineering discipline, not a prompting exercise.

## What Is Stable Enough to Build On

The natural question for anyone building in this environment is: what do you anchor to when the ground keeps moving?

I have been thinking about this in terms of layers.

**The model layer is not stable.** The specific model you are using today will be superseded in 6-12 months. If your system depends on quirks of a specific model's behavior or is tightly coupled to one provider's API surface, you are accumulating technical debt. The right architecture treats models as interchangeable components behind an abstraction layer. The prompt logic and output handling should be model-agnostic where possible.

**The task decomposition layer is relatively stable.** The way you break a complex problem into subtasks — the orchestration pattern — is driven more by the nature of the problem than by the specific model capabilities. These patterns are evolving but slower than the underlying models. Investing in clean task decomposition logic has a longer shelf life than investing in model-specific optimizations.

**The data and integration layer is the most stable.** Your data assets, your integration with external systems, your domain-specific knowledge and business logic — these compound over time and do not deprecate when a new model ships. The teams that are building lasting AI advantages are the ones treating their domain knowledge and data quality as the durable asset, with AI as the increasingly capable processing layer on top.

**The infrastructure assumptions are changing.** The economics of AI have shifted enough that some architecture decisions that made sense in 2023 do not make sense in 2026. What you cached heavily to avoid expensive model calls, you might not need to cache anymore. What you avoided running at inference time because of cost, you might now run. Revisiting the economic assumptions embedded in your system architecture is worth the time.

> **The durable assets in AI are not the models — they are the domain knowledge, data quality, and task decomposition logic that sit on top of the models.** Build those well. Treat the model layer as the fast-moving substrate it is, and architect accordingly.

![Infrastructure architecture diagram showing stable and fast-moving layers in an AI production system](/images/blog/stablecoins-01.jpg)
*The right mental model: data and domain knowledge as the durable foundation, task logic as the medium-term investment, models as the fast-moving layer. Architect for the half-life of each component.*

## The Question That Now Matters

I have stopped asking "is AI ready for production?" — that question has been answered. The questions I am actually sitting with now are harder.

How do you build durable systems when the capability surface of your core component changes faster than your release cycle? How do you make architectural decisions when the cost assumptions embedded in those decisions might be invalid in 12 months? How do you calibrate what to build internally versus buying from vendors when the vendor landscape itself is in flux?

These are genuine engineering and strategy questions. They do not have clean answers yet. The teams that are figuring them out in production right now — accepting the uncertainty, building with appropriate abstraction, staying close to the model and infrastructure changes as they happen — are building real advantages.

The pace of change is not slowing down. If anything, the dynamics that drove the 2024-2025 cycle — intense competition, massive capital deployment, open source closing the gap — are still in full effect. The next 18 months will produce changes as large as the last 18.

That is uncomfortable for people who want stable foundations. It is an advantage for people who are paying close attention and building to adapt.

I have made my bet on the latter.

---

*The infrastructure questions in AI systems — cost modeling, multi-model routing, production agent reliability — are the problems I'm working on daily. If you're building in this space and hitting the same walls, I'd like to compare notes.*
