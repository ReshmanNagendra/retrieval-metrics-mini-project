# Retrieval Metrics Evaluation: Keyword vs Semantic Search

## Results Table

| Query | Keyword rank | Semantic rank |
|---|---|---|
| my redis cache keeps showing old data | 8 | 1 |
| how do I add semantic search to a table I already have | miss | 2 |
| redis or memcached for caching | 1 | 2 |
| why did my query get slower after I added an index | miss | 1 |
| what does ACID actually guarantee | 2 | 1 |
| how do I keep my postgres online while changing the schema | 6 | 3 |
| my background jobs stop after every deploy | miss | 2 |
| how do I let my database accept more writes per second | 4 | 1 |
| sql or nosql for a new product | 1 | 3 |
| why does my redis memory keep climbing | miss | 2 |
| **Summary** | **MRR 0.30 · Recall@10 0.60** | **MRR 0.67 · Recall@10 1.00** |

## Findings and Interpretation

Overall, semantic search significantly outperforms keyword search on both evaluated metrics, achieving an MRR of 0.67 compared to keyword search's 0.30, and a perfect Recall@10 of 1.00 versus 0.60. Keyword search performed best on explicit, comparative queries involving rare or specific technical keywords ("redis or memcached for caching" at rank 1 vs rank 2, and "sql or nosql for a new product" at rank 1 vs rank 3), where users supplied the exact terms present in the indexed posts. In contrast, semantic search dominated across natural-language queries, symptom descriptions, and troubleshooting questions (such as "why did my query get slower after I added an index" and "my background jobs stop after every deploy"), which completely missed the top 10 under keyword search. Even though semantic search delivers a much higher overall score, an engineering team would still keep keyword search in production because each system wins on fundamentally different query types; combining both into a hybrid search system (such as BM25 + pgvector via Reciprocal Rank Fusion) provides higher retrieval performance and coverage than either individual system alone.
