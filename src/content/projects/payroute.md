---
title: 'PayRoute'
description: 'Intelligent payment routing engine — dynamically selects acquirer, currency path, and fallback rails to optimize approval rate and cost per transaction.'
tag: 'Routing'
status: 'Building'
year: '2022–present'
---

Every payment that enters our infrastructure faces a routing decision: which acquirer, which currency path, which settlement rail, and what to do if the primary route fails. At scale, these decisions have material impact on approval rates, processing cost, and merchant revenue.

PayRoute is the routing intelligence layer — a system that makes per-transaction routing decisions based on real-time signals and historical performance data.

## Why Routing Matters

A merchant at 2.0% MDR with 95% approval rate has better unit economics than a merchant at 1.7% MDR with 88% approval rate. The math is straightforward: each declined transaction is lost revenue.

Approval rates vary by acquirer, card type, geography, transaction amount, and time of day in ways that aren't fully predictable. A routing engine that learns from historical performance and adjusts in real-time can meaningfully outperform static routing configurations.

## How It Works

**Feature extraction** — for each transaction, a feature vector is computed: card BIN metadata, merchant category, transaction amount and currency, geographic signals, time features, and recent performance metrics for candidate routing paths.

**Route scoring** — candidate routes are scored on expected approval probability and expected cost. Scores are computed using models trained on historical outcome data.

**Route selection** — the highest-scoring route that satisfies the merchant's configured constraints (max cost, min approval rate, settlement speed) is selected.

**Fallback logic** — if the primary route declines, a fallback waterfall is executed in real-time. Secondary and tertiary routes are pre-computed at routing time to minimize fallback latency.

**Outcome feedback** — every routing decision and its outcome (approved, declined, timed out) feeds back into the model. Models are updated continuously.

## Results

- **+2.3 percentage points** improvement in overall approval rate versus static routing
- **-0.18%** reduction in average processing cost through cost-aware routing
- Routing decision latency: median 8ms, p99 22ms
- Fallback handling: 94% of declined primaries recover on first fallback
