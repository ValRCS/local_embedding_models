# Local Multilingual Embedding Models (March 2026)

Reference comparison for locally runnable embedding models on:

-   32GB RAM
-   RTX 5070-class GPU (16GB VRAM)
-   FP16 inference
-   Proper batching
-   Dense embedding output

Throughput estimates are sustained production estimates.

------------------------------------------------------------------------

## Long-Context Embedding Models (8K--32K)

Best suited for: - Large document chunks - Chapter-level embeddings -
Retrieval over long documents

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Model                   Country   License    Max       Native Dim       Optimization       Docs/min (256)  Docs/min   Canonical Link
                                               Context                                                       (4096)     
  ----------------------- --------- ---------- --------- ---------------- ------------------ --------------- ---------- ----------------------------------------------------------------
  Qwen3-Embedding 0.6B    China     Apache 2.0 32K       1024 (MRL)       Retrieval +        7,000--10,000   10--35     https://huggingface.co/Qwen/Qwen3-Embedding-0.6B
                                                                          similarity                                    

  Qwen3-Embedding 4B      China     Apache 2.0 32K       2560 (MRL)       Retrieval-strong   1,800--3,000    3--12      https://huggingface.co/Qwen/Qwen3-Embedding-4B

  Qwen3-Embedding 8B      China     Apache 2.0 32K       4096 (MRL)       Retrieval-heavy    700--1,200      1--4       https://huggingface.co/Qwen/Qwen3-Embedding-8B

  jina-embeddings-v4      Germany   Qwen       32K       Variable (MRL)   Retrieval + doc    3,500--6,000    8--25      https://huggingface.co/jinaai/jina-embeddings-v4
                                    Research                              matching                                      
                                    License                                                                             

  jina-embeddings-v3      Germany   Apache 2.0 8192      1024             General +          6,000--9,500    10--40     https://huggingface.co/jinaai/jina-embeddings-v3
                                                                          retrieval                                     

  BGE-M3                  China     MIT        8192      1024             Hybrid (dense +    9,000--13,000   20--60     https://huggingface.co/BAAI/bge-m3
                                                                          sparse)                                       

  GTE-multilingual-base   China     Apache 2.0 8192      768              Retrieval          9,500--14,000   20--70     https://huggingface.co/Alibaba-NLP/gte-multilingual-base

  Snowflake               USA       Apache 2.0 8192      1024             Retrieval          7,000--10,000   15--50     https://huggingface.co/Snowflake/snowflake-arctic-embed-l-v2.0
  Arctic-Embed-L-v2.0                                    (compressible)                                                 
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

------------------------------------------------------------------------

## High-Speed Multilingual Models (Shorter Context)

Best suited for: - Sentence-level similarity - Clustering - Concept
geometry - Query embeddings

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Model                   Country         License     Max Context      Native   Optimization    Docs/min (256)   Canonical Link
                                                                       Dim                                       
  ----------------------- --------------- ----------- ---------------- -------- --------------- ---------------- -------------------------------------------------------
  multilingual-e5-large   International   MIT         512              1024     Similarity +    12,000--18,000   https://huggingface.co/intfloat/multilingual-e5-large
                                                                                retrieval                        

  LaBSE                   USA             Apache 2.0  \~256--512       768      Sentence        15,000--21,000   https://huggingface.co/sentence-transformers/LaBSE
                                                                                similarity                       

  LASER encoders          USA             BSD-style   Sentence-level   1024     Cross-lingual   18,000--24,000   https://github.com/facebookresearch/LASER
                                                                                similarity                       
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------

------------------------------------------------------------------------

## Language Coverage

All listed models: - Claim 70+ languages or are based on multilingual
backbones - Suitable for Latvian, English, Russian, German - Runnable
locally on mid-tier hardware

Some (Qwen3) explicitly list Latvian.

------------------------------------------------------------------------

## Choosing by Use Case

### Retrieval over large documents

-   BGE-M3
-   Qwen3-Embedding (0.6B / 4B)
-   GTE-multilingual-base

### Clustering / Concept Graphs / PCA

-   multilingual-e5-large
-   BGE-M3
-   LaBSE

### Chapter-Level Embeddings

-   Qwen3-Embedding 0.6B
-   jina-embeddings-v4

------------------------------------------------------------------------

This repository is intended for empirical benchmarking and
experimentation across multilingual embedding spaces.
