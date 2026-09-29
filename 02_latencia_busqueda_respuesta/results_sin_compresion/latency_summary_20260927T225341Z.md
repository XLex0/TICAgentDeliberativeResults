# Latencia búsqueda → respuesta

- Run ID: `20260927T225341Z`
- Script: `scripts/evaluate_latency.py`
- Flujo: `query_original` → HyDE+BM25 → QAGenerationPipeline
- Modelo Ollama: `qwen2.5:1.5b` @ `http://127.0.0.1:11434`
- Queries: **15** (ok=15) | Top-K: `3`
- Compresión / iteración: `False` / `True`

## Resumen (ms)

| Etapa | Media | P50 | P95 | Min | Max |
|---|---|---|---|---|---|
| HyDE | 757.3 | 573.9 | 1663.2 | 291.9 | 4028.6 |
| BM25 | 8.8 | 7.2 | 18.2 | 3.5 | 25.8 |
| Retriever total | 766.1 | 581.1 | 1675.4 | 295.3 | 4034.3 |
| Compresión | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |
| Generación Q&A | 2393.3 | 2314.8 | 3469.0 | 1374.3 | 3497.8 |
| Generador total | 2393.3 | 2314.9 | 3469.0 | 1374.3 | 3497.8 |
| End-to-end (búsqueda→respuesta) | 3159.5 | 2813.8 | 4742.2 | 1951.0 | 6408.7 |

## Detalle por query

| ID | Query | Retrieve | Generador | E2E | Pares |
|---|---|---|---|---|---|
| q0 | retrieval augmented generation | 4034 | 2374 | 6409 | 3 |
| q1 | dense passage retrieval | 478 | 2315 | 2793 | 3 |
| q2 | hybrid search in information retrieval | 436 | 1989 | 2426 | 3 |
| q3 | vector database indexing algorithms | 626 | 1536 | 2162 | 3 |
| q4 | bm25 text retrieval optimization | 449 | 3457 | 3906 | 3 |
| q5 | query expansion techniques in search engin | 577 | 1374 | 1951 | 3 |
| q6 | hypothetical document embeddings hyde | 426 | 3498 | 3924 | 3 |
| q7 | reranking models for information retrieval | 480 | 1484 | 1964 | 3 |
| q8 | cross-encoder for semantic search | 581 | 2462 | 3043 | 3 |
| q9 | evaluation metrics for RAG systems | 295 | 3123 | 3418 | 3 |
| q10 | knowledge graph enhanced retrieval | 611 | 1942 | 2553 | 3 |
| q11 | multi-vector retrieval models | 598 | 3430 | 4028 | 3 |
| q12 | sparse and dense embeddings fusion | 664 | 2532 | 3197 | 3 |
| q13 | document parsing techniques for rag | 594 | 2220 | 2814 | 3 |
| q14 | semantic caching in language models | 642 | 2163 | 2805 | 3 |
