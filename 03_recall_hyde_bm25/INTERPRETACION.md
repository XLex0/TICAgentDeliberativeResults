# 03 — Recall ampliado (HyDE + BM25)

## Script

`script/evaluate_recall.py`

Solo **retriever** (sin Gemini, sin generador Q&A): HyDE (Ollama) + BM25 sobre el corpus del dataset sintético.

### Cómo reproducir

```bash
python script/evaluate_recall.py --limit 30 --top-k 3
```

---

## Resultados incluidos

| Run ID | Carpeta |
|--------|---------|
| `20260916T183926Z` | `results/` |

Formatos: `latest.json`, `latest.csv`, `summary.md` (+ fechados).

### Condiciones

- Queries: **30** · Top-K: **3** · Modelo HyDE: `qwen2.5:1.5b`

---

## Números clave

| Métrica | Score |
|---------|-------|
| Recall@3 | **0.5833** |
| Hit rate (≥1 gold en top-3) | **0.8667** |
| Queries con Recall = 1.0 | 7 / 30 |
| Queries con Recall = 0 | 4 / 30 |

---

## Interpretación

- El **hit rate es alto (~0.87)**: en la mayoría de queries entra al menos un documento gold.
- El cuello suele ser recuperar **todos** los gold, no encontrar ninguno.
- Fallos totales (recall 0) en el run: candidatos a análisis cualitativo de HyDE/expansión (p.ej. dilución de señal léxica).
- Esta prueba **no** mezcla juez Gemini: es la medición limpia del retriever local usado en la Fase A de RAGAS.

Detalle: `results/summary.md` y CSV.
