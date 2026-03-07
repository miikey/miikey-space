---
title: 'DeFi: My First Six Months Down the Rabbit Hole'
description: 'I spent six months going deep on Aave, Compound, Uniswap, and Yearn. Here is what I actually learned about the infrastructure, the risks, and why I think this matters for payments.'
heroImage: 'https://images.unsplash.com/photo-1639762681485-074b7f938ba0?w=1200&h=630&fit=crop&auto=format'
heroAlt: 'DeFi blockchain network'
pubDate: 'Sep 07 2020'
---

In early 2020, a colleague sent me the Compound whitepaper. By September I'd deployed more capital to DeFi protocols than I care to admit, contributed code to two open source protocol frontends, and completely restructured how I think about financial infrastructure.

Here's what six months of hands-on DeFi actually taught me.

![DeFi liquidity pools and protocol dashboards on multiple screens](https://images.unsplash.com/photo-1551288049-bebda4e38f71?w=1000&h=480&fit=crop&auto=format)
*The DeFi dashboard view — tracking positions across Aave, Compound, and Yearn simultaneously*

## The Infrastructure Is Real

Before going deep, I was skeptical of DeFi as a payments person. I'd seen too many blockchain-for-payments pitches that ignored the actual user experience problems: wallet management, gas fees, transaction finality times, on/off ramps. The gap between the whitepaper and the product was always enormous.

The DeFi protocols I spent time with — Aave, Compound, Uniswap v2, Yearn — were different. They weren't pitching payments. They were quietly building financial infrastructure that actually worked.

What impressed me most wasn't the yields (which I took with healthy skepticism). It was the composability. The way Yearn could programmatically move capital between Aave and Compound to optimize yields, triggered by anyone, settled on-chain with no counterparty required — that's a genuinely new primitive. In traditional finance, building that kind of automated multi-party capital allocation requires legal agreements, custodial relationships, and months of integration work. Here it's a smart contract call.

> In TradFi, multi-party capital allocation requires **months of legal agreements and custodial relationships**. In DeFi, it's a single smart contract call — triggered by anyone, settled on-chain, no counterparty required.

## What I Got Wrong

I underestimated smart contract risk. Not in an abstract way — I knew it was real — but I didn't internalize it correctly. The bZx flash loan attacks in February 2020 happened before I went deep into the space. By September I'd seen enough protocol exploits and economic attacks to understand that "audited" doesn't mean "safe."

The risk model for DeFi is fundamentally different from traditional finance. In TradFi, operational risk is counterparty risk — you're trusting institutions. In DeFi, it's code risk — you're trusting math and implementation. Code risk is in some ways more legible (the code is public, auditable), but it's also harder for most people to evaluate.

I also underestimated the oracle problem. Price oracles — the mechanisms that bring off-chain price data on-chain — are a critical attack surface that I hadn't fully appreciated until I saw several oracle manipulation attacks up close.

![Close-up of code on a dark screen showing smart contract logic](https://images.unsplash.com/photo-1555066931-4365d14bab8c?w=1000&h=480&fit=crop&auto=format)
*"Audited" doesn't mean "safe" — code risk is more legible than counterparty risk, but harder for most people to evaluate*

## The Payments Intersection

The reason I went deep on DeFi wasn't speculation — it was curiosity about whether the infrastructure could solve problems I'd been wrestling with in payments.

Specifically: stablecoin settlement. Using USDC or DAI as a settlement asset between payment corridors solves a real problem. You eliminate FX risk during settlement, enable 24/7 settlement (vs traditional T+2 during banking hours), and make the settlement transparent and auditable by both parties.

The on/off ramp problem is still the bottleneck. Getting money from a bank account into a stablecoin (and back) still requires touching the traditional financial system, with all its friction. But the settlement layer in between? That part can be genuinely better on-chain.

I built a proof-of-concept for this during those six months. Two counterparties in different countries, settling a cross-border transaction in USDC via a smart contract with agreed-upon conditions. The settlement itself — from "conditions met" to "funds available" — took 15 seconds. No correspondent banks. No FX spread. No T+2.

![Global wire transfer and digital payment flows visualized](https://images.unsplash.com/photo-1563986768609-322da13575f2?w=1000&h=480&fit=crop&auto=format)
*Two counterparties, two countries, USDC settlement in 15 seconds — no correspondent banks, no FX spread, no T+2*

## What Comes Next

DeFi in its current form is not for mainstream users. The UX is too hard, the risks are too opaque, the on-ramp friction is too high. But the infrastructure primitives — on-chain settlement, programmatic liquidity, composable financial operations — those are real and they're getting more robust.

The payment infrastructure of 2025 probably uses a lot of DeFi primitives that people never see. Just like most people don't know that their bank uses SWIFT when they send an international wire.

The plumbing changes. The user experience stays familiar. That's how infrastructure shifts happen.
