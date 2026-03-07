---
title: 'FTX and What It Means for Crypto Infrastructure'
description: 'The FTX collapse is the largest exchange failure in crypto history. But the lesson is not that crypto is broken. It is that custody and infrastructure design matter more than most people realized.'
heroImage: 'https://images.unsplash.com/photo-1518546305927-5a555bb7020d?w=1200&h=630&fit=crop&auto=format'
heroAlt: 'Crypto infrastructure'
pubDate: 'Nov 16 2022'
---

FTX filed for bankruptcy on November 11, 2022. The collapse — from apparent solvency to bankruptcy in roughly 72 hours — is the largest exchange failure in the history of the crypto industry. Somewhere between $8-10 billion in customer funds is missing.

I want to write about what this means for the infrastructure we're building and what comes next.

## What Actually Failed

FTX failed because of the oldest failure mode in financial history: an institution using customer deposits as its own capital. Allegedly, FTX was lending customer funds to Alameda Research — its affiliated trading firm — which used them for illiquid investments and to cover losses. When confidence collapsed and customers tried to withdraw, there wasn't enough money.

This is not a crypto failure. It's a custodial failure. The same failure mode took down MF Global in 2011, caused the Savings and Loan crisis in the 1980s, and has recurred throughout financial history whenever customer assets are commingled with institutional assets and oversight is inadequate.

The crypto-specific element is the speed. Traditional financial institutions have regulatory oversight, reserve requirements, and stress testing designed to catch this before it explodes. FTX operated in a regulatory grey zone with inadequate oversight, so when confidence broke, it broke completely in days rather than months.

## What It Means for the Industry

**Proof of reserves becomes table stakes.** The ability for an exchange to prove — cryptographically, on-chain — that customer deposits are fully backed will become a minimum expectation. Merkle tree proof-of-reserves was already a known technique. Expect adoption to accelerate dramatically.

**Regulatory clarity is now inevitable.** The industry's preference for operating in regulatory grey zones has been invalidated. Customer protection requires regulatory structure. The question now is what form that regulation takes and who shapes it. Operators who engage constructively in that process will be better positioned than those who resist it.

**Self-custody and non-custodial infrastructure get a rethink.** The pitch for holding your own keys — "not your keys, not your coins" — has never been more vindicated. But most users don't want to manage their own keys. This creates an opportunity for better custodial solutions with genuine cryptographic guarantees, rather than promises.

## What This Means for Payment Infrastructure

For those of us building payment infrastructure that touches crypto, the immediate question is: how do we provide the custody guarantees that customers now demand?

**MPC (Multi-Party Computation) wallets.** Rather than holding customer funds in hot wallets controlled by a single key, MPC distributes key management across multiple parties. No single party can move funds unilaterally. This doesn't solve regulatory risk, but it dramatically reduces the risk of unilateral misappropriation.

**Clear asset segregation.** Customer funds should be segregated from operating capital at the infrastructure level, not just the accounting level. Smart contracts with transparent, auditable fund flows provide this in a way that internal accounting systems don't.

**On-chain transparency as default.** The most damaging thing about the FTX situation is that it was invisible until it wasn't. Payment infrastructure that operates with on-chain visibility — where fund movements are auditable by anyone — provides a different trust guarantee than "trust us."

## What Comes Next

The bear market is going to be longer and deeper because of FTX. Capital that might have flowed into crypto infrastructure in 2023 will be more cautious. Some projects that would have survived will fail. This is painful but also clarifying.

The projects and infrastructure companies that survive the next 18-24 months will be those with real business models, genuine user value, and trustworthy infrastructure design. The speculative layer gets stripped away. The infrastructure layer remains.

I remain convinced that crypto-native payment infrastructure — stablecoin settlement, programmable compliance, self-sovereign custody — represents a genuinely better architecture for moving money globally. FTX makes that argument harder to make in the short term. It doesn't invalidate it.

Build with integrity. That's the only response.
