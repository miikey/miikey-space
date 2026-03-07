---
title: 'Threshold Signer'
description: 'MPC wallet infrastructure implementing threshold signature schemes for institutional-grade key management. No single point of key compromise.'
tag: 'MPC'
status: 'Building'
year: '2023–present'
---

The FTX collapse made one thing undeniable: custodial arrangements where a single entity controls private keys are a single point of failure — technical, operational, and moral. The industry needed a better model.

Threshold Signer is MPC-based key management infrastructure for payment companies and crypto-native institutions that need to hold significant digital asset value without creating single points of key compromise.

## How It Works

Multi-Party Computation (MPC) allows multiple parties to jointly compute a function — in this case, a digital signature — without any party ever possessing the complete private key.

Using a 2-of-3 threshold signature scheme (TSS):
- **Share 1**: Held by our secure infrastructure (HSM-backed)
- **Share 2**: Held by the client in their secure environment
- **Share 3**: Held by a hardware-backed backup participant (used for recovery)

A valid signature requires any 2 of 3 shares to cooperate. No single party can sign unilaterally. No single compromise reveals the key.

## Policy Enforcement

Authorization policies are enforced before our infrastructure participates in a signing ceremony:

- **Spend limits** — per-transaction and daily limits by asset and chain
- **Destination whitelisting** — only pre-approved addresses can receive funds above configurable thresholds
- **Time locks** — configurable delays for large transactions
- **Multi-approver** — transactions above threshold require explicit approval from multiple authorized individuals
- **Rate limiting** — velocity controls per time window

All policy changes are audited and require multi-person authorization.

## Technical Details

**Supported chains**: Ethereum and all EVM-compatible chains, Bitcoin (ECDSA), Solana (EdDSA). Signature scheme support is implemented independently per chain.

**Signing latency**: Median 180ms, p99 320ms for 2-of-3 signing ceremony. Acceptable for payment operations; not suitable for high-frequency trading use cases.

**Audit trail**: Every signing ceremony is logged with full context — who initiated, who approved, what was signed, what policy checks ran. Immutable audit log exportable for compliance.

**Recovery**: Share 3 (backup participant) is used for recovery scenarios. Recovery requires multi-factor authentication from the client plus verification from our team. No recovery without client authorization.

## Why This Matters

For a payment company moving $50M/day in stablecoins, the custody arrangement determines the blast radius of a breach. MPC custody means no single server compromise, no single insider threat, no single point of key exfiltration. The attacker must simultaneously compromise multiple independent systems operated by different parties.

That's a fundamentally different security posture than hot wallet custody.
