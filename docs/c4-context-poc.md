```mermaid
Staff Browser
  ↓
OpenWebUI (Chat UI)
  ↓  (chat + RAG retrieval requests)
RAG Gateway / API (FastAPI “tool server”)
  ↓                    ↘
Postgres (Sales tables)  Postgres + pgvector (Embeddings store)
  ↑
CSV Ingestion Job (pos_sales_data.csv, leftovers.csv → normalize → load)
  ↓
Ollama (llama3.2 for chat + embeddings model)

  ```
