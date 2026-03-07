---
title: 'UQPAY'
description: 'Next-gen payment infrastructure for the borderless economy. Global acquiring, card issuing, and cross-border settlement.'
tag: 'Fintech'
status: 'Live'
year: '2018–present'
links:
  - label: 'uqpay.com'
    href: 'https://uqpay.com'
---

UQPAY is the company I co-founded to build payment infrastructure for businesses operating across borders. The core thesis: the existing stack for global payments — correspondent banking, fragmented local rails, opaque FX — is too slow, too expensive, and too opaque for the speed at which modern businesses operate.

## What We Built

**Global acquiring** — merchant payment acceptance across Southeast Asia, the Middle East, and Latin America, with a single integration. Supports 150+ local payment methods, including QR wallets, bank transfer schemes, and real-time payment networks.

**Card issuing** — programmable virtual and physical card issuance with real-time spend controls, multi-currency support, and webhook-driven authorization. Built for fintechs, platforms, and enterprises that need to embed cards in their products without becoming a bank.

**Cross-border settlement** — multi-rail settlement infrastructure supporting both traditional fiat corridors and stablecoin-based settlement for speed-critical or cost-sensitive routes. Supports USDC, USDT, and native currency settlement depending on corridor.

**FX management** — real-time FX quoting and execution with transparent markups and configurable hedging strategies.

## Technical Stack

The infrastructure is built around an event-driven architecture with a distributed processing core. Key design principles:

- **Idempotency by default** — every operation is idempotent with client-supplied keys. Payment infrastructure gets retried constantly; idempotency is non-negotiable.
- **Dual-write consistency** — financial ledger writes are synchronous and durable before any external state changes. Eventual consistency is not acceptable for money movement.
- **Multi-rail routing** — an intelligent routing layer selects acquirer, currency path, and settlement rail per transaction based on approval rate history, cost, speed requirements, and compliance constraints.

## Scale

Processing transactions across 30+ markets, supporting merchants from early-stage fintechs to large enterprises. Settlement infrastructure handles both sub-$100 consumer remittances and multi-million dollar B2B transfers.
