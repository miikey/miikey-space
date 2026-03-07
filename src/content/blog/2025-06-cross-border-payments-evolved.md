---
title: 'Cross-Border Payments in 2025: What Actually Changed'
description: 'Six years after writing about why cross-border payments are broken, here is an honest assessment of what has improved, what has not, and where the next inflection points are.'
heroImage: 'https://images.unsplash.com/photo-1601597111158-2fceff292cdc?w=1200&h=630&fit=crop&auto=format'
heroAlt: 'Cross-border payments evolution'
pubDate: 'Jun 10 2025'
---

In January 2019, I wrote that cross-border payments were fundamentally broken — slow, expensive, and architecturally outdated. Six years later, it's worth revisiting with an honest assessment.

## What Actually Improved

**Stablecoin settlement corridors are real.** This was the thesis I laid out in 2019 and it's played out. USDC and USDT are handling meaningful B2B settlement volume across specific corridors — particularly US-LatAm, US-Southeast Asia, and intra-Asia. The settlement time has gone from T+2-5 to minutes. The FX transparency has improved dramatically. It's not universal, but it's no longer experimental.

**Local payment rail aggregation matured.** The fragmentation of local payment methods — GrabPay, GCash, Pix, UPI, PromptPay — used to be a pain point for cross-border merchants. The infrastructure for aggregating these rails through a single API has matured. Merchants can accept payments from consumers using their preferred local method, regardless of geography.

**Regulatory frameworks caught up.** MiCA, Singapore's PS Act amendments, Hong Kong's stablecoin framework — the regulatory infrastructure for new payment rails now exists in most major financial centers. This was the missing piece in 2019. Without it, enterprise adoption was impossible.

## What Didn't Change Enough

**Correspondent banking still dominates.** For large-value B2B payments between traditional banking counterparties, the correspondent banking model is largely unchanged. SWIFT gpi improved visibility but didn't change the fundamental architecture. Banks still route through correspondent chains for most international wires.

**Consumer remittance costs are still too high.** The global average cost of sending $200 has dropped from ~7% to ~5% since 2019, according to World Bank data. That's progress, but it's slower than hoped. The corridors where stablecoin-based remittance is active have seen much larger drops. The corridors where it isn't — often the ones that need it most — haven't moved much.

**Compliance fragmentation.** Every jurisdiction has its own KYC requirements, sanctions lists, reporting obligations, and data localization rules. The compliance cost of operating cross-border payment infrastructure across multiple jurisdictions has actually increased, not decreased. This is the unsexy but critical infrastructure problem.

## The Architecture That's Emerging

The payment infrastructure that's working best in 2025 has a few common architectural characteristics:

**Multi-rail by default.** Rather than committing to a single settlement rail, successful infrastructure supports multiple: traditional banking rails for large-value regulated flows, stablecoin rails for speed-optimized corridors, local payment rails for consumer-facing payments. The routing intelligence — which rail to use, for which transaction, in which corridor — is where the product differentiation is.

**Compliance as a service layer.** Rather than each participant building compliance infrastructure independently, compliance capabilities (KYC verification, sanctions screening, transaction monitoring) are being consumed as modular services. This reduces duplication and allows specialization.

**Real-time FX management.** The ability to lock, quote, and execute FX in real-time — rather than relying on batched end-of-day rates — is table stakes. Whether the underlying asset is fiat or stablecoin, the FX management layer makes or breaks the unit economics.

## What I'm Working On Now

The current focus of my work is on the routing intelligence layer — dynamically selecting the optimal payment rail for each transaction based on corridor, amount, speed requirement, cost, and compliance constraints. This is the problem that gets harder as you support more rails and more corridors, and it's where AI-driven optimization is starting to show real value.

The cross-border payment problem isn't solved. But it's more tractable than it was in 2019. The rails exist. The regulation exists. The remaining work is optimization, coverage, and reliability.

That's infrastructure work. It's what we do.
