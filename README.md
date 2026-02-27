# CreatingVectorDB FAISS, Chroma, Pinecone, Weaviate

## Summary
A Vector Database stores data as embeddings (vectors) instead of normal rows/columns

# FAISS DB

We’ll build a local vector database using:
1. sentence-transformers → to create embeddings
2. faiss → to store & search vectors

Extract PDF file data to create a vector DataBase using **FAISS**

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

# CHROMA DB

When working with huge documents (thousands or millions of chunks) in ChromaDB, giving proper IDs is very important for:

1. Avoiding duplicates
2. Updating specific chunks
3. Tracking document sources
4. Deleting specific documents
5. Production-scale RAG systems

# Why IDs Matter in Large Documents

## In ChromaDB:

Each vector must have a unique ID,
If you reuse an ID → it overwrites existing data,
For huge documents → you need structured ID strategy

## Use Chroma if:

You're building:
1. Startup MVP
2. RAG prototype
3. Local AI tool

You want:
1. Quick setup
2. No cloud dependency
3. Full control
4. Your data size is moderate

# Pinacone DB

Step 1: Create Pinecone Account
1. Go to https://www.pinecone.io
2. Create free account
3. Copy your API key

Step 2: Install SDK
pip install pinecone sentence-transformers

Step 3: (Python file)
1. Initialize Pinecone 
2. Generate Embeddings
3. Insert Vectors (Upsert)
   Each vector needs: id, values (embedding), metadata (optional)
4. Query Pinecone

Working with Large Documents
For huge documents:

1️⃣ Chunk the document
2️⃣ Generate structured IDs

## Architecture 

Client App
   ↓
Embedding Model (OpenAI / SBERT)
   ↓
Pinecone Index (Cloud)
   ↓
Top-K Results
   ↓
LLM (GPT / Claude / etc.)

## Use Pinecone if:

You're building:
1. Production SaaS
2. Multi-user system
3. Enterprise AI app

You expect:
1. Millions of vectors
2. High traffic
3. Low latency
4. You don't want to manage infrastructure

# Weaviate DB

Weaviate is an open-source AI-native vector database that:
1. Stores objects (like a normal DB)
2. Automatically generates embeddings (optional)
3. Performs vector similarity search
4. Supports hybrid search (keyword + semantic)
5. Can run locally OR in managed cloud

Think of it as:

PostgreSQL + Vector Search + AI modules combined

| Concept       | Meaning                                     |
| ------------- | ------------------------------------------- |
| Collection    | Like a table                                |
| Object        | Like a row                                  |
| Vector        | Embedding representation                    |
| Schema        | Defines structure                           |
| Hybrid Search | BM25 + Vector combined                      |
| Modules       | Built-in vectorizers (OpenAI, Cohere, etc.) |

Data → (Optional Auto-Embedding) → Stored as Object + Vector
Query → Vectorized → Similarity Search → Results

App

 ↓
 
Weaviate

   ↳
   
   Object Storage
   
   ↳
   
   Vector Index (HNSW)
   
   ↳
   
   Hybrid Search Engine
   
   ↳
   
   AI Modules

Step 1: Run Weaviate

Option 1 — Use Weaviate Cloud (Recommended)
1. Create account at https://weaviate.io
2. Create cluster
3. Get:
URL,
API key

Option 2 — Run Locally (Docker)

docker run -p 8080:8080 semitechnologies/weaviate:latest

Step 2: Install Python Client

pip install weaviate-client

Step 3: Python
1. Connect to Weaviate
2. Create a Collection (Schema)
3. Insert data
4. Perform Vector Search

### Hybrid Search (Major Advantage)
Hybrid = Keyword + Vector

Use Weaviate if:
1. You need hybrid search
2. You want built-in embedding modules
3. You want schema control
4. You may self-host
5. You need graph-style object relations

# FAISS VS Chroma VS Pinecone

