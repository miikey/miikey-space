---
title: 'ChatGPT Changed My Engineering Process. Here Is How.'
description: 'Three months into daily LLM use, here is what has actually changed in how I build — not the hype, the real behavioral shifts and where the limits are.'
heroImage: '/images/blog/llm-engineering-01.jpg'
heroAlt: 'AI language model'
location: 'San Francisco'
pubDate: 'Mar 21 2023'
---

ChatGPT launched in November 2022. By February 2023, GitHub Copilot was in widespread use on my team. By March, I was using LLMs for something in almost every working day.

Three months of serious daily use is enough time for the novelty to wear off and the real patterns to emerge. Here's an honest account of what has actually changed.


## What Changed Immediately

**Documentation and code explanation.** The first thing I changed was how I dealt with unfamiliar code. Before: find a senior person who knows the system, or spend an hour reading. After: paste the code into GPT-4, ask "explain this to me and point out anything unusual." The answers aren't always correct, but they're usually good enough to orient me in 2 minutes rather than 20.

**Boilerplate generation.** I write a lot less boilerplate from scratch. CRUD API, database schema for a described domain, test case scaffolding — these are all faster with LLM assistance. Not because the LLM writes perfect code (it doesn't), but because it writes plausible code that I can edit faster than I can write from scratch.

**Rubber duck debugging.** Describing a problem to an LLM forces you to articulate it clearly — the same effect as explaining it to a colleague. Except the LLM sometimes has a useful suggestion, and it's available at 2am.

## What Took Longer to Change

**Architecture decisions.** LLMs are genuinely not good at system design tradeoffs. They'll give you confident answers, but they tend toward consensus views and struggle with context-specific constraints. "Should I use an event-driven architecture for this payment processing system given our specific latency and consistency requirements?" requires human judgment about tradeoffs that LLMs flatten into generic best practices.

**Security-critical code.** I don't trust LLM-generated code for anything touching authentication, cryptography, or financial transaction processing without thorough review. The confidence of the output doesn't correspond to correctness in these domains. We had one near-miss with a subtle timing attack vulnerability in LLM-generated authentication code that a careful review caught.

**Cross-system reasoning.** LLMs lose coherence over long contexts and across multiple interconnected systems. Understanding how a change in the card authorization flow affects the settlement reconciliation process requires holding the full system model in mind — something LLMs don't do well yet.

## What Changed on the Team

The productivity distribution shifted. Engineers who were already strong got stronger — they used LLMs to move faster in areas where they had enough expertise to evaluate the output. Engineers who were struggling got... more confidently wrong answers more quickly.

> **LLMs don't tell you when they're wrong with any less confidence than when they're right.** A senior engineer can catch the confident wrong answer. A junior engineer often can't — and that asymmetry is the real risk management challenge for teams adopting these tools.

This is the thing nobody talks about enough: LLMs don't tell you when they're wrong with less confidence than when they're right. A senior engineer can catch the confident wrong answer. A junior engineer often can't.

We added a practice: any LLM-generated code that goes into production gets flagged as such in the PR. Not as a criticism — as context. It means the reviewer knows to apply more scrutiny to certain patterns.

![Engineers collaborating on code review at whiteboard](/images/blog/llm-code-fix.jpg)
*Team practices around LLM-generated code matter as much as the tools themselves — shared norms prevent the confident-but-wrong failure mode.*

## The Bigger Picture

We're at the beginning of a genuine shift in how software gets built. The current tools are impressive but clearly early. The things that LLMs do well — synthesis, explanation, pattern application, boilerplate generation — are real productivity multipliers. The things they do poorly — novel reasoning, cross-system coherence, reliable security — are still human work.

The engineers who will thrive aren't the ones who resist these tools or the ones who trust them uncritically. They're the ones who build accurate mental models of where LLMs are useful and where they're dangerous, and use them accordingly.

That's a judgment skill. It's not that different from knowing when to use a library and when to write your own.

![Close-up of code on a dark terminal screen](/images/blog/2023-03-llm-changed-engineering-process-inline-03.jpg)
*The code still has to work. LLMs change how fast you get to a working draft — they don't change what "working" means.*
