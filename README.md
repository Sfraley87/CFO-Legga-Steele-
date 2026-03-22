# Boardroom CFO — Financial Planning & Cash Runway Analysis Agent
### AI sub-agent for the Boardroom OS multi-agent framework

![n8n](https://img.shields.io/badge/Built%20with-n8n-orange?style=flat-square)
![Claude](https://img.shields.io/badge/LLM-Claude%20Sonnet%204.5-8A2BE2?style=flat-square)
![Cohere](https://img.shields.io/badge/Embeddings-Cohere-003366?style=flat-square)
![Memory](https://img.shields.io/badge/Memory-Vector%20Store-teal?style=flat-square)
![Type](https://img.shields.io/badge/Type-Sub--Agent-gray?style=flat-square)

---

## Overview

The **Boardroom CFO Agent** is a specialized AI sub-agent designed to handle financial planning, cash runway analysis, and treasury-level Q&A for mid-market companies. It operates as part of the **Boardroom OS** — a multi-agent executive intelligence platform where each C-suite function is handled by a dedicated AI agent with its own memory, context, and domain expertise.

This agent is invoked by a parent orchestrator and returns structured financial reasoning back into the broader system.

---

## What It Does

- Answers financial planning questions in natural language (burn rate, runway, scenario modeling, budget gaps)
- Retrieves relevant prior financial context from vector memory before responding
- Logs every interaction as a structured memory entry
- Re-embeds and stores the output — so context compounds over time and future queries benefit from prior analysis

**This agent gets smarter the more it's used.**

---

## Architecture

```
Parent Orchestrator
        │
        ▼
Execute Workflow Trigger      ← Called by Boardroom OS router
        │
        ▼
AI Agent: Legga               ← Claude Sonnet 4.5 | CFO persona + system prompt
        │              │
        │        Memory Retrieve (vector store)
        │              └── Cohere Embeddings
        │
        ▼
Build Log Entry               ← Structures agent output as a memory record
        │
        ▼
Memory Insert                 ← Writes to vector store for future retrieval
               └── Cohere Embeddings
```

### Key Design Decisions

**Retrieve → Reason → Log loop** — Before the agent answers, it pulls semantically relevant context from prior sessions. After it answers, that response is embedded and stored. This creates a compounding knowledge base rather than a stateless Q&A tool.

**Sub-agent pattern** — This workflow is not triggered by a user directly. It's called by a parent orchestrator via `Execute Workflow Trigger`, which means it can be composed into larger multi-agent pipelines without modification.

**Named agent identity (Legga)** — Each Boardroom OS agent has a named persona and domain-specific system prompt. The name is intentional — it creates a consistent identity that the orchestration layer can reference, route to, and build trust around.

---

## Agent Identity

| Property | Value |
|----------|-------|
| Agent Name | Legga |
| Domain | CFO / Financial Planning |
| Model | Claude Sonnet 4.5 |
| Embeddings | Cohere |
| Memory | In-memory vector store (session-persistent) |
| Trigger Type | Sub-agent (called by parent workflow) |

---

## Part of Boardroom OS

This agent is one node in a larger multi-agent executive platform. Boardroom OS is built on the premise that mid-market companies deserve the same AI-augmented decision-making infrastructure that enterprise firms are building internally — without the 7-figure implementation cost.

Each department gets its own AI agent:

| Agent | Domain |
|-------|--------|
| CFO Agent (this) | Financial planning, cash runway, burn rate |
| COO Agent | Operations, capacity, fulfillment |
| CMO Agent | Pipeline, campaign performance, growth |
| CSO Agent | Sales intelligence, forecasting |
| CHRO Agent | Headcount, retention, org health |

All agents share a central orchestration and memory layer — the Boardroom OS router.

---

## Setup

### Prerequisites
- n8n instance with LangChain nodes enabled
- Anthropic API key (Claude Sonnet 4.5)
- Cohere API key (for embeddings)

### Credentials Needed

| Credential | Node |
|------------|------|
| Anthropic API | `Anthropic Chat Model` |
| Cohere API | `Embeddings Cohere`, `Embeddings Cohere1` |

### Deployment Notes
- This workflow is designed to be called by a parent orchestrator, not run standalone
- The `vector_store_key` memory key should match across retrieve and insert nodes — do not change unless you're intentionally isolating memory namespaces
- To run standalone for testing, replace `Execute Workflow Trigger` with a `Chat Trigger` or `Manual Trigger`

---

## About

Built by **Shaun** — AI Automation Architect at [Synelium](https://synelium.com)

Synelium designs and deploys AI-powered automation infrastructure for mid-market companies. Boardroom OS is the flagship product — an agent orchestration platform that embeds AI into every executive function.

→ More projects:(https://github.com/Sfraley87)  
→ Connect: www.linkedin.com/in/shaun-fraley-41a0b9132


