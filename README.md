# Enterprise RAG Knowledge Assistant — Retrieval Engine

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![LangChain](https://img.shields.io/badge/LangChain-RAG-1C3C3C)
![FAISS](https://img.shields.io/badge/Vector%20DB-FAISS-4B8BBE)
![Embeddings](https://img.shields.io/badge/Embeddings-MiniLM--L6--v2-orange)
![Status](https://img.shields.io/badge/Status-Retrieval%20complete%20%7C%20Generation%20planned-yellow)

A semantic-search knowledge assistant that lets staff query internal policy documents in plain English and returns the most relevant passages — the **retrieval layer** that grounds a Retrieval-Augmented Generation (RAG) system.

> **Scope note (read this first):** this notebook implements the **retrieval half** of RAG — document chunking, embeddings, a FAISS vector index, and semantic search. It returns the exact source passages for a query. It does **not** yet call an LLM to generate a written answer; that generation step is scoped in the roadmap below. The naming and claims here reflect that honestly.

---

## The problem
In large retail/corporate environments, operational knowledge is buried across long policy handbooks and ESG compliance documents. Keyword search (`Ctrl+F`) fails when staff don't use the document's exact wording. Semantic retrieval matches on *meaning* instead.

## How it works
1. **Chunking** — a policy document is split with LangChain's `RecursiveCharacterTextSplitter` (300-char chunks, 50-char overlap) so context isn't cut mid-sentence.
2. **Embeddings** — each chunk is encoded with the open-source `sentence-transformers/all-MiniLM-L6-v2` model into a dense vector.
3. **Vector index** — vectors are stored in a local **FAISS** index for fast similarity search.
4. **Semantic retrieval** — a user query is embedded and compared by cosine distance; the top-k most relevant passages are returned with their source.

## Tech Stack
Python · LangChain · FAISS · HuggingFace `sentence-transformers` · Recursive character chunking

## About the source document
The knowledge base is a **sample "Retail Operations & ESG Compliance" document** written for this demo, so no proprietary company data is exposed. The pipeline is document-agnostic — point it at a real PDF/handbook and it works unchanged.

---

## Repository Structure
```
├── README.md
├── requirements.txt
├── notebooks/
│   └── enterprise_rag_knowledge_assistant.ipynb
├── src/
├── data/          # drop your own .pdf / .txt knowledge base here
├── images/
└── docs/
```

## How to Run
```bash
git clone https://github.com/kndukuba17-hub/Generative-AI-RAG-Pipeline.git
cd Generative-AI-RAG-Pipeline
pip install -r requirements.txt
jupyter notebook notebooks/enterprise_rag_knowledge_assistant.ipynb
```
The first run downloads the MiniLM embedding model (a few hundred MB). Runs on Jupyter or Google Colab.

## Roadmap (to make this a full RAG system)
- **Generation step:** inject retrieved chunks into an LLM prompt (e.g. an open model via HuggingFace, or the Claude/OpenAI API) so the assistant returns a written, cited answer.
- **Real documents:** load actual PDFs with a document loader instead of the sample handbook.
- **Evaluation:** add retrieval metrics (hit-rate / MRR) on a small labelled question set.
- **Guardrails:** return "not found in the documents" when no chunk clears a similarity threshold, to reduce ungrounded answers.
