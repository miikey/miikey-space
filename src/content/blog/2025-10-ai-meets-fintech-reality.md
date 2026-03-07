---
title: 'Where AI and Fintech Actually Intersect'
description: 'Not the pitch deck version. The practical reality of deploying AI across payment operations, risk management, and product development in a regulated financial services context.'
pubDate: 'Oct 14 2025'
---

There's a pitch deck version of AI in fintech: "AI-powered everything." And then there's what actually works in production when you're moving real money under real regulatory constraints.

After two years of deploying AI across our payment infrastructure, here's the honest version.

## Where AI Is Genuinely Working

**Transaction monitoring and anomaly detection.** This is the most mature and unambiguously valuable application. ML models trained on transaction patterns detect anomalies that rule-based systems miss — unusual velocity patterns, merchant category code mismatches, geographic impossibilities. Our current system catches 3x more true fraud than the rule-based system it replaced, with fewer false positives.

The key: the model flags; humans decide. Full automation of fraud decisions creates liability and regulatory risk that isn't worth the operational savings. The right abstraction is AI-augmented investigation, not AI-automated decisions.

**Payment routing optimization.** Dynamically selecting the optimal acquirer, currency path, and fallback strategy for each transaction. The optimization surface is complex: approval rates, cost, settlement speed, compliance constraints, and counterparty reliability. ML models that learn from historical outcomes are outperforming hand-tuned routing rules.

The improvement is meaningful: a 2-3% improvement in approval rates on a $1B annual payment volume is $20-30M in additional revenue for our merchants. This is where AI ROI is clearest.

**Customer support triage and resolution.** Our support agent handles ~65% of inbound merchant inquiries end-to-end or with minimal human editing. For the remaining 35%, it provides context and draft responses that reduce average handling time by ~40%.

## Where AI Is Not Working (Yet)

**Compliance automation.** The dream: AI reads regulations, interprets requirements, and automatically adjusts compliance controls. The reality: regulations are ambiguous by design, require contextual judgment, and the cost of misinterpretation in a regulated environment is severe. We use AI to assist compliance officers — summarizing regulatory changes, flagging potentially affected processes — but we're nowhere near automated compliance.

**Credit decisioning without guardrails.** AI-driven credit scoring for merchant advances has shown promise in controlled tests, but the regulatory requirements for explainability (why was this merchant declined?) and the fair lending implications create constraints that pure ML approaches struggle with. We use ML as one input in a structured decisioning framework, not as the decisioning system.

**End-to-end autonomous operations.** The promise of AI agents that handle complex multi-step operational workflows without human oversight is not production-ready for financial operations. Every attempt has produced edge cases where the agent takes confident wrong actions that are expensive to reverse.

## The Uncomfortable AI Questions for Fintech

**Model risk is real and underappreciated.** When an ML model is making routing decisions on live payment traffic, a subtle model degradation can cost real money before anyone notices. We've built monitoring for model performance that alerts on drift — but the tooling for ML observability in financial applications is still immature.

**Data moats are eroding.** The competitive advantage of proprietary training data is real but less durable than hoped. Foundation models improve on general capabilities fast enough that domain-specific fine-tuning advantages narrow over time. The durable advantage is in the quality of data labeling, evaluation frameworks, and deployment infrastructure — not the raw data itself.

**Talent allocation is shifting.** We now have more ML engineers than we had total engineers three years ago. The question of when to build vs. when to buy AI capabilities — and how to evaluate vendor claims in a hype-saturated market — is a constant challenge.

## The Product Philosophy

The framework I keep coming back to: AI should make expert judgment more scalable, not replace it.

A payment risk analyst who can investigate 50 cases per day with AI assistance is more valuable than an AI system that handles 200 cases autonomously but gets 5% wrong with no recourse.

Financial services is a domain where being wrong is expensive and trust is the product. AI that extends trust-building capabilities is valuable. AI that substitutes for them is risky.

Build accordingly.
