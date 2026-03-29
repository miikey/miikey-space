---
title: 'Hornet'
description: 'AI Agent Swarm orchestration engine — a single Lark message triggers automatic requirement analysis, architecture design, coding, testing, and code review, all the way to a production-ready Pull Request.'
tag: 'AI Infrastructure'
status: 'Building'
year: '2026–present'
links:
  - label: 'Internal'
    href: '#'
---

*Swarm ships, humans steer.*

![Hornet — AI Agent Swarm Orchestration Engine](/images/blog/hornet-01.jpg)

I led the engineering team at UQPay in building Hornet — an AI Agent Swarm orchestration engine. A single message in Lark triggers automatic requirement analysis, architecture design, coding, testing, and code review — all the way to a production-ready Pull Request. Humans approve at critical gates. The AI swarm handles everything in between.

## The Paradigm Shift: Harness Engineering

The AI engineering field has gone through three distinct phases:

**Prompt Engineering** (2022–2023) — crafting better prompts, wording, format, few-shot examples. The question was: what do you ask?

**Context Engineering** (mid-2025) — when agents started working on real codebases, teams discovered that great prompts weren't enough. The question became: what information do you send the model?

**Harness Engineering** (early 2026) — AI agents look impressive in demos but are brittle in production. They claim tasks are done without running tests, get stuck in infinite edit loops, silently ignore constraints. Better prompts and better context cannot fix these systemic reliability problems.

Harness Engineering is the discipline of building infrastructure *around* the model: tool permissions, sandbox isolation, state persistence, CI gates, retry budgets, human approval loops, agent-to-agent review, observability. As Andrej Karpathy frames it — the model is the engine, context is the fuel, and the harness is the steering wheel, brakes, lane boundaries, maintenance schedule, and warning lights.

Hornet is a complete implementation of Harness Engineering.

The LangChain team improved their Terminal Bench 2.0 ranking through harness changes alone — same model, better infrastructure. Stripe's agents produce 1,000+ merged PRs per week, powered not by stronger models but by better harness design. Hornet systematizes these practices into a reusable orchestration engine.

## Before vs After

A medium-complexity payment feature used to take 3–5 working days from requirement to merge. With Hornet, the same feature takes less than 10 minutes of machine time.

**Before (Traditional Workflow)**

PM writes PRD (2–4h) → Review meeting (1h) → Developer reads PRD, asks questions, designs (half day) → Coding + unit tests (4–8h) → Wait for review (2–8h idle) → Fix review comments → CI fails, fix → Re-review → PR merge. Context is rebuilt 4+ times. 60% of time is spent waiting, not building.

**After (Hornet Workflow)**

PM describes requirement in Lark `@hornet` (2 min) → AI auto-generates PRD (30 sec) → PM one-click approve → AI handles architecture, coding, lint, CI, code review → PR ready → Engineer one-click merge. Zero context loss. Humans only make decisions, never execute.

The core shift: **human time moves from "doing" to "deciding"**.

## Role Transformation

Hornet doesn't replace team members — it gives each role an AI squad. Every function upgrades from executor to decision-maker.

**Product Manager** — Describe requirement in natural language (2 minutes). AI auto-generates structured PRD + subtask breakdown. PM reviews and one-click approves. Time saved: ~80%. Role upgrade: PRD writer → PRD approver.

**Architect / Tech Lead** — AI Architect Worker (Opus) auto-generates API design, data models, and file change plans from PRD + code index. Architect reviews the plan, sets guardrails via `.rules.md` files. Guard Worker enforces them automatically. Value shift: drawing diagrams → setting rules and solving hard architectural problems.

**Developer** — AI Builder Worker (Sonnet) codes, writes tests, and fixes CI in a Drone sandbox. Developer reviews the AI-generated PR and one-click merges. Mental energy freed for edge cases and complex logic that truly need human judgment. Role upgrade: code executor → code approver.

**QA / Security** — Guard Worker (Opus) auto-scores every change (0–100) + security scan. Tests auto-generated and executed by Builder. QA only reviews high-risk items flagged by Guard. Quality: from spot-checks → 100% coverage with less effort.

## Breakthroughs for Payment Scenarios

As a payment company, UQPay has stricter quality and response-time requirements than typical SaaS. Hornet delivers three critical breakthroughs:

**Rapid Compliance Response** — Regulators require new KYC fields, adjusted transaction limits, or updated risk control rules. Before: minimum 1 week from compliance requirement to release. After: compliance manager describes requirement in Lark → Hornet auto-analyzes impact scope across services → parallel coding → CI passes → engineer approves merge. Same day.

**Minute-Level Hotfix** — On-call engineer posts issue + error logs in Lark `@hornet` → AI auto-locates code, writes fix → lint + CI pass → Guard security check → engineer one-click merge. 10–15 minutes total. Before: 2–4 hours minimum.

**Multi-Repo Parallel Development** — UQPay spans multiple service repos (user-service, order-service, web-frontend, shared-libs). A single feature often touches 2–3 repos. Scout indexes all repos. Blueprints support parallel steps — one Sting can code in user-service and order-service simultaneously. Architect Worker ensures API interface consistency. Cross-repo development from sequential → parallel, with AI-guaranteed interface consistency.

## How It Works

**16-Stage Automated Pipeline**

Queen is a deterministic state machine — zero LLM calls in transitions. 6 AI Workers handle their specialized roles. Humans approve at two critical gates only.

**6 Specialized AI Workers**

Smart model routing: Haiku for fast intent parsing, Sonnet for efficient coding, Opus for deep architecture analysis and code review. The right model for the right task at every stage.

**3-Layer Context Strategy**

Workers never read the full codebase. Scout pre-indexes repos, Queen curates ~1,500 lines for the LLM, Workers search on-demand for anything else. Even with massive context windows, you can't dump 50K lines in — curation and progressive disclosure are the discipline.

**Hive Architecture**

Every component named after a bee colony role. Queen orchestrates. Scouts index. Workers build. Drones isolate. Guard reviews. Built in Rust with MySQL, Redis, and Docker.

## Live Scenario

A product manager sends in Lark:

> `@hornet Add SMS verification code login to user registration. Requirements: 1) Rate-limit SMS sends 2) Code expires in 5 minutes. Repo: user-service`

```
[~5 sec]   Intake (Haiku)    NL → structured requirement
[~30 sec]  Product (Opus)    PRD + 4 subtask breakdown
[Gate 1]   PM approves PRD
[~45 sec]  Architect (Opus)  API design + Redis TTL schema
[2-5 min]  Builder (Sonnet)  Code: 4 files +280/-12 lines + tests
[Auto]     Lint → CI → Fix   clippy pass, 15/15 tests pass
[~30 sec]  Guard (Opus)      Score 88/100, no security issues
[~5 sec]   PR Created        Pull Request ready
[Gate 2]   Engineer merges
```

Total machine time: **< 10 min** | Token cost: **~$1.20**

## Key Metrics

| Metric | Value |
|--------|-------|
| Requirement to PR | < 10 min (excl. human approval) |
| Token cost per feature | ~$1.20 |
| Team throughput multiplier | 3× |
| Curated context per run | ~1,500 lines |
| Auto code review coverage | 100% |
| Human approval gates | 2 |

Monthly token cost at 100 Stings/month: ~$120. A mid-level engineer costs 50–100× that. Hornet isn't about saving money — it's about creating delivery velocity that was previously impossible.

---

*Let the swarm deliver. You steer.*
