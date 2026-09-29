# 02 — Latencia: búsqueda → respuesta

## Script

`script/evaluate_latency.py`

Mide, por `query_original` (sin Gemini):

1. Retriever HyDE + BM25 (ms)
2. Compresión + generación Q&A (ms)
3. End-to-end búsqueda → respuesta (ms)

### Cómo reproducir

```bash
python script/evaluate_latency.py --limit 15 --top-k 3
python script/evaluate_latency.py --limit 15 --top-k 3 --no-compression
```

---

## Resultados incluidos

| Condición | Run ID | Carpeta |
|-----------|--------|---------|
| Con compresión + iteración | `20260916T191220Z` | `results_con_compresion/` |
| **Sin** compresión + iteración (**último**) | `20260927T225341Z` | `results_sin_compresion/` |

Formatos: `latest.json`, `latest.csv`, `summary.md` (+ fechados).

### Condiciones comunes

- Queries: **15** · Top-K: **3** · Modelo: `qwen2.5:1.5b`

---

## Números clave (medias, ms)

| Etapa | Con compresión | Sin compresión (último) |
|-------|----------------|-------------------------|
| HyDE | 2676 | 757 |
| BM25 | 10 | 9 |
| Compresión | **20407** | **0** |
| Generación Q&A | 15107 | 2393 |
| Generador total | 35515 | 2393 |
| **E2E** | **38201 (~38 s)** | **3160 (~3.2 s)** |
| Pares / query | ~3 | **3/3 en las 15** |

---

## Interpretación

- El cuello de botella con compresión **no es BM25** (~10 ms) sino el **LLM local**: ~20 s comprimiendo + ~15 s generando.
- Sin compresión el E2E cae ~**12×** y se mantienen **3 pares** en todas las queries del batch.
- HyDE/generación también salieron más rápidos el 27-sep (posible carga/caché/hardware); el contraste dominante sigue siendo **compresión ≈ 0 vs ~20 s**.
- Alineado con RAGAS (`01`): bajar latencia sin destruir calidad → **omitir compresión** en el camino deliberativo de producto es razonable.

Detalle por query: `results_*/summary.md`.
