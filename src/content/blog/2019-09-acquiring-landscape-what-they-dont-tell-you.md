---
title: "The Acquiring Landscape: What They Don't Tell You"
description: "A frank breakdown of payment acquiring — interchange, scheme fees, merchant discount rates, and why the numbers rarely work out the way the sales deck says."
heroImage: '/images/blog/acquiring-landscape-01.jpg'
heroAlt: 'Payment processing infrastructure'
pubDate: 'Sep 18 2019'
---

I've sat in a lot of acquiring sales conversations. The pitch is always the same: competitive rates, seamless integration, fast settlement. What you get is usually more complicated.

Here's the honest breakdown of how payment acquiring actually works.

## The Fee Stack

When a card is charged, the merchant doesn't lose one fee — they lose a stack of them:

![Payment fee stack — interchange, scheme fees, and acquirer margin all come out before the merchant sees a cent](/images/blog/2019-09-acquiring-landscape-what-they-dont-tell-you-inline-01.jpg)
*Every card transaction carries multiple layers of fees — most merchants only see the final MDR.*

**Interchange**: Paid to the card-issuing bank. This is the largest fee and it's non-negotiable. It varies by card type (credit vs debit), card tier (standard vs premium), transaction type (card-present vs card-not-present), and region. A premium Visa Infinite card used for an e-commerce transaction in Southeast Asia has a dramatically different interchange rate than a debit card tapped at a point of sale in Europe.

**Scheme fees**: Paid to Visa or Mastercard. These have multiplied over the years — authorization fees, cross-border fees, data integrity fees, network access fees. Schemes publish their fee schedules publicly but they're hundreds of pages long and change twice a year.

**Acquirer margin**: What the acquirer keeps. In a blended rate pricing model (common for SMBs), this is bundled into a single MDR (Merchant Discount Rate). In interchange-plus pricing (better for volume merchants), you see the components separately.

For a typical international e-commerce transaction, you might see:
- Interchange: 1.5-1.8%
- Scheme fees: 0.15-0.3%
- Acquirer margin: 0.3-0.8%
- Total MDR: 2.0-2.9%

Those numbers shift significantly depending on your volume, your risk profile, your vertical, and your geographic mix.

## Cross-Border Complexity

Cross-border transactions add layers. When the cardholder's bank and the acquirer are in different countries, you have:

> A merchant at **2.0% MDR with 95% approval rates** has better unit economics than one at **1.7% MDR with 88% approval rates**. Approval rate is the metric that actually matters — run the numbers before you sign.

**Currency conversion**: If you settle in USD but your merchant is in Singapore and the cardholder's card is in EUR, there's an FX rate somewhere in that chain. Who takes the FX risk and when matters enormously for your unit economics.

**Cross-border interchange**: Higher. Often 0.4-0.8% on top of domestic rates.

**Scheme cross-border fees**: Yes, separate from interchange. Visa and Mastercard both charge additional fees for cross-border authorization and settlement.

**Compliance jurisdiction complexity**: Which country's rules apply? The acquirer's? The merchant's? The cardholder's bank's? Usually the acquirer's country governs the acquiring relationship, but exceptions exist for sanctions screening, data localization, and consumer protection rules.

## Approval Rates Are Everything

Every declined transaction is lost revenue. The reasons for declines fall into a few buckets:

**Issuer declines**: The cardholder's bank said no. Insufficient funds, fraud suspicion, card expired. You can't do much about these, but you can build retry logic for soft declines.

**Technical declines**: Timeout, network error, processing failure. Should be rare but they happen. Retry logic helps here too.

**Acquirer declines**: Your acquirer's fraud rules triggered. This is where working closely with your acquirer to tune rules for your merchant's transaction profile makes a real difference.

![Decline waterfall — understanding which declines are recoverable vs permanent changes your authorization strategy](/images/blog/2019-09-acquiring-landscape-what-they-dont-tell-you-inline-02.jpg)
*Soft declines are recoverable with smart retry logic. Hard declines are permanent. Knowing the difference saves revenue.*

## What to Actually Optimize For

When evaluating acquirers, in rough priority order:

1. **Approval rate** — across your specific card mix and geographies
2. **Settlement speed** — T+1 vs T+3 matters for cash flow
3. **Risk tolerance for your vertical** — some acquirers won't touch certain industries
4. **Support quality** — when disputes happen, you want a real person who knows your account
5. **Pricing** — yes, last. It matters, but it's one variable in a complex system.

The best acquirer relationship is one where you're treated as a partner, not a revenue line. Find that, and optimize everything else around it.
