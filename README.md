# Multi-Source Document Retrieval with LangChain

A beginner-friendly notebook demonstrating the main stages of a Retrieval-Augmented Generation (RAG) workflow: loading documents, splitting text into chunks, creating embeddings, storing vectors, and retrieving relevant content with similarity search.

## Features

- **Text ingestion** using LangChain's `TextLoader` with a local `speech.txt` file
- **Web ingestion** using `WebBaseLoader` to load content from an article about AI agents
- **PDF ingestion** using `PyPDFLoader` with a local `Outcome.pdf` file
- **Text splitting** using `RecursiveCharacterTextSplitter`
- **Vector storage** using Chroma
- **Alternative vector storage** using FAISS
- **Similarity search** to retrieve document chunks relevant to a query

## Project Workflow

1. Load source content from a text file, web page, or PDF
2. Split the loaded documents into smaller chunks
3. Convert chunks into embeddings using OpenAI embeddings
4. Store the embeddings in Chroma or FAISS
5. Submit a query and retrieve the most relevant chunks

## Requirements

Python 3.10 or later is recommended. The notebook uses these packages:

- `langchain`
- `langchain-community`
- `langchain-openai`
- `langchain-text-splitters`
- `faiss-cpu`
- `chromadb`
- `python-dotenv`
- `beautifulsoup4`
- `pypdf`

## Installation

Install the dependencies in Google Colab or your Python environment:

```bash
pip install -U langchain langchain-community langchain-openai langchain-text-splitters faiss-cpu chromadb python-dotenv beautifulsoup4 pypdf
```

In Google Colab, use `%pip install` in a code cell instead of `pip` if needed.

## API Key Setup

The notebook uses OpenAI embeddings, which require an OpenAI API key and available API billing.

For Google Colab, the safer option is to store the key in **Secrets** under the name `OPENAI_API_KEY`, enable notebook access, and load it like this:

```python
import os
from google.colab import userdata

os.environ["OPENAI_API_KEY"] = userdata.get("OPENAI_API_KEY")
```

Alternatively, for a local environment, put the key in a `.env` file:

```text
OPENAI_API_KEY=your_api_key_here
```

Do not commit `.env` files or API keys to GitHub. If a key has been exposed, revoke it and create a new one.

## Input Files

Place these files in the notebook's working directory before running the relevant cells:

- `speech.txt` — used by the text-file loader
- `Outcome.pdf` — used by the PDF loader

The notebook also loads an example article from the web, so an internet connection is required for that step.

## Example Query

The notebook currently tests similarity search with:

```python
query = "show me the table of contents"
```

Change the query to ask about the contents of the documents you loaded.

## Important Notes

- The notebook currently contains an older text-splitter import. For current LangChain packages, use:

  ```python
  from langchain_text_splitters import RecursiveCharacterTextSplitter
  ```

- For current OpenAI embedding integrations, prefer:

  ```python
  from langchain_openai import OpenAIEmbeddings
  ```

- The notebook creates Chroma and FAISS indexes from the first 40 document chunks. This is a demonstration; increase or change the selected documents as needed.
- The local filenames `speech.txt` and `Outcome.pdf` must exist, or their loader cells will fail.
- This notebook demonstrates document retrieval and similarity search. It does not yet implement a complete RAG answer-generation chain that passes retrieved context to a chat model.

## Running the Notebook

1. Open `rag.ipynb` in Google Colab or Jupyter.
2. Install the dependencies.
3. Configure your OpenAI API key securely.
4. Upload `speech.txt` and `Outcome.pdf` if you intend to run those cells.
5. Run the notebook cells in order and test similarity search.

## Learning Outcomes

By completing this notebook, you will practise the core stages of document ingestion and vector retrieval used in RAG applications, and compare two vector stores: Chroma and FAISS.
