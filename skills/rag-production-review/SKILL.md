---
name: rag-production-review
description: Reviews a RAG codebase or design against production-readiness concerns, covering scalability, reliability/monitoring, data management, security, and cost. Use when the user asks to review a RAG pipeline before shipping, audit an existing implementation, or asks "what am I missing" about a RAG app.
---

# RAG Production Review

Audit the user's RAG implementation against the checklist below, drawn from [Awesome-RAG's Production Considerations and Best Practices sections](https://github.com/Danielskry/Awesome-RAG#-production-considerations). For each unchecked item, state the concrete risk, not just the missing feature.

## Scalability & performance
- Indexing pipeline handles incremental updates, not just full re-index
- Query latency addressed via efficient ANN indexing (HNSW/IVF), caching, parallel retrieval
- Concurrent request handling: connection pooling, request queuing, load balancing
- GPU/CPU/memory and DB connection pool usage is monitored

## Reliability & monitoring
- Logging, tracing, and metrics (latency, throughput, error rate) exist for the retrieval and generation stages separately
- Health checks cover embedding service, vector DB connectivity, and LLM API status independently
- Retry logic, circuit breakers, and graceful degradation are implemented (what happens when retrieval fails: does it fall back to no-context generation, or fail loudly?)
- A/B testing capability exists for comparing retrieval strategies, chunking, or prompts

## Data management
- Incremental/near-real-time indexing supported (no full re-embed for small updates)
- Document versions, embedding model versions, and prompt templates are tracked
- Validation pipeline catches corrupted embeddings, missing metadata, stale content
- Vector index and metadata store are backed up

## Security & compliance
- Authentication, authorization, and audit logging on retrieval/query endpoints
- Data encrypted at rest and in transit; data residency requirements addressed if applicable
- Content moderation and PII detection applied to both ingested docs and generated output
- Rate limiting present to prevent abuse
- **Prompt injection**: input validation/sanitization, clear delimiters separating instructions from retrieved/user content, output monitoring for anomalies. Check this explicitly, it's the most commonly skipped item

## Cost optimization
- Embeddings are cached, not recomputed for unchanged content
- Query routing avoids unnecessary retrieval calls (e.g., skip retrieval for greetings/chitchat)
- Embedding/LLM model choice is justified against cost, not just quality
- Infra is right-sized against actual traffic, not worst-case guesses

## Also check core pipeline quality (fast to overlook)
- **Chunking**: is the strategy justified (fixed/recursive/semantic/document-based) for this document type, with 10-20% overlap and preserved metadata?
- **Embedding consistency**: same model used for indexing and querying, a common silent bug
- **Retrieval**: hybrid search (vector + BM25) and re-ranking present, or explicitly deferred with a reason
- **Source attribution**: responses cite retrieved sources; groundedness is checked somewhere in the pipeline

## Output format

Produce a checklist grouped by the five categories above, each item marked ✅ present / ⚠️ partial / ❌ missing based on what's in the code, with a one-line risk statement for every ❌.
