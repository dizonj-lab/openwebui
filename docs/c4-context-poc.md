``` mermaid
C4Context
title Kusinaku Local AI Assistant with RAG - System Context (C4)

Person(staff, "Kusinaku LAN User", "Staff using a phone/tablet/laptop on the local network to ask questions and get grounded answers.")

System_Boundary(lan, "Kusinaku LAN") {
  System(userDevice, "Staff Device", "Browser on phone/tablet/laptop connected to Kusinaku LAN.")
  System(aiServer, "AI Server (Physical Machine)", "On-prem machine hosting Docker containers for the AI assistant.")
}

System_Boundary(stack, "Docker Stack on AI Server") {

  System(webui, "OpenWebUI (Docker Container)", "Chat UI accessed by staff via browser.")

  System(api, "RAG Gateway API (Docker Container)", "FastAPI tool server for safe analytics and retrieval orchestration.")

  SystemDb(pg, "Postgres (Docker Container)", "Structured data store for Kusinaku facts (sales + leftovers).")

  SystemDb(vec, "Postgres + pgvector (Docker Container)", "Vector store for embeddings and RAG chunk metadata.")

  System_Boundary(ollamaBoundary, "Ollama Runtime (Docker Container)") {
      System(ollama, "Ollama Runtime", "Local LLM runtime service.")
      System(model, "Llama3.2 Foundational Model", "Chat model used for reasoning and responses.")
      System(embed, "Embeddings Model", "Generates embeddings for RAG retrieval.")
  }
}

System_Ext(dataFiles, "CSV Data Files", "pos_sales_data.csv, leftovers.csv")

System(ingest, "CSV Ingestion Job", "Normalizes CSV data, loads Postgres facts, builds chunks, generates embeddings.")

Rel(staff, userDevice, "Uses")
Rel(userDevice, webui, "Accesses via HTTP/HTTPS over LAN")

Rel(webui, api, "Sends chat requests and tool/RAG calls to")
Rel(api, pg, "Runs read-only analytics queries against")
Rel(api, vec, "Performs semantic retrieval against")
Rel(api, ollama, "Requests chat completions and embeddings from")

Rel(ollama, model, "Hosts")
Rel(ollama, embed, "Hosts")

Rel(dataFiles, ingest, "Provided to")
Rel(ingest, pg, "Loads normalized fact data into")
Rel(ingest, vec, "Stores chunks and embeddings into")
Rel(ingest, embed, "Uses for vector generation")

Rel(aiServer, webui, "Hosts")
Rel(aiServer, api, "Hosts")
Rel(aiServer, pg, "Hosts")
Rel(aiServer, ollama, "Hosts")
```
