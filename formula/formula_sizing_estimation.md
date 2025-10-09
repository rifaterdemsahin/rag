# Index Size Estimation

This document provides a formula and an estimation for the size of the `faiss_index.bin` file as the number of documents grows.

## Sizing Formula

The size of the FAISS index is primarily determined by two factors:

1.  **The number of documents** you are indexing.
2.  **The dimensionality of the vector embeddings** produced by the language model.

The model used in this project (`all-MiniLM-L6-v2`) produces a vector of **384 dimensions** for each document. Each dimension is stored as a 32-bit floating-point number, which takes up **4 bytes**.

Therefore, the size of a single vector is:
`384 dimensions * 4 bytes/dimension = 1536 bytes`

The total index size will be the sum of all vectors plus a small amount of overhead for the index structure itself.

The formula can be approximated as:
`Estimated Size = (Number of Documents * Size per Vector) + Overhead`

## Estimation Based on Current Size

We can perform a linear extrapolation based on the current index size to get a practical estimate.

-   **Current Number of Documents:** 11
-   **Current Index Size:** 17,074 bytes

First, we calculate the average size per document in the current index:
`Average Size per Document = 17,074 bytes / 11 documents ≈ 1552 bytes/document`

This is very close to the theoretical vector size of 1536 bytes, with the small difference being the FAISS overhead.

## Estimated Size for 20,000 Documents

Now, we can use this average to estimate the size for 20,000 documents:

-   **Target Number of Documents:** 20,000
-   **Estimated Size (in bytes):** `20,000 documents * 1552 bytes/document = 31,040,000 bytes`

To make this number easier to read, we can convert it to megabytes (MB):

-   **Estimated Size (in MB):** `31,040,000 bytes / (1024 * 1024) ≈ 29.6 MB`

So, for 20,000 markdown documents, you can expect the `faiss_index.bin` file to be approximately **30 MB**.


---

