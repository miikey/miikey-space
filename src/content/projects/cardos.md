---
title: 'CardOS'
description: 'Programmable card issuance platform. Handles BIN sponsorship, card lifecycle management, and real-time authorization controls via webhook.'
tag: 'Issuing'
status: 'Building'
year: '2022–present'
---

Most businesses that want to issue cards face the same obstacle: the infrastructure required is deep, complex, and gated behind bank relationships that take months to establish. CardOS exists to collapse that timeline.

CardOS is a card issuance platform that handles the regulatory, certification, and infrastructure complexity of card programs — exposing a clean API for businesses that want to embed card issuance in their products.

## What CardOS Handles

**BIN sponsorship** — we maintain BIN sponsorship relationships with licensed issuing banks across multiple regions. Customers access these through our platform, without needing to negotiate their own bank relationships.

**Card lifecycle** — virtual and physical card issuance, card activation, PIN management, card blocking and replacement, and card termination. Full lifecycle management via API.

**Real-time authorization** — every card transaction calls a customer-configured webhook before authorization is approved or declined. Customers can implement custom spend controls, real-time balance checks, merchant category restrictions, and any other business logic in their own systems.

**Multi-currency support** — cards can be funded in multiple currencies with configurable FX handling at authorization time.

**Spend controls** — configurable limits by transaction amount, daily/monthly aggregate, merchant category code, and geography. Controls can be updated in real-time via API.

## The Authorization Flow

```
Merchant POS → Card Network → BIN Sponsor → CardOS
                                                ↓
                                    Customer Webhook (50ms budget)
                                                ↓
                                    CardOS → BIN Sponsor → Approved/Declined
```

The customer webhook receives the full authorization context and returns an approve/decline decision with optional metadata. This happens within the card network's authorization window — customers have approximately 50ms to respond.

## Use Cases

**Corporate expense cards** — companies issue cards to employees with spend controls enforced in real-time. Expenses are captured and categorized automatically at authorization.

**Virtual cards for AP automation** — single-use or multi-use virtual cards for accounts payable, with per-card spend limits and merchant restrictions.

**Consumer fintech** — consumer-facing applications that want to offer card products without becoming card issuers themselves.

**Platform monetization** — platforms that want to offer financial products to their users as a distribution channel.
