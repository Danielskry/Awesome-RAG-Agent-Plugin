---
name: rag-advisor
description: Recommends a RAG architecture pattern and framework given a project's requirements (scale, data types, latency, freshness, reasoning complexity). Use when the user is starting a new RAG project, deciding between naive/agentic/graph RAG, or picking between LangChain, LlamaIndex, Haystack, and similar frameworks.
---

# RAG Advisor

Help the user pick a RAG architecture pattern and supporting framework/tooling by matching their requirements against the options below, drawn from [Awesome-RAG](https://github.com/Danielskry/Awesome-RAG).

## Step 1: Clarify requirements

Ask (or infer from the repo/context) only what's missing:
- Data: structured/unstructured, single vs. multi-source, how often it changes
- Query complexity: single-hop lookup vs. multi-step reasoning vs. exploratory research
- Latency/cost budget: interactive chat vs. batch/offline
- Need for source attribution, multi-modality (images/video), or time-sensitive data

## Step 2: Match an architecture pattern

| Pattern | When to recommend |
|---|---|
| **Naive RAG** | Simple retrieve-then-generate; prototype or low query complexity |
| **Advanced RAG** | Adds query rewriting, re-ranking, context compression; most production text QA |
| **Modular RAG** | Composable retrieval/ranking/generation components; teams that need to swap parts independently |
| **Agentic RAG** | LLM decides when/what/how to retrieve, can loop; multi-step or tool-using queries ([LangGraph agentic RAG](https://langchain-ai.github.io/langgraph/tutorials/rag/langgraph_agentic_rag/)) |
| **Self-RAG** | Model self-reflects on retrieval quality and adjusts; when hallucination risk is high |
| **Corrective RAG (CRAG)** | Refines/corrects retrieved docs before use; noisy or low-quality corpora |
| **GraphRAG** | Knowledge-graph-backed retrieval; entity-heavy, relationship-heavy domains ([microsoft/graphrag](https://github.com/microsoft/graphrag)), or codebases ([Code-Graph-RAG](https://github.com/vitali87/code-graph-rag)) |
| **Reasoning-based RAG (e.g. PageIndex)** | Vectorless, LLM-guided tree search over hierarchical docs; long structured/professional documents where chunking loses too much |
| **Vision-RAG / Multimodal RAG** | Page-as-image or text+image+audio retrieval; visually dense documents (tables, charts, scanned PDFs) |
| **Cache-Augmented Generation (CAG)** | Preload docs into context and reuse KV cache; small, static corpora where retrieval overhead isn't worth it |

Default recommendation when unsure: start with **Advanced RAG** (hybrid search + re-ranking), and only add agentic/graph complexity once naive retrieval demonstrably fails on real queries.

## Step 3: Match a framework

- **[LangChain](https://python.langchain.com/docs/modules/data_connection/)**: general-purpose, largest ecosystem, good default for Python teams
- **[LlamaIndex](https://docs.llamaindex.ai/en/stable/optimizing/production_rag/)**: strongest for data connectors and production RAG patterns out of the box
- **[Haystack](https://github.com/deepset-ai/haystack)**: pipeline-oriented, good for teams that want explicit, inspectable pipelines
- **[Semantic Kernel](https://github.com/microsoft/semantic-kernel)**: Microsoft/.NET-heavy stacks
- **[Dify](https://github.com/langgenius/dify)** / **[Flowise](https://github.com/FlowiseAI/Flowise)**: low-code/UI-driven builders
- **[Mastra](https://github.com/mastra-ai/mastra)** / **[Swiftide](https://github.com/bosun-ai/swiftide)**: TypeScript / Rust-native stacks
- **[CocoIndex](https://github.com/cocoindex-io/cocoindex)** / **[Pathway](https://github.com/pathwaycom/pathway/)**: ETL/incremental-indexing-first pipelines with realtime updates
- **[Cognita](https://github.com/truefoundry/cognita)** / **[Verba](https://github.com/weaviate/Verba)**: turnkey, production-ready RAG-out-of-the-box apps
- No framework: recommend a custom pipeline when requirements are simple, latency-critical, or the team wants full control over retrieval logic

## Output format

Give: (1) the recommended pattern with a one-line reason, (2) the recommended framework with a one-line reason, (3) one explicit tradeoff they're accepting, (4) a link to the relevant section of Awesome-RAG for deeper reading.