| Feature          | FAISS  | Chroma | Pinecone |
| ---------------- | ------ | ------ | -------- |
| Local            | ✅      | ✅      | ❌        |
| Cloud Managed    | ❌      | ❌      | ✅        |
| Production Scale | Medium | Medium | High     |
| Easy Setup       | Medium | Easy   | Easy     |
| Enterprise Ready | ❌      | ❌      | ✅        |

# FAISS VS Chroma

| Feature           | **FAISS**              | **ChromaDB**                |
| ----------------- | ---------------------- | --------------------------- |
| Type              | Vector search library  | Full vector database        |
| Developed by      | Meta (Facebook)        | Open-source startup project |
| Storage           | In-memory (by default) | Persistent storage          |
| Metadata support  | ❌ No built-in          | ✅ Yes                       |
| Filtering         | ❌ Not native           | ✅ Yes                       |
| API simplicity    | Low-level              | High-level                  |
| Production ready? | Needs infra setup      | Easier for RAG apps         |
| Best for          | Pure similarity search | LLM / RAG applications      |

# Chroma VS Pinecone

| Feature        | **ChromaDB**                        | **Pinecone**                              |
| -------------- | ----------------------------------- | ----------------------------------------- |
| Type           | Open-source vector database         | Managed cloud vector database             |
| Hosting        | Local / self-hosted                 | Fully managed (cloud)                     |
| Setup          | Very easy                           | Easy but cloud-based                      |
| Scaling        | Limited (single machine)            | Massive scale (millions/billions vectors) |
| Dev Experience | Very LLM-friendly                   | Enterprise-ready                          |
| Best for       | Prototypes, MVPs, small-medium apps | Production SaaS, large-scale systems      |

🟢 Chroma = Developer-Friendly Local Vector DB
🌲 Pinecone = Scalable Managed Cloud Vector DB

| Feature                   | Chroma  | Pinecone |
| ------------------------- | ------- | -------- |
| Metadata filtering        | ✅       | ✅        |
| Persistence               | ✅       | ✅        |
| Horizontal scaling        | ❌       | ✅        |
| Distributed               | ❌       | ✅        |
| GPU indexing              | ❌       | Managed  |
| Multi-tenant (namespaces) | Basic   | Advanced |
| SLA                       | ❌       | ✅        |
| Enterprise security       | Limited | Advanced |

| Scale          | Chroma                | Pinecone          |
| -------------- | --------------------- | ----------------- |
| < 100K vectors | ✅ Excellent           | ✅                 |
| 1M vectors     | ⚠️ Depends on machine | ✅ Smooth          |
| 10M+ vectors   | ❌ Hard                | ✅ Designed for it |
| 100M+          | ❌                     | ✅                 |

|             | Chroma              | Pinecone           |
| ----------- | ------------------- | ------------------ |
| Cost        | Free (self-hosted)  | Paid (usage-based) |
| Infra cost  | Your server cost    | Included           |
| Maintenance | Your responsibility | Managed            |

# Pinecone VS Weaviate

| Feature                       | Pinecone        | Weaviate            |
| ----------------------------- | --------------- | ------------------- |
| Managed Cloud                 | ✅ Yes           | ✅ Yes               |
| Open Source                   | ❌               | ✅                   |
| Self-hosted                   | ❌               | ✅                   |
| Hybrid Search (BM25 + Vector) | Basic filtering | ✅ Native            |
| Graph-like relations          | ❌               | ✅                   |
| Auto-embedding                | ❌               | ✅ Built-in modules  |
| Massive scale                 | ✅ Excellent     | ✅ Good              |
| Dev simplicity                | Very simple     | Moderate complexity |

|                  | Pinecone      | Weaviate                 |
| ---------------- | ------------- | ------------------------ |
| Infra management | Fully managed | Optional                 |
| Cost model       | Usage-based   | Usage-based or self-host |
| Control          | Limited       | High                     |



    
