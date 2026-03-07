---
title: 'DeFi Summer Retrospective: What Survived'
description: 'DeFi Summer 2020 produced a thousand projects and a billion dollars of value locked. Twelve months later, here is an honest look at what actually survived and why.'
heroImage: '/images/blog/defi-summer-01.jpg'
heroAlt: 'Crypto DeFi charts'
pubDate: 'Feb 10 2021'
---

DeFi Summer 2020 — the few months when yield farming launched a thousand protocols and total value locked went from $1B to $15B in a matter of weeks — feels both recent and ancient.

Twelve months out, the signal is starting to separate from the noise. Here's my honest assessment of what survived and what the survival tells us.

## What Survived


> Of the **1000+ DeFi projects** launched in Summer 2020, fewer than 20 still have meaningful usage today. Bears filtered for real utility over speculative yield.

![DeFi blue chips — Aave, Uniswap and Curve still standing after hundreds of forks faded](/images/blog/2021-02-defi-summer-retrospective-inline-01.jpg)
*The protocols that survived DeFi Summer shared one trait: genuine utility beyond yield farming.*

**The lending primitives.** Aave and Compound are bigger now than they were at the peak of DeFi summer. The core mechanic — deposit collateral, borrow against it, earn yield as a lender — turns out to be genuinely useful. The TVL numbers have cycles but the underlying behavior has become a permanent part of how on-chain capital gets deployed.

**Automated market makers.** Uniswap v3 launched in May 2021 with concentrated liquidity — a meaningful technical improvement over the original constant-product formula. The AMM model has proven more durable than the order book alternatives. Liquidity provision is still inefficient for the LP, but the model keeps improving.

**Stablecoins.** USDC, DAI, USDT — stablecoin usage has grown significantly since DeFi summer, and not just in DeFi. The on/off ramp problem is slowly getting solved, and as it does, stablecoins are absorbing more real cross-border payment volume. This was the thesis I wrote about last year and it's playing out.

## What Didn't Survive

**Food farms and anonymous forks.** The vampire attack mechanics — fork a protocol, launch with higher yields, drain liquidity from the original — created enormous token prices that collapsed just as quickly. SushiSwap survived because the community was able to build a real team around it. Most didn't.

**Algorithmic stablecoins (first generation).** The ESD/BASIS/DSD crop of algorithmic stablecoins from late 2020 all went to zero or near-zero. The mechanism design was flawed in ways that weren't obvious until stress-tested. This is a lesson about the difference between "works in a bull market" and "works."

**Protocol governance tokens as yield.** The governance token farming model — earn tokens for providing liquidity — created powerful bootstrapping mechanics but terrible long-term token economics. Tokens distributed at scale to yield farmers who immediately sell them don't build communities.

## BSC and the Multi-Chain Reality

Something I didn't fully anticipate: the rise of BNB Chain (BSC) as a DeFi platform. While Ethereum L1 gas fees made DeFi inaccessible for smaller capital deployments, BSC offered Ethereum compatibility at a fraction of the cost.

PancakeSwap, Venus, and the BSC DeFi ecosystem that emerged in early 2021 brought a new user cohort into DeFi — users who couldn't afford $50-100 gas fees but could operate at $0.10-1. The tradeoffs (centralization, lower security guarantees) were real, but so was the accessibility.

I spent time tracking the BSC ecosystem closely, contributing to the Defistation analytics dashboard. The user numbers were real. The capital was often smaller than Ethereum DeFi, but the breadth of participation was wider.

## What This Tells Us About Infrastructure Cycles

DeFi summer followed a pattern I've seen in other infrastructure cycles: a speculative mania on top of real underlying primitives, followed by a crash that destroys the speculation while leaving the primitives intact and strengthened.

The difference between DeFi 2020 and the ICO boom of 2017 is that DeFi summer's survivors left behind working code, not just whitepapers. Aave's smart contracts work. Uniswap's liquidity pools work. The code is the infrastructure, and it kept running through the mania and the crash.

The next wave — L2 scaling, better oracle design, cross-chain interoperability — is being built on top of these proven primitives. That's how compounding infrastructure progress works.
