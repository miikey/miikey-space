---
title: 'Why Cross-Border Payments Are Still Broken in 2019'
description: 'Swift was built in 1973. We landed on the moon in 1969. Yet moving $100 across borders still takes 3-5 days and costs 6%. Something is fundamentally wrong.'
heroImage: '/images/blog/cross-border-payments-01.jpg'
heroAlt: 'Global payment network'
pubDate: 'Jan 14 2019'
---

Swift was built in 1973. We landed on the moon in 1969. Yet moving $100 across borders still takes 3-5 days and costs an average of 6% in fees. Something is fundamentally wrong with how we've accepted this as normal.

I've spent the last two years in the weeds of payment infrastructure — building acquiring pipelines, negotiating with card networks, watching FX spreads eat into every transaction. And the more I see, the more convinced I am that the core problem isn't technical. It's structural.

## The Correspondent Banking Problem

When you wire money internationally, your bank doesn't have a direct relationship with the recipient's bank. Instead, your money hops through a chain of correspondent banks — sometimes 3, sometimes 5 — each taking a cut and adding latency. It's like routing an email through five different servers, except each server charges you a fee.

![Correspondent banking chain — money hops through multiple intermediaries before reaching the recipient](/images/blog/2019-01-why-cross-border-payments-are-broken-inline-01.jpg)
*The correspondent banking chain. Every hop = fees + latency.*

SWIFT's GPI initiative has improved tracking visibility, but the fundamental architecture remains the same. You can now watch your money sit in each bank's nostro account. Great. But it's still sitting.

> The average cost of sending $200 internationally is **6.3%** — that's $12.60 gone before the recipient sees a cent. For migrant workers sending remittances home, this isn't a rounding error. It's a month of groceries.

## Acquirer Limitations in Emerging Markets

We've been building payment rails for Southeast Asia and the problems are even more acute here. Traditional acquiring in markets like Indonesia, Vietnam, Thailand — you're dealing with:

- High domestic interchange rates (often 1.5-2% vs 0.2% in Europe)
- Limited multi-currency settlement options
- T+3 to T+5 settlement cycles
- Compliance requirements that change with little notice

![Southeast Asia payment landscape — fragmented local rails across multiple markets](/images/blog/2019-01-why-cross-border-payments-are-broken-inline-02.jpg)
*Local payment methods dominate Southeast Asia — GrabPay, GCash, OVO, PromptPay — but no unified rail.*

The businesses that suffer most are the ones moving money for people who most need it — migrant workers sending remittances home, small exporters getting paid by international buyers, freelancers working for global clients.

## What's Actually Changing

A few things give me genuine optimism:

**Stablecoins for settlement rails.** Not consumer payments — settlement. Using USDC or USDT as a bridge asset between corridors makes mathematical sense. No FX risk during settlement, near-instant finality, programmable compliance. The trust problem is real, but it's solvable at the infrastructure level.

**Local payment method aggregation.** GrabPay, GCash, OVO, PromptPay — the real payment method innovation is happening at the local level. The infrastructure play is aggregating these rails and exposing them through a single API. That's what we're building.

**Regulatory sandboxes.** MAS in Singapore, OJK in Indonesia — regulators in Southeast Asia are actually moving faster than their Western counterparts on enabling fintech innovation. The sandbox model is working.

## The Uncomfortable Truth

The biggest barrier to fixing cross-border payments isn't technology. It's the fact that banks make enormous margins on FX and correspondent fees. The incumbents have little incentive to disrupt themselves.

Which is why I think the disruption will come from the edges — from fintech infrastructure companies quietly building better rails underneath the existing system, from stablecoins that make FX a software problem, from local payment networks that bypass correspondent banking entirely for regional corridors.

We're in the early innings. But for the first time in decades, I think the architecture is actually going to change.
