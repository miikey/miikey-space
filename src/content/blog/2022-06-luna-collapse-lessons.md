---
title: 'When Algorithms Fail: Lessons from LUNA'
description: 'The Terra/LUNA collapse erased $40 billion in value in 72 hours. As someone who had tracked algorithmic stablecoins closely, here is what I think we should learn from it.'
heroImage: 'https://images.unsplash.com/photo-1611974789855-9c2a0a7236a3?w=1200&h=630&fit=crop&auto=format'
heroAlt: 'Market chart crash'
pubDate: 'Jun 08 2022'
---

In May 2022, TerraUSD (UST) — the algorithmic stablecoin backed by LUNA — lost its peg and then collapsed entirely. In roughly 72 hours, approximately $40 billion in market value was erased. LUNA went from $80 to fractions of a cent.

I had been tracking algorithmic stablecoin designs closely since 2020. I want to write honestly about what happened, what I got right in my skepticism, and what I got wrong in underestimating the scale of the potential failure.

## What Happened

UST maintained its dollar peg through an algorithmic relationship with LUNA. When UST traded below $1, you could burn UST to mint $1 worth of LUNA (at market price), creating buy pressure on UST and sell pressure on LUNA. When UST traded above $1, the reverse happened.

The system worked as long as demand for UST was growing. The Anchor Protocol — which offered 20% yield on UST deposits — was generating that demand artificially. 20% yield on a stablecoin is not a market rate. It's a subsidy. The question was always: what happens when the subsidy ends?

The answer: depositors leave. As Anchor yields were adjusted downward, UST demand weakened. Once UST started trading slightly below peg, the redemption mechanism triggered — users burned UST for LUNA. LUNA supply increased. LUNA price fell. The redemption ratio worsened. More LUNA was needed to back the same value of UST. Which created more sell pressure on LUNA. Which made everything worse.

This is a death spiral. The mechanism that was supposed to protect the peg instead accelerated the depeg.

## What I Got Right

I wrote in late 2020 that first-generation algorithmic stablecoins had a fundamental mechanism design problem: they relied on continuous demand growth to maintain stability. A stablecoin that only works in growth conditions isn't stable — it's procyclical.

The UST/LUNA design was more sophisticated than ESD or BASIS, but it shared the core vulnerability. The reflexive relationship between UST and LUNA meant that the stress test it couldn't survive was exactly the one that market conditions eventually imposed.

## What I Got Wrong

I underestimated how large the system would get before it failed, and therefore how catastrophic the failure would be. Algorithmic stablecoins failing isn't new. ESD, DSD, FRAX went through similar dynamics in 2021. They were smaller. They failed smaller.

UST at $18 billion circulating supply was a different scale. The contagion — to crypto funds holding LUNA, to protocols that had integrated UST, to market confidence broadly — was proportionally larger.

I also underestimated how many sophisticated investors had convinced themselves that the mechanism was sound. When the collapse happened, the shock was not just financial but psychological. Smart people had built large positions on a flawed premise.

## What the Payments Industry Should Take Away

For those of us thinking about stablecoins for payments and settlement (which I've written about since 2020), LUNA raises a question worth sitting with: which stablecoin designs are actually sound?

My updated view: the stablecoin designs with the best long-term survival prospects are:

**Fiat-backed**: USDC, USDT. Backed by actual dollars in bank accounts and T-bills. The risk is counterparty risk (the issuer), not mechanism design risk. More boring, more durable.

**Overcollateralized crypto-backed**: DAI. Backed by crypto assets worth more than the issued stablecoins. The mechanism has been stress-tested. It survives bear markets because the overcollateralization provides a buffer.

**Algorithmic**: Proceed with extreme caution. The mechanism design needs to be provably sound across adversarial conditions, not just normal market conditions. That's a much higher bar than most designs have cleared.

For payment infrastructure, I'm only comfortable building on fiat-backed stablecoins at this point. The settlement reliability guarantee needs to be unconditional.

The LUNA collapse was a $40 billion stress test of a mechanism design. The lesson is expensive. We should actually learn from it.
