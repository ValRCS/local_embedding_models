# Local Multilingual Embedding Models (March 2026)

Reference comparison for locally runnable embedding models on:

- 32GB RAM
- RTX 5070-class GPU (16GB VRAM)
- FP16 inference
- Proper batching
- Dense embedding output

Throughput estimates are sustained production estimates.

---

## Long-Context Embedding Models (8K–32K)

Best suited for:
- Large document chunks
- Chapter-level embeddings
- Retrieval over long documents

| Model | Country | License | Max Context | Native Dim | Optimization | Docs/min (256) | Docs/min (4096) | Canonical Link |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Qwen3-Embedding 0.6B | China | Apache 2.0 | 32K | 1024 (MRL) | Retrieval + similarity | 7,000–10,000 | 10–35 | https://huggingface.co/Qwen/Qwen3-Embedding-0.6B |
| Qwen3-Embedding 4B | China | Apache 2.0 | 32K | 2560 (MRL) | Retrieval-strong | 1,800–3,000 | 3–12 | https://huggingface.co/Qwen/Qwen3-Embedding-4B |
| Qwen3-Embedding 8B | China | Apache 2.0 | 32K | 4096 (MRL) | Retrieval-heavy | 700–1,200 | 1–4 | https://huggingface.co/Qwen/Qwen3-Embedding-8B |
| jina-embeddings-v4 | Germany | Qwen Research License | 32K | Variable (MRL) | Retrieval + doc matching | 3,500–6,000 | 8–25 | https://huggingface.co/jinaai/jina-embeddings-v4 |
| jina-embeddings-v3 | Germany | Apache 2.0 | 8192 | 1024 | General + retrieval | 6,000–9,500 | 10–40 | https://huggingface.co/jinaai/jina-embeddings-v3 |
| BGE-M3 | China | MIT | 8192 | 1024 | Hybrid (dense + sparse) | 9,000–13,000 | 20–60 | https://huggingface.co/BAAI/bge-m3 |
| GTE-multilingual-base | China | Apache 2.0 | 8192 | 768 | Retrieval | 9,500–14,000 | 20–70 | https://huggingface.co/Alibaba-NLP/gte-multilingual-base |
| Snowflake Arctic-Embed-L-v2.0 | USA | Apache 2.0 | 8192 | 1024 (compressible) | Retrieval | 7,000–10,000 | 15–50 | https://huggingface.co/Snowflake/snowflake-arctic-embed-l-v2.0 |

---

## High-Speed Multilingual Models (Shorter Context)

Best suited for:
- Sentence-level similarity
- Clustering
- Concept geometry
- Query embeddings

| Model | Country | License | Max Context | Native Dim | Optimization | Docs/min (256) | Canonical Link |
| --- | --- | --- | --- | --- | --- | --- | --- |
| multilingual-e5-large | International | MIT | 512 | 1024 | Similarity + retrieval | 12,000–18,000 | https://huggingface.co/intfloat/multilingual-e5-large |
| LaBSE | USA | Apache 2.0 | ~256–512 | 768 | Sentence similarity | 15,000–21,000 | https://huggingface.co/sentence-transformers/LaBSE |
| LASER encoders | USA | BSD-style | Sentence-level | 1024 | Cross-lingual similarity | 18,000–24,000 | https://github.com/facebookresearch/LASER |

---

## Language Coverage

All listed models:
- Claim 70+ languages or are based on multilingual backbones
- Suitable for Latvian, English, Russian, German
- Runnable locally on mid-tier hardware

Some (Qwen3) explicitly list Latvian.

---

## Choosing by Use Case

### Retrieval over large documents
- BGE-M3
- Qwen3-Embedding (0.6B / 4B)
- GTE-multilingual-base

### Clustering / Concept Graphs / PCA
- multilingual-e5-large
- BGE-M3
- LaBSE

### Chapter-Level Embeddings
- Qwen3-Embedding 0.6B
- jina-embeddings-v4

## CPU-Only Embedding Performance (Xeon E3-1245 v3, 32GB DDR3, SATA SSD)

Assumptions:

- Intel Xeon E3-1245 v3 (Haswell, 4 cores / 8 threads, AVX2 support)
- 32GB DDR3 RAM
- SATA SSD
- CPU-only inference (no GPU)
- 256-token chunks
- Dense embeddings
- Proper batching (critical on CPU)

Performance depends heavily on:

- Model size
- Backend (PyTorch vs ONNX Runtime)
- Quantization (fp32 vs int8)
- Batch size
- Thread configuration

Below are realistic sustained throughput estimates in **chunks per minute**.

| Model Class (Examples) | Approx Model Size | Backend | Estimated Chunks / Minute (CPU-only) |
| --- | --- | --- | --- |
| LASER encoders | Smaller / lightweight | Native CPU / optimized | 300–1,000+ |
| LaBSE | ~400–500M | PyTorch CPU | 40–120 |
| multilingual-e5-large | ~560M | PyTorch CPU | 20–80 |
| GTE-multilingual-base | ~600M | PyTorch CPU | 20–80 |
| BGE-M3 | ~600M | PyTorch CPU | 20–80 |
| Encoder models (int8 via ONNX Runtime) | Same as above | ONNX Runtime int8 | 40–150 |
| Qwen3-Embedding 4B / 8B | Multi-GB | CPU-only | Not practical (often single digits/min) |

---

### Wall-Clock Interpretation

- 100 chunks/min ≈ 6,000 chunks/hour  
- 50 chunks/min ≈ 3,000 chunks/hour  
- 25 chunks/min ≈ 1,500 chunks/hour  

Embedding a large corpus on this CPU is feasible, but measured in **hours or days**, not minutes.

---

### Practical Recommendations for Xeon-Class Hardware

1. Prefer encoder models (e5 / GTE / BGE-M3 / LaBSE) over multi-billion parameter embedding LLMs.  
2. Use batching aggressively (e.g., 16–64) and benchmark.  
3. Use ONNX Runtime int8 where supported for potential ~2× speedup.  
4. Keep chunk size at 256–512 tokens. Longer chunks will significantly reduce throughput.  

---

This repository is intended for empirical benchmarking and experimentation across multilingual embedding spaces.
