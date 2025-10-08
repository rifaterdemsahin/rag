# Index Size Estimation for Different Embedding Models

The size of the vector database is directly proportional to the dimensionality of the embedding model used. A model with more dimensions can capture more nuance but will result in a larger index file.

This document compares several popular embedding models and estimates the index size for a collection of **20,000 documents**.

## Sizing Formula

The calculation remains the same across all models. We assume each dimension is a 32-bit float (4 bytes).

1.  **Size per Vector (Bytes)** = `Model Dimensions` * `4`
2.  **Total Estimated Size (Bytes)** = `Size per Vector` * `20,000`

## Model Comparison

| Model Name                  | Type          | Dimensions | Size per Vector (Bytes) | Est. Size for 20k Docs (MB) | Notes                                           |
| --------------------------- | ------------- | ---------- | ----------------------- | --------------------------- | ----------------------------------------------- |
| **all-MiniLM-L6-v2**        | Text          | **384**    | 1,536                   | **~29.6 MB**                | The current model. Balanced speed and performance. |
| **nomic-embed-text-v1.5**   | Text          | **768**    | 3,072                   | ~58.6 MB                    | High-performance open model. Larger context.    |
| **text-embedding-ada-002**  | Text          | **1536**   | 6,144                   | ~117.2 MB                   | Popular proprietary model from OpenAI.          |
| **CLIP-ViT-B-32**           | Image & Text  | **512**    | 2,048                   | ~39.1 MB                    | Multimodal. Can embed both text and images.     |

---

### Analysis

-   **`all-MiniLM-L6-v2` (Current Model):**
    -   At **384 dimensions**, it provides the smallest index size in this list, making it a great choice for local, memory-constrained applications.
    -   **Calculation**: `384 * 4 * 20,000 = 30,720,000 bytes ≈ 29.3 MB`

-   **`nomic-embed-text-v1.5`:**
    -   This model has **768 dimensions**, double that of MiniLM. Consequently, the index size also doubles. It is a strong open-source contender known for high performance on leaderboards.
    -   **Calculation**: `768 * 4 * 20,000 = 61,440,000 bytes ≈ 58.6 MB`

-   **`text-embedding-ada-002` (OpenAI):**
    -   With **1536 dimensions**, this model produces a significantly larger index. It's a powerful model but would require roughly 4x the storage space of our current setup.
    -   **Calculation**: `1536 * 4 * 20,000 = 122,880,000 bytes ≈ 117.2 MB`

-   **`CLIP-ViT-B-32` (Multimodal):**
    -   This model is interesting because it can create embeddings for both text and images in the same vector space, enabling cross-modal search (e.g., search for an image using a text description).
    -   At **512 dimensions**, its storage footprint is quite manageable, falling between MiniLM and Nomic.
    -   **Calculation**: `512 * 4 * 20,000 = 40,960,000 bytes ≈ 39.1 MB`

## Conclusion

Choosing an embedding model is a trade-off between performance, resource consumption (CPU/RAM), and storage space. While larger models often provide better accuracy, smaller models like `all-MiniLM-L6-v2` are ideal for local, efficient semantic search applications like this one. If multimodal search is a requirement, a model like CLIP offers that capability with a modest increase in index size.

---

## Specific Use Case: 15,000 Multimodal Documents

Let's estimate the index size for a specific real-world scenario:

-   **Total Documents:** 15,000 items
-   **Content Mix:** 7,500 markdown files (text) and 7,500 images.
-   **Total Raw Data Size:** 15 GB

To handle both text and images, a multimodal model is essential. We will use **`CLIP-ViT-B-32`** for this calculation.

-   **Model:** `CLIP-ViT-B-32`
-   **Dimensions:** 512
-   **Size per Vector:** 2,048 bytes (512 * 4)

### Estimated Index Size Calculation

`Total Estimated Size = 15,000 documents * 2,048 bytes/document = 30,720,000 bytes`

Converting this to megabytes:

`30,720,000 bytes / (1024 * 1024) ≈ 29.3 MB`

### Conclusion for Use Case

For a collection of **15,000 documents** (half text, half images), the vector index file (`faiss_index.bin`) would be approximately **29.3 MB**.

It is important to note that the **15 GB raw size** of the source documents does not affect the size of the *vector index*. The index size is determined purely by the number of items and the dimensionality of the embedding model.
