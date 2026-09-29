# Resumen evaluación RAGAS (segmentada)

- Run ID: `20260927T225832Z`
- Diseño: retrieve(`query_original`) → QAGenerationPipeline → RAGAS(F, AR)
- Modelo juez: `gemini-3.6-flash`
- Embeddings: `gemini-embedding-001`
- Ollama: `qwen2.5:1.5b`
- Queries: **8** | Pares Q&A: **24**
  (ok=24, partial=0, error=0)
- Top-K: `3`
- Compresión / iteración: `False` / `True`

## Promedios

| Métrica | Score |
|---|---|
| Recall@3 (por query) | 0.6667 |
| Fidelidad (faithfulness) | 0.6836 |
| Relevancia de la respuesta | 0.8038 |

Archivos: `ragas_results_20260927T225832Z.json`, `ragas_results_20260927T225832Z.csv`
