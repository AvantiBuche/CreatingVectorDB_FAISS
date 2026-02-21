# CreatingVectorDB_FAISS and ChromaDB
Extract PDF file data and to create a vector DataBase using **FAISS**

## Summary
A Vector Database stores data as embeddings (vectors) instead of normal rows/columns

## Code
Text → Embedding Model → Vector → Store in Vector DB ----
User Query → Embedding → Similarity Search → Return Top Matches

## How it Works
| Step | What Happens                       |
| ---- | ---------------------------------- |
| 1    | Text converted to embeddings       |
| 2    | Stored as high-dimensional vectors |
| 3    | Query converted to vector          |
| 4    | Nearest neighbor search performed  |
| 5    | Most similar documents returned    |

## Steps

1. install faiss
2. install pypdf
   - Pypdf is used to extract the data from pdf file
3. import pandas and numpy
4. import PdfReader from pypdf
5. define file path and extract data
6. install and import sent_tokenize from nltk
   - for chunking paragraphs to sentences
8. import SentenceTransformer
   - Load embedding model to convert text to vector
9. print shape of vector embeddings
10. import FAISS
    - create vector database using faiss
11. perform similar search with Query and customize results using top K
    
