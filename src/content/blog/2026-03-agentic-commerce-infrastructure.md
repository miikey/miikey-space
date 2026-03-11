---
title: 'The Infrastructure Layer for Agentic Commerce Is Being Assembled'
description: 'Stripe just shipped the Agentic Commerce Suite. That is not a product launch — it is a signal that the foundational infrastructure for AI-driven commerce is being built right now. Here is how I think about the full stack.'
heroImage: '/images/blog/llm-stack-fintech.jpg'
heroAlt: 'Agentic commerce infrastructure layers'
location: 'Singapore'
pubDate: 'Mar 11 2026'
---

Last week, Stripe announced the [Agentic Commerce Suite](https://stripe.com/blog/agentic-commerce-suite) — a solution that lets businesses make their products discoverable by AI agents, simplify checkout for agent-initiated transactions, and accept payments through a new primitive called Shared Payment Tokens.

I've been building payment infrastructure long enough to recognize when a product launch is a feature announcement versus when it's a signal that a new infrastructure layer is being assembled. This is the latter.

The specific capabilities Stripe shipped matter less than what they reveal: the plumbing for agentic commerce is being built in real time, right now, in 2026. The window where the architectural decisions get made is open. It won't stay open long.

Here is how I think about what's being built, layer by layer.

## The Discovery Problem: ACP Is the New SEO

One of the sharpest observations in Stripe's announcement is framing the merchant problem as a discovery problem. Businesses aren't asking "how do I process agent payments?" — they're asking "how do I get discovered by AI agents?"

This reframing matters. It means the first problem in agentic commerce is not payment. It's visibility.

In the web era, the answer to "how do I get found?" was SEO — optimizing your content and structure so search engine crawlers could index and rank it. Google became the discovery layer that most of the internet's commercial activity flowed through.

In the agentic era, the equivalent question is: "how do I get found by an AI shopping agent working on behalf of a buyer?" The answer is structured product data, real-time availability signals, and machine-readable catalog endpoints — all formatted to a standard that agents can consume programmatically.

Stripe is calling this standard ACP, the [Agentic Commerce Protocol](https://www.agenticcommerce.dev/). The design choice — a hosted ACP endpoint per merchant, syndicating product information to multiple agents through a single integration — is sound. Merchants don't want to build a custom catalog API for each agent they want to work with. They shouldn't have to.

> **ACP is to agentic commerce what sitemaps were to SEO — the machine-readable contract that lets the discovery layer do its job.** The merchants who figure out catalog optimization for agent discovery in 2026 will have the same structural advantage that early SEO adopters had in 2008.

The implication for merchants is direct: product discovery is about to bifurcate. There will be the Google graph and there will be the agent graph. Both matter. The optimization strategies are different.

![An engineer configuring product catalog APIs and structured data endpoints for multi-channel distribution](/images/blog/2024-09-ai-agents-demo-vs-reality-inline-01.jpg)
*The catalog layer is where agentic commerce starts — structured, machine-readable, real-time. Getting this right is the new SEO.*

## Shared Payment Tokens: The Right Design Pattern

The payment primitive Stripe introduced — Shared Payment Tokens — is worth spending time on because the design is genuinely interesting.

The problem it solves: an AI agent needs to complete a purchase on behalf of a buyer. The buyer has payment credentials on file somewhere. The agent needs to use those credentials to pay a merchant. But you don't want the agent to have raw access to the buyer's payment details — that's a security and fraud exposure you can't contain.

SPTs thread this needle with a pattern I recognize from my work on delegated payment authorization:

- **Scoped to a specific seller.** The token can't be used by a different merchant than the one it was issued for.
- **Bounded by time and amount.** The token expires and has a ceiling. An agent can't use it to make an unbounded charge three weeks later.
- **Observable throughout its lifecycle.** Every use of the token is visible, auditable, and can be revoked.

This is essentially a capability token with enforced constraints. The agent gets the minimum authority it needs to complete the transaction and nothing more. This is the right design pattern.

From a payments architecture perspective, what's notable is that Stripe built this on top of their existing Checkout Sessions API rather than as a separate system. That integration choice means SPTs inherit the full compliance, fraud, and settlement stack that Stripe has built over 15 years. New primitive, existing infrastructure. That's a good engineering decision.

The pattern also generalizes. Scoped, time-bounded, observable tokens for delegated authority — this is the right design not just for shopping agents but for any agent acting on behalf of a principal. The specific implementation will vary by context, but the design shape is correct.

## The Fraud Recalibration Problem Is Bigger Than It Looks

There is an observation buried in Stripe's announcement that I think deserves more attention than it got:

> *"Fraud signals tuned to human traffic are becoming outdated; AI agents lack human variability and can be misflagged as fraudulent."*

This is accurate and it has significant implications.

Fraud detection systems in payments are calibrated on behavioral signals derived from years of human transaction data. Velocity patterns, session behavior, device fingerprints, interaction timing — all of these are tuned to recognize what normal human commerce looks like. Anomalies get flagged.

AI agents are anomalous by definition relative to this baseline. They operate at machine speed. They don't browse, they query. They don't hesitate at checkout, they execute. They don't have the natural variance of human behavior. Running current fraud models on agent traffic will produce systematic false positives — legitimate agent-initiated transactions flagged as bot activity.

This isn't just a nuisance. False positives at scale mean legitimate revenue being declined, increased chargeback disputes, merchant trust erosion. For high-volume agentic commerce use cases — autonomous purchasing agents operating across thousands of transactions per day — this becomes a significant operational problem.

The solution isn't to whitelist all agent traffic. That would be a fraud exposure of a different kind. The solution is to build risk models calibrated specifically to agent behavior: different signal sets, different baseline patterns, different anomaly thresholds. Stripe is doing this with Radar for SPT transactions. The broader industry needs to do the same.

> **Every risk model in payments was built on human behavioral data. The shift to agentic commerce means rebuilding those models from first principles — not tuning them, rebuilding them. This is a multi-year infrastructure effort that most payment companies haven't started yet.**

![A payment operations team reviewing transaction monitoring dashboards, risk scores, and agent traffic patterns](/images/blog/2024-09-ai-agents-demo-vs-reality-inline-02.jpg)
*Fraud models calibrated on human behavior will systematically misclassify agent traffic. Rebuilding the risk stack for agentic commerce is infrastructure work that most payment companies haven't started.*

## The Full Stack, Layer by Layer

Pulling back, here is how I think about the complete infrastructure stack for agentic commerce — what exists, what's being built, and what's still early:

**Discovery layer** — machine-readable product catalogs, ACP endpoints, agent-optimized data formats. *Status: being built now.* Stripe is one entrant; others will follow. This will likely standardize around ACP or a derivative within 18 months.

**Checkout and fulfillment layer** — tax calculation, shipping logic, inventory verification, order management for agent-initiated transactions. *Status: Stripe has a workable solution; needs to mature for edge cases.* The complexity here is that checkout for agents needs to be fast and deterministic — agents can't handle the ambiguous states that human checkout flows navigate naturally.

**Payment primitive layer** — the token or credential mechanism that lets agents initiate payments. *Status: SPTs are the most complete current implementation.* Expect competing approaches from other payment infrastructure providers. The design principles — scoped, bounded, observable — will likely converge regardless of the specific implementation.

**Fraud and risk layer** — risk models calibrated for agent behavior, not just agent-aware human models. *Status: early.* Stripe is ahead of most by building this into SPT processing from the start. The rest of the industry is behind.

**Settlement and cross-border layer** — how agent-initiated payments clear and settle, especially across jurisdictions. *Status: largely unsolved.* For domestic payments, existing rails work. For cross-border agentic commerce — an agent in Singapore buying from a merchant in Germany, settling in seconds — the current correspondent banking infrastructure is a poor fit. Stablecoin settlement rails are the natural solution here, but the integration with mainstream commerce infrastructure is still early work.

**Identity and accountability layer** — how agents are identified, how their actions are attributed, how liability is assigned. *Status: nascent.* SPTs address part of this for the buyer-agent relationship. The broader question of agent identity — how a merchant knows which agent it's dealing with, what trust level to assign it, how to handle disputes — doesn't have a standard answer yet.

## What This Means for the Infrastructure Window

Infrastructure windows close faster than people expect. The companies that built the payment processing stack in the 2010s — Stripe itself being the obvious example — did so during a window when the architectural decisions were still being made. That window closed. It's now extremely difficult to displace the incumbents who got there first, because they have the network effects, the compliance infrastructure, and the merchant relationships.

The agentic commerce infrastructure window is open now. The ACP standard is live but not locked. The SPT design pattern is real but not universal. The fraud models haven't been rebuilt yet. The cross-border and stablecoin layers are genuinely unbuilt.

From where I sit — working on payment routing, cross-border settlement, and AI-driven financial operations — the opportunity is in the layers that the current wave of agentic commerce infrastructure isn't addressing: the settlement layer for agent transactions across jurisdictions, the identity layer for agents as economic participants, and the risk models that treat agent traffic on its own terms rather than as a variant of human traffic.

![Infrastructure engineers reviewing architecture diagrams for cross-border settlement systems with stablecoin integration](/images/blog/mpc-wallets-01.jpg)
*The settlement and identity layers for agentic commerce are the most open problems. Cross-border, stablecoin-native, agent-identity-aware infrastructure doesn't exist yet at production scale.*

Stripe shipping the Agentic Commerce Suite is a signal that this market is real and the infrastructure investment is warranted. The catalog discovery and checkout layers are getting solved. The harder, more fundamental layers — settlement, identity, risk — are where the next two years of infrastructure work will happen.

The window is open. It won't stay that way.

---

*I'm building in the payment routing and settlement layer of this stack. If you're working on the infrastructure problems in agentic commerce — from any angle — I'd like to compare notes.*
