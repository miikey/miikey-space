---
title: 'RiskGuard'
description: 'AI-powered fraud detection and real-time risk scoring for card acquiring pipelines. Combines ML anomaly detection with rule-based decisioning.'
tag: 'AI · Risk'
status: 'Building'
year: '2023–present'
---

Payment fraud is an arms race. Rule-based systems catch known fraud patterns — and fraudsters adapt. The velocity of new fraud techniques has outpaced the velocity of rule updates for most acquiring operations.

RiskGuard is a risk decisioning engine built for card acquiring that combines ML-based anomaly detection with interpretable rule-based decisioning, designed to run in the authorization path with sub-50ms latency requirements.

## The Problem with Pure ML

ML models are excellent at detecting anomalies. They're poor at explaining decisions — which creates two problems in payment risk:

**Regulatory explainability.** In many markets, adverse action decisions (declining a transaction) require an explainable reason. "The model said so" isn't compliant.

**Operator trust and tuning.** Risk teams need to understand why transactions are being declined to tune thresholds, investigate patterns, and respond to merchant escalations. Black-box decisions make this impossible.

RiskGuard uses ML for what it's good at (anomaly scoring, pattern detection across high-dimensional feature space) and rule-based logic for what requires explainability (final decisioning with auditable reason codes).

## Architecture

**Feature pipeline** — real-time feature computation from transaction data, merchant history, cardholder behavior (where available), device signals, and network-level features. Feature computation runs in <5ms.

**ML scoring layer** — an ensemble of gradient boosting and neural network models producing a fraud probability score. Models are retrained weekly on labeled data. Separate models for card-present, card-not-present, and cross-border transaction types.

**Rule engine** — a configurable rule layer that takes the ML score as an input along with other signals and produces an approve/decline/review decision with reason codes. Rules are version-controlled and changes go through approval workflows.

**Feedback loop** — chargebacks, disputes, and manual review outcomes feed back into model training. The system improves continuously from its own decisions.

## Results

On our acquiring volume:
- **3x improvement** in true fraud detection rate versus the previous rule-only system
- **40% reduction** in false positive rate (legitimate transactions declined)
- Authorization latency impact: median +12ms, p99 +38ms
- Full audit trail for every decision, exportable for regulatory review
