# How to Run This Project

This document provides a step-by-step formula for setting up and using the markdown semantic search tool.

## 1. Setup the Environment

First, you need to create a Python virtual environment to keep the project's dependencies isolated.

```bash
# Create the virtual environment
python3 -m venv venv
```

## 2. Activate the Environment

Before you can install packages or run the scripts, you must activate the virtual environment.

```bash
# Activate the virtual environment
source venv/bin/activate
```
*Your terminal prompt should now be prefixed with `(venv)`.*

## 3. Install Dependencies

Install all the required Python packages using the `requirements.txt` file.

```bash
# Install dependencies
pip install -r requirements.txt
```

## 4. Add Your Markdown Files

Place any markdown (`.md`) files you want to search through into the `docs/` directory. You can create subdirectories if you wish.

## 5. Index Your Files

Run the `index.py` script to process your markdown files and create the local vector database. This only needs to be done once, or whenever you add, remove, or modify your markdown files.

```bash
# Index the files in the 'docs' folder
python3 index.py --folder ./docs
```

This will create two files in your project root: `faiss_index.bin` and `filepaths.txt`.

## 6. Perform a Semantic Search

Now you can use the `search.py` script to find relevant documents. Replace `"your query here"` with the topic you're interested in.

```bash
# Run a search
python3 search.py --query "your query here"
```

### Example Search

```bash
python3 search.py --query "what is semantic search"
```

## 7. Deactivate the Environment (Optional)

When you are finished working on the project, you can deactivate the virtual environment.

```bash
# Deactivate the environment
deactivate
