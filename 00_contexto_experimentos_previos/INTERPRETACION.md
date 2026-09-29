# 00 — Contexto: experimentos previos (TIC-Experiments)

Esta carpeta **no duplica** el volumen de `TIC-Experiments`. Sirve como puente del anexo hacia las fases tempranas del trabajo experimental.

Repositorio: [https://github.com/XLex0/TIC-Experiments](https://github.com/XLex0/TIC-Experiments)

---

## Mapa de fases tempranas

| Carpeta en TIC-Experiments | Rol |
|----------------------------|-----|
| `GenerateDataEvaluation/` | Construcción del dataset sintético (ground truth QG/QA) vía Semantic Scholar + LLM |
| `ProTeGÏ Optimizaction/` | Optimización del prompt de generación (ProTeGi); prompt ganador 65w en XML |
| `RetrieverArchitecture/` | Benchmarks de arquitecturas de recuperación (BEIR / SciFact, varios SLM) |
| `EndtoEndRAG/` | Piloto E2E RAG académico + dashboards de evaluación |

---

## Cómo encaja con este anexo

1. **Dataset** → alimenta los scripts de `01`–`04` (`query_original`, `documentos_fuente`).
2. **Prompt ProTeGi (65w)** → es el que usa el generador de producto / `QAGenerationPipeline`.
3. **RetrieverArchitecture / EndtoEndRAG** → exploraciones previas; la evaluación **segmentada** de este anexo es la que queda alineada al flujo real Centinela (retrieve independiente de `generate-qa`).

---

## Lectura recomendada en TIC-Experiments

- `GenerateDataEvaluation/zfinal.md` — fase 00 dataset  
- `ProTeGÏ Optimizaction/zfinal.md` — auditoría visual del prompt  
- `RetrieverArchitecture/` + `EndtoEndRAG/` — resultados y dashboards piloto  

Los números canónicos del **agente deliberativo en producto** están en las carpetas `01`–`04` de este repo.
