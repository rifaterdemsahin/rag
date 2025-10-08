# Gemini - Markdown Semantic Search

This project is designed to read all markdown files from a specified folder, process their content, and build a local vector database. This database enables powerful semantic search capabilities, allowing users to find relevant information based on the meaning and context of their queries, rather than just keyword matching.

## Features

*   **Markdown File Ingestion:** Automatically reads and parses all `.md` files in a given directory.
*   **Vector Database Creation:** Generates vector embeddings for the content of the markdown files and stores them locally.
*   **Semantic Search:** Provides a search interface to query the vector database and retrieve the most relevant documents based on semantic similarity.

## How it Works

1.  **File Discovery:** The tool scans a target folder for all markdown files.
2.  **Content Extraction:** It extracts the text content from each file.
3.  **Vectorization:** Each piece of content is converted into a numerical vector representation using a pre-trained language model.
4.  **Indexing:** The vectors are stored in a local vector database (e.g., ChromaDB, FAISS) for efficient searching.
5.  **Querying:** When a user enters a search query, the query is also converted into a vector. The system then finds the vectors in the database that are closest to the query vector, returning the most semantically similar documents.

## Getting Started

### Setting Up Virtual Environment

Before installing dependencies, it's recommended to create a virtual environment to isolate project dependencies:

**On Windows:**
```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
venv\Scripts\activate
```

**On macOS/Linux:**
```bash
# Create virtual environment
python3 -m venv venv

# Activate virtual environment
source venv/bin/activate
```

### Installation and Usage

1.  **Installation:** `pip install -r requirements.txt`
2.  **Indexing:** `python index.py --folder ./docs`
3.  **Searching:** `python search.py --query "your search query"`

### Deactivating Virtual Environment

When you're done working on the project, you can deactivate the virtual environment:

```bash
deactivate
