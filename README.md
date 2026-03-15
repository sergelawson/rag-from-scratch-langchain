# RAG from Scratch

`RAG from Scratch` is a small retrieval-augmented generation learning project built around LangChain, ChromaDB, and Google Generative AI embeddings. The repo currently centers on a notebook-driven workflow for loading local documents, splitting them into chunks, embedding them, and persisting those embeddings for retrieval.

## What This Repo Contains

- A notebook that explores the end-to-end RAG pipeline: [notebook/document.ipynb](notebook/document.ipynb)
- Sample source documents in [data](data)
- A persisted Chroma vector store in [vector_store](vector_store)
- A minimal Python entry point in [main.py](main.py)

## Current Workflow

The main implementation lives in the notebook and follows this flow:

1. Load local text and PDF documents from the `data/` directory.
2. Split documents into chunks with `RecursiveCharacterTextSplitter`.
3. Generate embeddings with Google Generative AI using `models/gemini-embedding-001`.
4. Store vectors in a persistent ChromaDB collection under `vector_store/`.
5. Retrieve relevant chunks through a small RAG retriever abstraction.

The notebook defines helper classes for:

- `EmbeddingManager`
- `VectorStore`
- `RAGRetriever`

## Project Structure

```text
advanced-rag/
├── data/
│   ├── anthropic_genai.pdf
│   ├── compiler.txt
│   ├── llm.txt
│   └── memory.pdf
├── notebook/
│   └── document.ipynb
├── vector_store/
├── main.py
├── pyproject.toml
├── requirements.txt
└── README.md
```

## Dependencies

The project uses:

- `langchain`
- `langchain-community`
- `langchain-google-genai`
- `langchain-chroma`
- `langchain-text-splitters`
- `chromadb`
- `pypdf`
- `pymupdf`
- `sentence-transformers`
- `faiss-cpu`

Dependency management files are available in [pyproject.toml](pyproject.toml), [requirements.txt](requirements.txt), and [uv.lock](uv.lock).

## Setup

This project requires Python `3.13+`.

Using `uv`:

```bash
uv sync
```

Using `pip`:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Create a `.env` file with your Google API key:

```env
GOOGLE_API_KEY=your_api_key_here
```

## Running The Project

The notebook is the primary interface for the RAG workflow:

```bash
jupyter notebook notebook/document.ipynb
```

The script entry point is currently just a placeholder:

```bash
python main.py
```

## Notes

- The repository already includes a persisted Chroma database in `vector_store/`.
- The notebook uses local files rather than a remote data source.
- `main.py` does not yet expose the notebook workflow as a CLI or app.

## Next Improvements

- Move the notebook classes into reusable Python modules.
- Add a command-line interface for indexing and querying documents.
- Add a generation step on top of retrieval for full question answering.
- Add tests for document loading, chunking, and retrieval behavior.
