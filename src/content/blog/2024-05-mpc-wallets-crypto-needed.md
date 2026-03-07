---
title: 'MPC Wallets: The Infrastructure Upgrade Crypto Needed'
description: 'Multi-Party Computation for key management is not a new idea, but it is finally practical at scale. Here is why MPC wallets matter and what the architecture looks like.'
heroImage: '/images/blog/mpc-wallets-01.jpg'
heroAlt: 'Crypto wallet security'
pubDate: 'May 07 2024'
---

For most of crypto's history, wallet security has been a binary problem: either you control your keys (self-custody, risky) or someone else controls them (custodial, counterparty risk). The FTX collapse in 2022 made the counterparty risk of custodial arrangements viscerally clear. But self-custody at scale — for businesses, for funds, for anyone managing material amounts of value — has operational problems that key management risk just doesn't solve.

MPC (Multi-Party Computation) wallets represent a genuine third path. After spending the last year building MPC-based key management infrastructure, I want to explain why this matters and how it works.

![Digital padlock on a glowing circuit board representing cryptographic security](/images/blog/2024-05-mpc-wallets-crypto-needed-inline-01.jpg)
*The binary choice between "hold your own keys" and "trust a custodian" defined crypto's first decade. MPC breaks that binary.*

## The Problem with Traditional Key Management

A private key is a large random number. Whoever possesses it can sign transactions from the associated wallet. The security model is simple: protect the key.

The problem: protecting a key at scale is hard. Hardware wallets work for individuals. For institutional operations — a payment company moving $50M/day across multiple chains, a fund managing complex position changes — the operational requirements are different:

- Multiple authorized signers should be required for large transactions (no single point of authorization failure)
- Key material should not exist as a complete key at any single point (no single point of compromise)
- Authorization policies should be programmable and auditable
- Recovery should be possible without central key escrow

Hardware HSMs (Hardware Security Modules) handle some of this, but they're expensive, physically constrained, and don't natively support threshold signing.

## How MPC Solves This

Multi-Party Computation enables a group of parties to jointly compute a function (in this case: a digital signature) without any party ever seeing the complete private key.

In threshold signature schemes (TSS), the private key is mathematically split into "key shares." A threshold number of shares (e.g., 3 of 5) must cooperate to produce a valid signature. No individual share can sign alone, and no individual share reveals the complete key.

> **No single key share can sign alone, and no single share reveals the complete key.** An attacker must compromise multiple independent infrastructure environments simultaneously — a fundamentally different (and much harder) attack vector than stealing one key from one place.

What's powerful about this:

**No single point of compromise.** Compromising one key share (one server, one device, one party) doesn't compromise the wallet. An attacker needs to compromise multiple shares simultaneously — a fundamentally different attack requirement.

**No single point of authorization.** Policies like "transactions over $1M require approval from 3 of 5 authorized parties" are enforced cryptographically, not just procedurally.

**Programmable authorization.** Spending limits, time locks, whitelist-only destinations — these can be enforced at the key management layer, before a transaction is ever broadcast.

**Auditable.** Every signing ceremony is logged: who participated, what was approved, when. Full audit trail without relying on internal accounting systems.

![Server room with rows of blinking equipment](/images/blog/2024-05-mpc-wallets-crypto-needed-inline-02.jpg)
*MPC key shares are distributed across independent infrastructure — different servers, different environments, different trust boundaries.*

## The Architecture We Built

Our implementation distributes key shares across three participants:
1. Our infrastructure (one share, always required)
2. The client's secure environment (one share)
3. A hardware-backed backup participant (one share, used for recovery)

Policy enforcement runs on our infrastructure before authorizing our share's participation in a signing ceremony. This means: even if an attacker fully compromises the client's environment, they can't move funds without also compromising our infrastructure (which has independent monitoring and rate limiting) or the backup (which has additional friction on access).

For transaction signing, latency is around 200-400ms in normal conditions — fast enough for payment operations.

## The Remaining Challenges

MPC wallet infrastructure is significantly better than alternatives, but it's not a silver bullet:

**Complexity.** The cryptographic protocols are complex and require careful implementation. TSS implementations have had vulnerabilities. Use libraries that have been extensively audited; don't implement the cryptography yourself.

**Operational complexity.** Managing key share distribution, backup procedures, and recovery protocols is operationally demanding. The human factors matter as much as the technical ones.

**Cross-chain support.** Different chains use different signature schemes (ECDSA, EdDSA, Schnorr). MPC implementations need to support each scheme separately. Cross-chain wallet management requires careful architecture.

![Engineer reviewing security audit logs on a screen](/images/blog/defi-fix.jpg)
*Every signing ceremony produces a full audit trail — who participated, what policy was enforced, when. Compliance built into the cryptography.*

Despite these challenges: for any organization managing material value in crypto assets, MPC-based key management is now the standard I'd recommend. The FTX era is over. The infrastructure for trustworthy custody exists. Use it.
