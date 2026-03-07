---
title: 'LiquidBridge'
description: 'Cross-chain liquidity bridge for stablecoin settlements across EVM and non-EVM chains. Powers real-time FX for UQPAY remittance corridors.'
tag: 'DeFi'
status: 'Building'
year: '2024–present'
---

Cross-chain interoperability is one of the unsolved problems of crypto infrastructure. When settlement needs to happen between two parties on different chains, the options are limited: use a centralized bridge (counterparty risk), use a slow optimistic bridge (latency), or pre-fund liquidity on both chains (capital inefficiency).

LiquidBridge is a cross-chain liquidity protocol designed specifically for payment and settlement use cases — optimizing for low latency and capital efficiency over maximum decentralization.

## Design Principles

**Payment-optimized, not DeFi-optimized.** Most bridge designs optimize for general asset transfer. LiquidBridge optimizes for the specific requirements of payment settlement: sub-minute finality, predictable cost, high reliability, and compliance-ready.

**Liquidity mesh, not lock-and-mint.** Rather than locking assets on one chain and minting wrapped versions on another, LiquidBridge uses a network of pre-funded liquidity positions on each supported chain. Transfers are fulfilled by liquidity providers on the destination chain, with settlement on the source chain handled asynchronously.

**USDC as the canonical asset.** All cross-chain liquidity is denominated in USDC. This eliminates the wrapped asset complexity and aligns with how institutional settlement is denominated.

## Architecture

**Liquidity pools** — USDC liquidity pools on each supported chain (Ethereum, Base, Polygon, Arbitrum, Solana). Liquidity providers earn fees from settlement flow.

**Fulfillment network** — a network of fulfillment nodes that monitor for transfer intents and fulfill them on the destination chain. Fulfillment is competitive — the first node to fulfill a transfer earns the fee.

**Intent-based transfers** — rather than atomic cross-chain transactions (which require complex synchronization), LiquidBridge uses an intent model: a transfer intent is published on the source chain, a fulfillment node executes on the destination chain, and settlement is verified and finalized.

**Finality**: Median 45 seconds end-to-end for cross-chain USDC settlement. Suitable for payment settlement use cases; not suitable for trading.

## Current Usage

Powering cross-chain settlement for specific UQPAY corridors where different chains offer optimal liquidity or cost. Live on Ethereum, Base, and Polygon. Solana support in development.
