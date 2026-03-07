---
title: 'ClearChain'
description: 'Blockchain settlement layer for cross-border payment networks. Reduces FX settlement from T+2 to near real-time using a multi-chain liquidity mesh.'
tag: 'Protocol'
status: 'Building'
year: '2023–present'
---

Cross-border payment settlement is architecturally broken. The correspondent banking model routes value through chains of intermediary banks, each holding nostro accounts in foreign currencies, each adding latency and cost. For a payment from Singapore to Brazil, value might touch 4-5 banks before arriving — taking 2-5 business days and costing 2-4% in aggregate fees.

ClearChain is an on-chain settlement layer designed to replace the correspondent banking leg of cross-border settlement for payment networks, fintechs, and banks.

## The Core Mechanism

Rather than routing through correspondent banks, participating institutions pre-fund liquidity positions in a smart contract-based settlement pool. When a payment is initiated:

1. The sending institution's liquidity position is debited in the origin currency
2. The receiving institution's position is credited in the destination currency
3. FX conversion happens atomically using on-chain liquidity pools
4. Settlement is final in ~10 seconds

The net effect: T+2 becomes T+0. The 2-4% correspondent fee becomes a 0.1-0.3% liquidity fee. The settlement is transparent and auditable by both parties.

## Technical Architecture

**Multi-chain liquidity mesh** — liquidity pools exist on multiple EVM chains (currently Ethereum, Base, Polygon). Cross-chain liquidity is bridged using a trust-minimized bridge with optimistic security assumptions and a 30-minute fraud proof window for large transfers.

**USDC as the settlement asset** — all settlement flows through USDC, eliminating intra-settlement FX risk. FX conversion happens at the edges (local currency → USDC on the sending side, USDC → local currency on the receiving side).

**Compliance layer** — on-chain compliance checks run before settlement authorization. Sanctions screening, transaction limits, and counterparty whitelisting are enforced at the contract level.

**Permissioned participant model** — institutions must be KYB-verified and approved to participate. Not a public DeFi protocol — a permissioned network with institutional participants.

## Status

Currently in private beta with three payment network participants across two corridors (US-Philippines, Singapore-Indonesia). Processing a growing share of our cross-corridor settlement volume.
