---
title: 'AI Agents in Production: The Gap Between Demo and Reality'
description: 'Agent demos are compelling. Production agents are a different problem. Here is what building and running AI agents in a payment context actually looks like.'
pubDate: 'Sep 16 2024'
---

The AI agent demo is a genre. A compelling system prompt, a few tool calls, an LLM that chains reasoning steps together and produces an impressive result. The demo convinces you that autonomous AI agents are real and production-ready.

Then you try to build one for a real use case. The gap between demo and production is where most agent projects currently live.

Having built and deployed several agents in production contexts over the past year, here's my honest accounting.

## What Demos Hide

**Reliability at tail cases.** Agent demos show the success path. Production systems encounter the full distribution of inputs: malformed data, unexpected edge cases, adversarial inputs, ambiguous instructions. LLMs handle the common cases well. Tail case handling requires explicit engineering that demos skip.

**Latency and cost at scale.** A multi-step agent that takes 30 seconds and costs $0.30 per invocation is a fine demo. At 10,000 daily invocations, that's $3,000/day and a UX problem. Cost and latency optimization for agents is a distinct engineering problem from making them work at all.

**The failure modes of tool calls.** Tool calls are where agents interact with the real world: APIs, databases, external services. External services are unreliable, rate-limited, and don't conform to what the LLM expects. Building robust tool call handling — retries, error propagation, partial failure recovery — is most of the work.

**Prompt fragility.** Agent behaviors can change unexpectedly when the underlying model is updated. A prompt that produces reliable behavior with GPT-4-turbo-0125 may produce different behavior with the next version. Production agents need regression testing for behavior, not just unit testing for code.

## What We Built in Payments

We deployed agents in two contexts that I can talk about:

**Transaction anomaly investigation.** When our monitoring system flags a suspicious transaction pattern, an agent investigates: pulls the transaction history, checks merchant category codes, cross-references against known fraud patterns, looks up account history, and produces a structured risk assessment with a recommended action. This used to take a fraud analyst 15-20 minutes. The agent does it in 30-45 seconds with comparable quality on straightforward cases.

The limits: novel fraud patterns it hasn't seen before, cases requiring contextual judgment about business type or geography, situations where the recommended action needs human confirmation before execution. We kept the human in the loop for final decisions.

**Support ticket triage and response drafting.** Inbound merchant support tickets get classified, relevant account information is pulled, and a draft response is generated. The agent handles ~60% of tickets with a draft that requires minimal editing. For the remaining 40%, it provides context that makes human response faster.

The failure modes we encountered: confidently wrong responses about account specifics, hallucinated policy details, responses that technically answered the question asked but missed the underlying concern.

## The Production Architecture That Works

After iterations, the architecture that's holding up:

**Tight tool boundaries.** Each tool does one thing and validates inputs and outputs strictly. The agent composes tools; the tools enforce correctness.

**Explicit state machines for multi-step workflows.** Rather than letting the agent reason freely about what to do next, constrain the state space. Define the valid transitions. The agent can choose from valid transitions; it can't go off-piste.

**Conservative defaults.** When uncertain, do less. Flag for human review rather than taking an action that might be wrong. This makes agents less impressive in demos. It makes them safer in production.

**Evaluation before deployment.** A test suite of 200+ real cases with labeled expected outputs. Agents don't ship unless they clear the evaluation threshold on the full suite. This catches regressions when prompts change or models update.

## The Real Value Proposition

The honest value proposition for production agents isn't "fully autonomous." It's "human judgment at higher leverage." The agent does the information gathering, synthesis, and first-pass reasoning. The human makes decisions on cases that matter, with better information and in less time.

That's a meaningful productivity gain. It's not the Sci-Fi version. Build for the realistic version and you'll ship something that actually works.
