# Data

The knowledge base for this demo is a **sample "Retail Operations & ESG Compliance" document** defined inline in the notebook — no proprietary company data is used.

To use your own documents:
1. Drop a `.pdf` or `.txt` file in this folder.
2. Swap the inline text for a LangChain document loader (e.g. `PyPDFLoader`) pointed at the file.
3. Re-run the chunking and embedding cells.

Local knowledge-base files and built FAISS indexes are kept out of git via `.gitignore`.
