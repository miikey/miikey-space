---
title: 'MPP Is What "Agent Payments" Actually Looks Like as a Standard'
description: 'Stripe and Tempo just published the Machine Payments Protocol — an open standard that lets AI agents pay for things directly, without human intervention. This is not a product launch. It is the protocol layer for the agent economy arriving on schedule.'
heroImage: '/images/blog/card-issuance-api-01.jpg'
heroAlt: 'Payment protocol infrastructure for AI agents'
location: 'Singapore'
pubDate: 'Mar 19 2026'
---

A few weeks ago I wrote that AI agents need wallets — that the missing primitive for agentic systems was not capability but economic identity. That agents could reason and execute but still could not pay, and that every workflow touching a transaction hit the same wall.

Last week, Stripe and Tempo published the [Machine Payments Protocol](https://mpp.dev) — an open standard that defines exactly how an AI agent should be able to pay for things. Visa announced support. Coinbase's parallel [x402 standard](https://x402.org) is moving in the same direction. Stripe said it supports both.

The protocol layer for agent payments is now being assembled in real time. This is faster than I expected and slower than the use cases demanded.

Here is how I think about what just happened.

## The Problem MPP Solves Is Structural, Not Incidental

To understand why MPP matters, you have to start with what it means for an AI agent to pay for something today.

The current payment experience — every checkout flow, every SaaS subscription, every API billing page — was designed for a human with a browser and a credit card. The implicit UX assumptions are everywhere: you navigate to a pricing page, you read the tiers, you select a plan, you fill in a form, you authorize a charge. These steps feel frictionless to a person. To a software agent, they are a wall.

The friction is not a UI problem. It is a protocol problem. There is no machine-readable way to ask "what does this cost?" and receive a structured answer. There is no standard for a service to say "pay this amount at this address to get this resource." There is no interoperable mechanism for an agent to authorize a payment without a human intermediary.

MPP defines all three.

The protocol flow is clean:

1. The agent requests a service or resource
2. The service returns a structured payment request — amount, currency, supported payment methods, terms
3. The agent authorizes payment using its configured payment method (stablecoin, credit card, or BNPL)
4. The resource is delivered

Four steps. No human. No checkout page. No credential management per-vendor. The payment negotiation happens at the protocol level, in the same request-response pattern that agents already use for everything else.

> **The insight at the center of MPP is that payments are just another API call if you design them that way.** The reason they have not worked like API calls until now is not technical — it is that nobody had defined the protocol. Stripe and Tempo just defined it.

This is the right abstraction. The flow is analogous to how HTTP handles content negotiation: the client announces what it can accept, the server announces what it offers, they agree, the transaction completes. MPP applies the same pattern to payments.

## What the Early Use Cases Actually Reveal

The use cases that have launched on MPP are instructive — not because of their scale, but because of what they reveal about where agent payment friction was highest.

**Browserbase** is letting agents pay per session for headless browser access. Before MPP, the billing model for this kind of API was the standard monthly subscription — you pay Stripe $X/month, you get an API key, the agent uses it. The problem is that the agent has no way to negotiate scope, no way to pay only for what it uses, and the billing is attached to a human account that may not correspond to any particular agent's usage.

Per-session pricing changes this. The agent knows the cost before it starts. It pays for exactly what it uses. The economic relationship is between the agent and the service — not between a human cardholder and a subscription plan that happens to proxy access.

**PostalForm** — an agent paying to send a physical letter — is the more interesting use case to me. It is not interesting because of the domain (physical mail is not a big market). It is interesting because it is a demonstration that MPP works across the analog-digital boundary. The agent initiates a digital payment, and a physical action happens in the world as a result. That is the general case for a large category of agentic workflows: digital authorization, real-world execution.

The sandwich shop is the proof-of-concept that made people laugh, but the underlying mechanic is serious. An agent that can navigate a checkout flow, evaluate options, authorize payment, and have food delivered is not a toy — it is a template for autonomous consumer purchasing at scale. The reason it is a sandwich today is because sandwiches are low-stakes and easy to demo. The reason it matters is that the same flow works for anything with a checkout.

![AI agent completing a transaction workflow — from service request through payment authorization to resource delivery, no human in the loop](/images/blog/2024-09-ai-agents-demo-vs-reality-inline-01.jpg)
*The use cases launching on MPP are small in scale but large in implication. Per-session pricing, physical world delivery, autonomous purchasing — these are the patterns that define how agents will transact at scale.*

## MPP vs x402: Why Standards Competition Here Is Healthy

The obvious question when a new standard ships is: will it win? In this case, I think the more useful question is: which part of the market does each standard serve?

**x402** (Coinbase, World) is built on crypto rails. It is native to the on-chain world — USDC or similar stablecoins, cryptographic authorization, settlement on L2s. For agents operating in DeFi, Web3 infrastructure, or any context where on-chain settlement is already part of the system, x402 is the natural fit. No fiat conversion, no traditional payment processor, full programmability.

**MPP** is built to span both worlds. Stripe's explicit design choice — supporting stablecoins, credit cards, and BNPL — means MPP can serve agents operating in traditional commerce contexts where fiat is still the settlement layer. The merchant does not need to accept crypto. The agent can pay with a card-on-file. The protocol is agnostic about the underlying payment method.

Stripe announcing support for both is the correct call. These standards are not substitutes; they serve different payment contexts. The infrastructure that gets built on top of them — routing, compliance, risk management — needs to handle both, because different merchants and different agent use cases will land in different places.

> **Standards competition in payments usually ends one of two ways: one wins, or both become layers in a stack that routes between them.** I think MPP and x402 are on track for the second outcome. Stripe routing between them is the early evidence.

The analogy is card networks. Visa and Mastercard coexist because merchants accept both and issuers issue both. The routing happens at the payment processor level. MPP and x402 will coexist because the agents that matter will need to pay in both modes — on-chain when the service is natively crypto, off-chain when the service is traditional commerce. The infrastructure that does the routing is where the durable value gets built.

![Payment protocol architecture showing MPP and x402 as parallel rails with shared routing infrastructure — stablecoin and fiat settlement paths converging at the processor layer](/images/blog/2025-01-stablecoins-having-their-moment-inline-01.jpg)
*MPP and x402 are not competing for the same market. They are covering different payment rails for the same underlying use case — agent-initiated transactions. The infrastructure that routes between them is the more interesting build.*

## The Protocol Layer vs the Application Layer

Something worth being clear about: MPP is a protocol, not a product. What Stripe shipped is a specification — a definition of how agents and services should communicate about payment. What gets built on top of that specification is where the interesting work happens.

The parallel I keep reaching for is HTTP. HTTP defined how browsers and servers should communicate. It did not define what the content should be, what the business logic should look like, or how to handle authentication. Those were application-layer problems that got solved over years by a thousand different projects. HTTP provided the common substrate that made all of them interoperable.

MPP is doing the same thing for agent payments. It defines the payment negotiation layer. It does not define:

- How agents should manage payment credentials securely
- How services should verify agent identity and assign trust levels
- How spending policies should be enforced for agent-initiated transactions
- How disputes should be handled when an agent pays for something incorrectly
- How cross-border tax and compliance should work for agent-initiated purchases

These are all open problems. They are also the application-layer problems that builders will spend the next 3-5 years solving. The protocol gives them a common foundation to build on.

For anyone building payment infrastructure for the agentic era — which includes the systems I work on — the right mental model is: MPP is the substrate. Build your agent payment stack on top of it the same way you would build an application on top of HTTP. The protocol is not the product. The product is everything you build on the protocol.

> **MPP being open source and multi-rail is the right design.** A proprietary standard would have fragmented the ecosystem before it had a chance to form. An open standard that Stripe, Visa, and Coinbase all support gives builders a stable foundation. The business model is in the application layer, not in owning the protocol.*

## What I Am Watching

The things I am paying attention to as MPP gains adoption:

**Agent identity at the protocol level.** MPP as specified does not have a strong story about how a merchant knows which agent it is dealing with. Knowing that a payment came from "an AI agent authorized by some human" is not sufficient for most compliance contexts. The identity layer needs to mature. I expect DID-adjacent standards to become relevant here sooner than people think.

**Spend controls and policy enforcement.** Enterprises will not deploy agents on MPP without a way to define what agents can spend, on what categories, up to what limits, with what audit requirements. This is not a protocol problem — it is an application-layer problem — but it needs to be solved before enterprise adoption accelerates.

**The fraud question.** MPP-initiated transactions will have different behavioral signatures than human-initiated ones. The fraud models that protect current payment rails were not designed for agent traffic. We are back to the same problem I flagged in the agentic commerce piece: risk models calibrated on human behavior will systematically misclassify agent transactions. Rebuilding those models for MPP traffic is infrastructure work that most payment companies have not started.

**Cross-border MPP.** The use cases that launched on MPP are mostly domestic US transactions. The interesting version of this — an agent in Singapore paying a service in Germany, settling in seconds, with correct tax handling — is the cross-border problem. That requires more than a payment protocol; it requires the settlement rails and compliance infrastructure to catch up.

![Global payment routing map — cross-border agent transactions spanning multiple jurisdictions, settlement rails, and compliance frameworks](/images/blog/acquiring-landscape-01.jpg)
*The domestic MPP use cases are the easy version. Cross-border agent payments — with tax, compliance, and FX implications across jurisdictions — is the harder problem that the protocol alone does not solve.*

## The Thesis Is Playing Out on Schedule

I wrote about agent wallets because the missing primitive for agentic systems was obvious from where I sit. Agents that could not pay could not be fully autonomous. The infrastructure for agent economic identity was the gap between "impressive demo" and "production system."

MPP is the standard that makes agent economic identity interoperable. It is what "AI agents need wallets" actually looks like when the industry moves from thesis to infrastructure. The timing — Stripe and Tempo publishing this standard in early 2026, Visa immediately announcing support, Coinbase's parallel standard moving simultaneously — is consistent with the infrastructure window I described in the agentic commerce piece.

The protocol layer is being assembled now. The application layer will take years. The teams that are building on the protocol today — agent payment infrastructure, spend controls, identity, cross-border settlement — are building the equivalent of what Stripe built on top of HTTP in 2010.

The window is open. MPP just made it significantly easier to identify where the work needs to happen.

---

*The payment routing and cross-border settlement systems I work on are being updated to support MPP. If you are building agent payment infrastructure — or hitting walls trying to get agents to pay for things in production — I'd like to compare notes.*
