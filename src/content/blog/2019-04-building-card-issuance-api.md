---
title: 'Building a Card Issuance API: What Nobody Tells You'
description: 'Card issuance sounds straightforward until you actually try to build it. Here is what six months of BIN sponsorship negotiations, EMV certification, and scheme compliance actually looks like.'
heroImage: '/images/blog/card-issuance-api-01.jpg'
heroAlt: 'Credit card payment terminal'
pubDate: 'Apr 03 2019'
---

Six months ago we started building a card issuance API. I thought it would take eight weeks. Here's what actually happened.

## The BIN Sponsorship Problem

Before you can issue a single card, you need a BIN (Bank Identification Number) — the first 6-8 digits that identify the card and route authorization requests. BINs are owned by banks. To issue cards, you either need to be a bank (you're not) or find a bank willing to sponsor your BIN and take on the regulatory liability.

![BIN sponsorship chain — the regulatory structure behind every card you've ever issued](/images/blog/2019-04-building-card-issuance-api-inline-01.jpg)
*Behind every card product: a bank sponsor, a scheme agreement, and a compliance stack most engineers never see.*

This is where the process stalls for most fintech companies.

> BIN sponsorship negotiation cycles run **3-6 months on average**. If you start when you think you're six weeks from launch, you will miss your launch by at least a quarter.

The BIN sponsor relationship is a principal-agent arrangement. The bank is the principal — they're the licensed issuer on record. You're the agent — you manage the customer relationship and take the fraud risk (sort of). The fee structures are opaque, the negotiation cycles are long, and the requirements vary wildly by geography.

Things nobody tells you upfront:
- Some sponsors require minimum monthly transaction volumes you can't hit on day one
- Indemnity clauses can leave you on the hook for chargeback losses beyond any reasonable cap
- "Real-time authorization" from the sponsor's side often means 200-400ms round trip which is fine, until it's not
- EMV certification has to happen separately from scheme certification — they're different processes

## EMV Certification Hell

EMV (the chip standard) certification isn't a one-time thing. It's per card product, per card variant (physical vs virtual), per scheme (Visa, Mastercard), per country. Each certification is a formal testing process with the card schemes.

We used a third-party HSM (Hardware Security Module) provider for key management — generating and storing the keys that make chip cards cryptographically unique. That part actually went smoothly. The certification testing itself was the issue.

The test suites are hundreds of test cases. You fail test case 47? Start over. The schemes don't publish all the failure criteria upfront. You discover them by failing.

We burned six weeks on Mastercard M/Chip certification alone.

## The Authorization Flow

Once you're live, the technical architecture looks something like this:

```
Merchant POS → Acquirer → Card Network → Your BIN Sponsor → Your Authorization API
```

Your API has somewhere between 150-300ms to respond with an Approve or Decline. In that window, you need to:

1. Identify the cardholder
2. Check available balance / credit limit
3. Apply your fraud rules
4. Check for spend controls (if any)
5. Return an ISO 8583 formatted response

![ISO 8583 message routing — the 1987 protocol that still powers every card authorization on earth](/images/blog/2019-04-building-card-issuance-api-inline-02.jpg)
*ISO 8583. Binary, bitmap-indexed, born in 1987. You will learn to love it.*

ISO 8583 is the message format the card networks use. It's a beautiful relic of 1987. Binary, field-based, with a bitmap indicating which fields are present. You will write a lot of code to handle edge cases in how different processors implement it.

## What We Got Right

**Webhook-first design.** Every authorization event, settlement notification, and card state change is delivered as a webhook. Our customers can build real-time card controls without polling. This decision has saved us enormous support headaches.

**Idempotency everywhere.** Card issuance APIs get retried constantly — by customers, by their customers, by broken webhooks. Every endpoint accepts an idempotency key. This sounds obvious but is somehow missing from several major competitors' APIs.

**Sandbox that mirrors production.** Our sandbox uses the same authorization flow as production, with simulated network responses. Test card numbers that trigger specific decline codes. Merchants can actually test edge cases before going live.

## What We'd Do Differently

Start the BIN sponsorship negotiation on day one, not when you think you're six weeks from launch. And hire someone who has actually done scheme certification before — the institutional knowledge is not in any documentation, it's in people's heads.

> Card issuance is fundamentally a **regulatory and compliance business** that happens to have an API. The technology is the easy part. Build accordingly.
