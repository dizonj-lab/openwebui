# OpenWebUI Quick PoC
# 
# Kusinaku Local AI Assistant (PoC)

Local AI assistant powered by OpenWebUI + Ollama + Llama3.2, grounded using Kusinaku operational data (sales + leftovers).

---

## 1. Purpose

This project demonstrates a **local, practical AI interface** for operational use.

The immediate goal:

- Provide staff with a ChatGPT-like interface
- Ground responses using real business data
- Validate architecture patterns quickly

---

## 2. Disclaimer

This is **not** a comprehensive or authoritative architecture document.

This project is:

- research
- design exploration
- proof of concept
- implementation experiment

Inspired by:

- consulting-style architecture practices
- AI engineers, architects, and researchers publishing patterns and papers
- enterprise environments with overlapping AI initiatives

Sometimes large organizations resemble blind men trying to describe an elephant.

This PoC was completed in **less than 24 hours using a laptop**.

---

## 3. Overview

### What it does

- Local ChatGPT-like interface
- Answers grounded in Kusinaku data
- Supports analytics + RAG-style retrieval

### Data Sources

- `pos_sales_data.csv`
- `leftovers.csv`

---

## 4. Architecture (High-Level)

> Local-first design with enterprise evolution in mind.

### System Context Diagram

## 5. Core Components

### OpenWebUI
- Staff-facing chat interface
- Local ChatGPT-like experience
- Runs inside Docker
- Acts as the human interaction layer

### RAG Gateway API (FastAPI Tool Server)
- Controlled access layer between AI and data
- Executes safe analytics queries
- Handles retrieval orchestration
- Future governance and guardrail point

### Postgres (Sales + Leftovers)
- Structured operational data
- Source of truth for analytics
- Supports SQL-based grounding

### Postgres + pgvector
- Stores embeddings and RAG chunks
- Enables semantic retrieval
- Keeps vector search close to data

### Ollama Runtime
- Local LLM inference engine
- Hosts foundational model and embeddings model

### Llama3.2 (Foundational Model)
- Primary reasoning and response generation
- Local and private execution

### CSV Ingestion Job
- Reads sales and leftovers CSV files
- Normalizes schema
- Loads facts into Postgres
- Generates chunks and embeddings

---

## 6. Why This PoC Exists (Rationale)

Most AI initiatives start with large-scale architecture discussions and complex tooling.

This PoC intentionally starts small:

- prove value quickly
- validate architecture patterns
- keep control over complexity
- demonstrate practical grounding of AI responses

Core belief:

> Architecture clarity before scale.

---

## 7. How It Works (Data Flow)

1. CSV files are ingested.
2. Data is normalized and loaded into Postgres.
3. Chunking creates retrieval-ready summaries.
4. Embeddings are generated via Ollama.
5. Staff interacts using OpenWebUI.
6. Requests go through the Tool API.
7. API performs:
   - SQL analytics queries
   - Vector retrieval (RAG)
8. Llama3.2 generates grounded responses.

---

## 8. Quick Start (Local)

### Start the stack

(In-progress)
