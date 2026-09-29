# 04 — Comparación Recall: HyDE+BM25 vs TF-IDF

## Script

`script/compare_recall.py`

Misma dataset, mismas 30 `query_original`, mismo corpus sintético (501 docs), top-k=3.

**Nota:** no se usa el pickle TF-IDF de producción (Neo4j), porque el gold sintético no coincide con ese índice. El baseline es TF-IDF sklearn entrenado **sobre el mismo corpus** que HyDE+BM25.

### Cómo reproducir

```bash
python script/compare_recall.py --limit 30 --top-k 3
```

---

## Resultados incluidos

| Run ID | Carpeta |
|--------|---------|
| `20260916T185850Z` | `results/` |

Formatos: `latest.json`, `latest.csv`, `summary.md` (+ fechados).

---

## Números clave

| Métrica | HyDE+BM25 | TF-IDF | Δ |
|---------|-----------|--------|---|
| Recall@3 | 0.6278 | **0.8778** | −0.25 |
| Hit rate | 0.9000 | **1.0000** | −0.10 |
| Recall=1.0 | 9/30 | **22/30** | — |
| Latencia media | ~2178 ms | **~3 ms** | — |

Ganadores por query: TF-IDF **16** · empate **13** · HyDE **1**.

---

## Interpretación

- En este benchmark **keyword-heavy**, el baseline léxico (TF-IDF) gana claramente en Recall y cobertura perfecta.
- HyDE+BM25 es órdenes de magnitud más lento (llamada a Ollama) y a veces **diluye** la señal léxica que TF-IDF aprovecha.
- Implicación de producto: el BFF puede usar TF-IDF primero y **fallback semántico** cuando el índice léxico viene vacío (mocks / vocabulario no alineado) — coherente con el diagrama deliberativo Fase 1.
- HyDE aporta más valor potencial en queries naturales/ambiguas; convendría un subconjunto aparte si se quiere demostrar esa ventaja.

Detalle: `results/summary.md`.
