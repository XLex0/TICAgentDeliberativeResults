# 01 — RAGAS: calidad de la generación Q&A

## Script

`script/ragas.py`

Flujo segmentado:

1. Retrieve con `query_original` → **Recall@k**
2. `QAGenerationPipeline` (mismo componente que `generate-qa`) → pares `(pregunta, respuesta)`
3. Juez Gemini por par → **Fidelidad** + **Answer Relevancy**

No se usa Context Relevancy: las preguntas se generan desde el contexto recuperado.

### Cómo reproducir

```bash
export GEMINI_API_KEY=...
# requiere Ollama con qwen2.5:1.5b y el dataset sintético
python script/ragas.py --limit 8 --top-k 3                 # con compresión
python script/ragas.py --limit 8 --top-k 3 --no-compression
```

---

## Resultados incluidos

| Condición | Run ID | Carpeta |
|-----------|--------|---------|
| Con compresión + iteración | `20260916T181506Z` | `results_con_compresion/` |
| **Sin** compresión + iteración (**último**) | `20260927T225832Z` | `results_sin_compresion/` |

Formatos: `latest.json`, `latest.csv`, `summary.md` (+ archivos fechados).

### Condiciones comunes

- Queries: **8** (primeras `query_original`)
- Pares Q&A: **24** (3 por query; todos `ok`)
- Top-K: **3**
- Ollama: `qwen2.5:1.5b`
- Juez: `gemini-3.6-flash` · embeddings `gemini-embedding-001`

---

## Números clave

| Métrica | Con compresión | Sin compresión (último) | Δ |
|---------|----------------|-------------------------|---|
| Recall@3 | 0.6250 | **0.6667** | +0.04 |
| Fidelidad | **0.7139** | 0.6836 | −0.03 |
| Answer Relevancy | 0.7864 | **0.8038** | +0.02 |
| Pares ok | 24/24 | 24/24 | = |

---

## Interpretación

- El **generador se sostiene** sin compresión: relevancia sube ligeramente y la fidelidad baja poco (~3 puntos).
- **24/24 pares válidos** en ambos modos → el bucle diferencial / validación XML cumple el cupo.
- Recall@3 varía entre runs (HyDE estocástico); no es el foco principal de esta prueba de *generación*.
- Caso a vigilar en el run sin compresión: **q4** (fidelidad 0) — patrón puntual ya visto antes en otras queries.
- **Decisión:** con calidad comparable, priorizar el modo sin compresión por latencia (ver carpeta `02`).

Detalle por query: ver `results_*/summary.md` y CSV/JSON.
