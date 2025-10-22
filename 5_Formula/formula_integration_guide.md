# Formula: Integrating Semantic Search into AI Chat Queries

This document provides a step-by-step guide on how to port the existing semantic search functionality to a new project and integrate it as a Retrieval Augmented Generation (RAG) component for AI-based chat queries.

## 1. Understanding the Core Components

The semantic search system relies on three main components:
-   **Sentence Transformer Model**: Converts text (documents and queries) into numerical vector embeddings.
-   **FAISS Index**: Stores these embeddings and allows for fast similarity search.
-   **File Paths Mapping**: A simple text file (`filepaths.txt`) that maps the index IDs back to their original document paths.

## 2. Step-by-Step Integration Guide

### Step 2.1: Copy Core Files to Your New Project

Start by copying the essential files from this project into your new AI chat project's directory structure.

1.  **`index.py`**: This script is used to build or update your vector index.
2.  **`search.py`**: This script contains the logic for performing a semantic search. We will modify this to be a reusable function.
3.  **`requirements.txt`**: This file lists all necessary Python dependencies.
4.  **`docs/` folder**: Create a `docs/` folder in your new project and place all your markdown documents (or any other text-based documents you want to search) inside it.

### Step 2.2: Install Dependencies

Navigate to your new project's root directory in your terminal and install the required Python packages. It's highly recommended to use a virtual environment.

```bash
# Create a virtual environment (if you haven't already)
python3 -m venv venv_chat_project

# Activate the virtual environment
source venv_chat_project/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### Step 2.3: Initial Indexing of Your Documents

Before you can search, you need to create the FAISS index and the file paths map for your documents.

```bash
# Run the indexer (assuming your documents are in ./docs)
python3 index.py --folder ./docs
```

This will generate `faiss_index.bin` and `filepaths.txt` in your project's root directory. These files will be used by your chat application.

### Step 2.4: Modify `search.py` for Programmatic Access

To integrate the search functionality into your chat application, you'll want to call it as a function rather than running it as a standalone script.

**Conceptual Change to `search.py`:**

```python
# /path/to/your/new_project/search_module.py (or similar)

import numpy as np
import faiss
from sentence_transformers import SentenceTransformer
import os # Added for path joining

# Global variables to load resources once
_index = None
_filepaths = None
_model = None

def _load_resources():
    """Loads FAISS index, file paths, and sentence transformer model."""
    global _index, _filepaths, _model
    if _index is None:
        print("Loading FAISS index from 'faiss_index.bin'...")
        _index = faiss.read_index('faiss_index.bin')
    if _filepaths is None:
        print("Loading file paths from 'filepaths.txt'...")
        with open('filepaths.txt', 'r', encoding='utf-8') as f:
            _filepaths = [line.strip() for line in f.readlines()]
    if _model is None:
        print("Loading sentence transformer model...")
        _model = SentenceTransformer('all-MiniLM-L6-v2')

def semantic_search(query_text: str, k: int = 5) -> list[tuple[str, float]]:
    """
    Performs a semantic search and returns a list of (filepath, distance) tuples.
    """
    _load_resources() # Ensure resources are loaded

    query_embedding = _model.encode([query_text], convert_to_tensor=False)
    query_embedding = np.array(query_embedding).astype('float32')

    distances, indices = _index.search(query_embedding, k)

    results = []
    if len(indices[0]) > 0:
        for i, idx in enumerate(indices[0]):
            if idx < len(_filepaths):
                results.append((_filepaths[idx], distances[0][i]))
            else:
                print(f"Warning: Index {idx} is out of bounds for filepaths list.")
    return results

# The original main() function can be removed or kept for standalone testing
# if __name__ == "__main__":
#     # ... original main() logic ...
```

### Step 2.5: Integrate with Your AI Chat Query Logic (RAG Pattern)

Now, in your main AI chat application script (e.g., `chat_app.py`), you can import and use the `semantic_search` function. This implements a basic Retrieval Augmented Generation (RAG) pattern.

```python
# /path/to/your/new_project/chat_app.py

from search_module import semantic_search # Assuming you saved the modified search.py as search_module.py
import os

# Placeholder for your AI model interaction (e.g., OpenAI, Gemini API)
def get_ai_response(prompt: str) -> str:
    # This is where you would call your AI model API
    # Example: response = openai.Completion.create(engine="text-davinci-003", prompt=prompt, max_tokens=150)
    # For demonstration, we'll just echo the prompt
    return f"AI Response (based on context):\n{prompt}\n---"

def chat_with_rag(user_query: str):
    print(f"User: {user_query}")

    # 1. Retrieve relevant documents
    search_results = semantic_search(user_query, k=3) # Get top 3 relevant docs

    context_text = ""
    if search_results:
        print("\nRetrieving context from relevant documents:")
        for filepath, distance in search_results:
            print(f"- {filepath} (Distance: {distance:.4f})")
            try:
                with open(filepath, 'r', encoding='utf-8') as f:
                    context_text += f.read() + "\n\n---\n\n" # Append document content
            except Exception as e:
                print(f"Could not read {filepath}: {e}")
    else:
        print("No relevant documents found for context.")

    # 2. Augment the prompt with retrieved context
    if context_text:
        prompt = (
            f"Based on the following context, answer the user's question:\n\n"
            f"Context:\n{context_text}\n\n"
            f"User Question: {user_query}\n\n"
            f"Answer:"
        )
    else:
        prompt = f"User Question: {user_query}\n\nAnswer:"

    # 3. Generate response using the AI model
    ai_response = get_ai_response(prompt)
    print(f"\nAI: {ai_response}")

if __name__ == "__main__":
    # Example usage
    chat_with_rag("what is semantic search?")
    print("\n" + "="*50 + "\n")
    chat_with_rag("tell me about databases")
    print("\n" + "="*50 + "\n")
    chat_with_rag("who is mehmet?")
```

### Step 2.6: Run Your Chat Application

```bash
# Make sure your virtual environment is active
source venv_chat_project/bin/activate

# Run your chat application
python3 chat_app.py
```

This setup allows your AI chat queries to first retrieve relevant information from your local markdown documents, and then use that information to provide more accurate and context-aware responses.
