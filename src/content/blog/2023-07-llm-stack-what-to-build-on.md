---
title: 'The LLM Stack: What to Actually Build On'
description: 'Six months into the LLM boom, the stack is becoming clearer. Here is my current view on which layers are commodity, which are differentiating, and where the value actually accrues.'
heroImage: '/images/blog/llm-stack-01.jpg'
heroAlt: 'AI technology stack'
location: 'San Francisco'
pubDate: 'Jul 12 2023'
---

Six months after ChatGPT changed the conversation, the LLM application landscape is starting to stratify. The hype is still loud, but the layer architecture is becoming clearer to those building in it.

Here's my current mental model of where value sits and what to actually build on.

## The Commodity Layer

GPT-4, Claude, Gemini, Llama — foundation model capability has commoditized faster than anyone expected. The gap between frontier and open-source models has narrowed dramatically. The gap between different frontier models, for most practical applications, is smaller than the marketing suggests.

If your product's value proposition is "better LLM," you're in trouble. Model capability is a leaky moat that improves rapidly and is hard to defend.

> The foundation model layer is becoming a **commodity utility** — like compute or bandwidth. The value accrues to whoever owns the workflow, the data, and the user relationship built on top.

The exception: tasks genuinely at the frontier — complex reasoning, nuanced code generation, long-context synthesis. For those, the best models matter. But the set of tasks where the best model is decisively better than the second-best is shrinking.

## The Differentiation Layer: Context and Retrieval

The place where most real application value sits is in how you give LLMs context. A base LLM knows a lot about the world but nothing about your business. The application layer is about bringing relevant context to the model at inference time.

This is why RAG (Retrieval-Augmented Generation) is genuinely important architecture. Connecting a vector database of your domain-specific content to an LLM query transforms the output quality for domain applications.

The architecture that's working:
- Embedding pipeline for your domain data (documents, code, logs, knowledge base)
- Vector database for semantic retrieval
- Retrieval step before inference, injecting relevant context
- LLM inference with augmented context
- Output parsing and validation

![Developer building a RAG pipeline — code editor with vector database integration](/images/blog/llm-stack-code.jpg)
*The differentiation isn't the model. It's the quality of your retrieval, your domain data, and your validation layer.*

The embedding model and vector database are both largely commodity at this point. LanceDB, Chroma, Pinecone — they work. The differentiation is in what data you embed, how you structure your retrieval, and how you validate outputs.

## The Hard Problem: Reliability and Evaluation

The thing that surprises most teams building LLM applications: evaluation is the hard part.

In traditional software, correctness is often binary — the function returns the right value or it doesn't. With LLMs, outputs are probabilistic and correctness is often subjective. How do you know if your RAG pipeline is returning better answers? How do you measure whether a change to your prompt improved or degraded output quality?

Building rigorous evaluation pipelines is unglamorous and essential. Teams that skip it end up in a loop of vibes-based iteration that may or may not be improving things.

We built an evaluation framework for our payment-domain LLM applications that:
- Maintains a test set of ~300 queries with human-annotated expected outputs
- Runs automated evaluations on every prompt change using an LLM-as-judge approach
- Tracks metrics over time: accuracy, latency, cost-per-query
- Flags regressions before they reach production

![Engineering team reviewing LLM evaluation metrics and prompt performance over time](/images/blog/llm-stack-eval.jpg)
*Evaluation is the unglamorous work that separates teams shipping reliable LLM products from teams stuck in vibes-based iteration.*

This slowed down initial development. It sped up iteration after the first month significantly.

## For Financial Services Applications

The specific considerations for LLM applications in payments and financial services:

**Hallucination risk is existential.** An LLM that confidently outputs an incorrect transaction amount or compliance requirement isn't just wrong — it's potentially catastrophic. Every output that touches a financial decision needs validation against authoritative sources, not just the LLM's output.

**Audit trails matter.** Regulatory requirements mean you need to be able to explain every decision. "The LLM said so" isn't an audit trail. Build logging and explainability from the start.

**On-premise and private deployment.** Sending customer financial data to a third-party LLM API is a compliance conversation you probably don't want to have. Evaluate private deployment options (Azure OpenAI, Bedrock, self-hosted open source) before committing to architecture.

The opportunity in financial services is real. The compliance and reliability bar is higher than most LLM application developers are used to. Teams that clear that bar will build defensible products.
