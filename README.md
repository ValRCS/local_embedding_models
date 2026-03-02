# local_embedding_models
Research and Prototypes of local embeddings

## Multilingual Embedding Models -- Local Comparison (March 2026)

Hardware assumptions: - 32GB RAM - RTX 5070-class GPU with 16GB VRAM -
FP16 inference - Proper batching - Dense embedding output only

Throughput values are realistic sustained production estimates for
256-token and 4096-token chunks.

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Model                   Canonical Link                                                   Org         Country         License     Lang Coverage  Max Context      Native Dim       Output Types   Primary            Docs/min (256)   Docs/min
                                                                                                                                                                                                   Optimization                        (4096)
  ----------------------- ---------------------------------------------------------------- ----------- --------------- ----------- -------------- ---------------- ---------------- -------------- ------------------ ---------------- ----------
  Qwen3-Embedding 0.6B    https://huggingface.co/Qwen/Qwen3-Embedding-0.6B                 Qwen        China           Apache 2.0  100+ (explicit 32K              1024 (MRL        Dense          Retrieval +        7,000--10,000    10--35
                                                                                           (Alibaba)                               LV)                             adjustable)                     similarity                          

  Qwen3-Embedding 4B      https://huggingface.co/Qwen/Qwen3-Embedding-4B                   Qwen        China           Apache 2.0  100+ (explicit 32K              2560 (MRL        Dense          Retrieval-strong   1,800--3,000     3--12
                                                                                           (Alibaba)                               LV)                             adjustable)                                                         

  Qwen3-Embedding 8B      https://huggingface.co/Qwen/Qwen3-Embedding-8B                   Qwen        China           Apache 2.0  100+ (explicit 32K              4096 (MRL        Dense          Retrieval-heavy    700--1,200       1--4
                                                                                           (Alibaba)                               LV)                             adjustable)                                                         

  jina-embeddings-v4      https://huggingface.co/jinaai/jina-embeddings-v4                 Jina AI     Germany         Qwen        30+ (LV        32K              Variable (MRL)   Dense +        Retrieval + doc    3,500--6,000     8--25
                                                                                                                       Research    included)                                        multi-vector   matching                            
                                                                                                                       License                                                                                                         

  jina-embeddings-v3      https://huggingface.co/jinaai/jina-embeddings-v3                 Jina AI     Germany         Apache 2.0  30+ (LV        8192             1024             Dense          General            6,000--9,500     10--40
                                                                                                                                   supported)                                                      embedding +                         
                                                                                                                                                                                                   retrieval                           

  BGE-M3                  https://huggingface.co/BAAI/bge-m3                               BAAI        China           MIT         100+           8192             1024             Dense +        Hybrid retrieval   9,000--13,000    20--60
                                                                                                                                                                                    sparse +                                           
                                                                                                                                                                                    multi-vector                                       

  GTE-multilingual-base   https://huggingface.co/Alibaba-NLP/gte-multilingual-base         Alibaba NLP China           Apache 2.0  70+            8192             768              Dense + sparse Retrieval          9,500--14,000    20--70

  Snowflake               https://huggingface.co/Snowflake/snowflake-arctic-embed-l-v2.0   Snowflake   USA             Apache 2.0  Multilingual   8192             1024             Dense (MRL)    Retrieval          7,000--10,000    15--50
  Arctic-Embed-L-v2.0                                                                                                                                              (compressible)                                                      

  multilingual-e5-large   https://huggingface.co/intfloat/multilingual-e5-large            intfloat    International   MIT         100            512              1024             Dense          Similarity +       12,000--18,000   N/A
                                                                                                                                                                                                   retrieval                           

  LaBSE                   https://huggingface.co/sentence-transformers/LaBSE               Google      USA             Apache 2.0  109+           \~256--512       768              Dense          Sentence           15,000--21,000   N/A
                                                                                           Research                                                                                                similarity                          

  LASER encoders          https://github.com/facebookresearch/LASER                        Meta AI     USA             BSD-style   200+           Sentence-level   1024             Dense          Cross-lingual      18,000--24,000   N/A
                                                                                                                                                                                                   similarity                          
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

