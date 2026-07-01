---
name: rag-evaluator
description: Designs an evaluation plan for a RAG system's retrieval and generation quality, covering similarity metrics, groundedness/completeness/utilization checks, and which evaluation tool to wire up. Use when the user asks how to test, benchmark, or debug retrieval/answer quality, or how to detect hallucinations.
---

# RAG Evaluator

Help the user build an evaluation plan for a RAG system, drawn from [Awesome-RAG's Metrics & Evaluation section](https://github.com/Danielskry/Awesome-RAG#-metrics--evaluation).

## Step 1: Separate retrieval evaluation from generation evaluation

RAG failures are almost always one of: **bad retrieval** (right doc not found), **bad use of context** (right doc found, model ignores/misreads it), or **bad grounding** (model adds unsupported claims). Diagnose which one before recommending fixes.

## Step 2: Retrieval quality, embedding similarity metrics

- **Cosine similarity**: default choice for comparing text embeddings; direction encodes semantics
- **Dot product**: equivalent to cosine when vectors are normalized; cheaper at scale
- **Euclidean distance**: degrades in high dimensions (curse of dimensionality); mainly useful post dimensionality-reduction
- **Jaccard similarity**: token/n-gram overlap; useful for keyword/BM25-style comparisons, not dense embeddings

Recommend cosine or dot product unless there's a specific reason otherwise.

## Step 3: Generation quality, key dimensions

- **Groundedness**: is the response based entirely on retrieved context? Low groundedness means higher hallucination risk
- **Completeness**: does the response cover all aspects of the query?
- **Utilization**: how much of the retrieved context actually contributed to the answer (check via LLM-as-judge scanning for inclusion of retrieved chunks)
- **Relevance / Fluency / Factual accuracy / Coherence**: classic human-eval dimensions, useful for spot-checks and annotation queues

## Step 4: Automated benchmarking (secondary, use with care)

- **BLEU** / **ROUGE** / **METEOR**: n-gram overlap metrics, weak signal for open-ended RAG answers, better for summarization/translation-style tasks. Don't over-index on these alone.

## Step 5: Pick a tool

- **[Ragas](https://docs.ragas.io/en/stable/)**: purpose-built RAG pipeline evaluation (faithfulness, answer relevance, context precision/recall); usually the first tool to reach for
- **[LangSmith](https://docs.smith.langchain.com/)**: production monitoring and evaluation if already on LangChain/LangGraph
- **[LangFuse](https://github.com/langfuse/langfuse)** / **[Opik](https://github.com/comet-ml/opik)**: open-source LLM observability, tracing, and prompt management
- **[Weights & Biases](https://wandb.ai/wandb-japan/rag-hands-on/reports/Step-for-developing-and-evaluating-RAG-application-with-W-B--Vmlldzo1NzU4OTAx)**: experiment tracking across chunking/embedding/prompt variants
- **[Hugging Face Evaluate](https://github.com/huggingface/evaluate)**: BLEU/ROUGE computation
- **[WFGY Problem Map](https://github.com/onestardao/WFGY/tree/main/ProblemMap)**: 16-mode checklist for diagnosing specific RAG/LLM failure patterns; use when the failure mode is unclear

## Step 6: Build a synthetic test set

Generate query/expected-answer/expected-source-doc triples covering: exact-match lookups, multi-hop questions, out-of-corpus questions (should refuse/say "don't know"), and ambiguous queries. Re-run this set after every chunking/embedding/prompt change. This is the regression suite for RAG.

## Output format

Give: (1) which failure category the reported symptom most likely falls into, (2) the specific metric(s) to add, (3) one concrete tool recommendation, (4) a minimal test-set structure to start with.
