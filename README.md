# AskYourGov — RAG Q&A on Public Government Data (LangChain + LangGraph)

A production‑style Retrieval‑Augmented Generation (RAG) system that answers natural‑language questions about public government programs, taxes, benefits, housing, immigration, and regulations across countries.

**Why this project?**
- Non‑niche domain, data is open and abundant.
- RAG is the #1 enterprise LLM pattern.
- Demonstrates modern LLM engineering: LangChain, LangGraph, observability, evals, hybrid retrieval, and source grounding.

---

## ✨ Features
- Multi-country loaders (UK, EU, US, DE) from official portals.
- Robust chunking + **hybrid retrieval** (sparse BM25 + dense embeddings).
- Optional **contextual compression** + **LLM reranking** for higher precision.
- LangGraph workflow (Retrieve → Grade → Generate → Guardrails).
- Source‑grounded answers with confidence + citations.
- Streamlit UI + LangServe API.
- LangSmith traces and dataset evals.

---

## 🌍 Open Data Sources
Start with one, add more later:
- UK (gov.uk): https://www.gov.uk/  (sitemap: https://www.gov.uk/sitemap.xml)
- EU (Your Europe): https://europa.eu/youreurope/
- Germany (Make it in Germany): https://www.make-it-in-germany.com/en/
- US (Benefits.gov): https://www.benefits.gov/

> Tip: Begin with **gov.uk**. It’s well-structured, stable, and highly searchable.

---

## 🧱 Architecture (high level)

```mermaid
flowchart LR
    U[User Question] --> R[Retriever: BM25 + Embeddings]
    R --> C[Contextual Compression / Rerank]
    C --> G[Generator (GPT-4o)]
    G --> V[Answer Validator / Hallucination Guard]
    V -->|needs more| R
    V --> A[Final Answer + Citations]
