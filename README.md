# Generative AI Corporate Q&A: Retrieval-Augmented Generation (RAG)

## Executive Summary
In large retail and corporate environments, critical operational knowledge is often buried within hundreds of pages of static PDF documents, employee handbooks, and ESG (Environmental, Social, and Governance) compliance reports. Manually searching for this information costs thousands of hours in lost productivity.

This project develops a **Retrieval-Augmented Generation (RAG) pipeline** designed to act as an internal AI knowledge assistant. 

**Commercial Objective:** Enable retail operations and corporate compliance teams to instantly query internal company documents using natural language. The system retrieves the exact relevant paragraphs and uses them as context to generate accurate, hallucination-free answers, drastically improving operational efficiency and policy adherence.

## Technical Stack
* **Language:** Python
* **LLM Framework:** LangChain
* **Vector Database:** FAISS (Facebook AI Similarity Search)
* **Embeddings:** HuggingFace (`sentence-transformers/all-MiniLM-L6-v2`)
* **Data Processing:** Recursive Character Text Splitting

## Core Methodology
1. **Document Ingestion & Chunking:** Ingests a simulated "Omnichannel Retail Operations & ESG Policy" document. Uses LangChain's `RecursiveCharacterTextSplitter` to break the massive text into semantic, overlapping chunks to preserve context.
2. **Vector Embeddings:** Utilises an open-source HuggingFace embedding model to translate human text into high-dimensional mathematical vectors, capturing the true semantic meaning of the sentences.
3. **Vector Store Creation:** Builds a local FAISS vector database to store and index the embeddings for hyper-fast semantic search.
4. **Retrieval Engine:** When a user asks a question, the engine converts the query into a vector, calculates the cosine distance against the database, and retrieves the top 3 most relevant corporate policy chunks to answer the question.
