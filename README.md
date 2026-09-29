# TIC Agent Deliberative Results

**Anexo de tesis** — resultados del agente deliberativo / pipeline RAG segmentado de Centinela (TiC).

Autor: Alexander Motoche Viracocha  
Proyecto: Asistente sociotécnico basado en LLM/RAG sobre Centinela V3

Este repositorio concentra, de forma **reproducible y legible**, los scripts de evaluación del pipeline de producto y sus **últimos resultados**, junto con una interpretación en Markdown por prueba.

> Experimentos previos (dataset, ProTeGi, arquitecturas de retriever, E2E piloto) viven en  
> [`XLex0/TIC-Experiments`](https://github.com/XLex0/TIC-Experiments). Ver carpeta [`00_contexto_experimentos_previos/`](./00_contexto_experimentos_previos/).

---

## Cómo leer este anexo

Cada carpeta numerada contiene:

| Elemento | Contenido |
|----------|-----------|
| `script/` | Script Python usado para la prueba |
| `results*/` | Artefactos crudos del **último run** (JSON, CSV, summary MD) |
| `INTERPRETACION.md` | Qué se midió, condiciones, números clave y lectura |

---

## Índice de pruebas

| # | Carpeta | Script | Último run | Mensaje clave |
|---|---------|--------|------------|---------------|
| 00 | [`00_contexto_experimentos_previos/`](./00_contexto_experimentos_previos/) | — | — | Enlace a fases tempranas en TIC-Experiments |
| 01 | [`01_ragas_calidad_generacion/`](./01_ragas_calidad_generacion/) | `ragas.py` | 2026-09-27 (sin compresión) + 2026-09-16 (con) | Calidad comparable con/sin compresión |
| 02 | [`02_latencia_busqueda_respuesta/`](./02_latencia_busqueda_respuesta/) | `evaluate_latency.py` | 2026-09-27 sin compresión | E2E ~38 s → ~3.2 s (~12×) |
| 03 | [`03_recall_hyde_bm25/`](./03_recall_hyde_bm25/) | `evaluate_recall.py` | 2026-09-16 | Recall@3 ≈ 0.58 · hit rate ≈ 0.87 |
| 04 | [`04_comparacion_hyde_vs_tfidf/`](./04_comparacion_hyde_vs_tfidf/) | `compare_recall.py` | 2026-09-16 | En corpus keyword-heavy, TF-IDF gana Recall |

---

## Diseño de evaluación (segmentado, alineado al producto)

```
query_original
  → Retriever (HyDE + BM25)
  → QAGenerationPipeline (generate-qa; igual que el front)
  → Métricas (Recall / Fidelidad / Answer Relevancy / Latencia)
```

Búsqueda y generación se evalúan **por separado**, como en producción (`articles/relevant` + `generate-qa` asíncrono).

- Retriever / SLM local: **Ollama** `qwen2.5:1.5b`
- Juez RAGAS: **Gemini** `gemini-3.6-flash` + embeddings `gemini-embedding-001`
- Dataset: `dataset_qg_qa_sintetico.json` (ground truth de TIC-Experiments / GenerateDataEvaluation)

---

## Decisión de diseño (síntesis)

Sin compresión de contexto, la **calidad RAGAS se sostiene** (fidelidad ~0.68 vs ~0.71; relevancia ~0.80 vs ~0.79) y la **latencia baja ~12×**. Por eso no se adoptó “comprimir los 3 documentos en una sola petición” como siguiente paso obligatorio.

Detalle por carpeta en cada `INTERPRETACION.md`.
