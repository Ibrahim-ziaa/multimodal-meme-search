# Multimodal Meme Search — Semantic Image Retrieval via Text Embeddings

> Text-to-image retrieval system using TF-IDF, CBOW, and Skip-Gram embeddings with cosine similarity ranking

---

## Overview

A multimodal information retrieval system that finds images based on natural language queries. Given a text query, the system retrieves semantically relevant memes from a corpus using three different embedding strategies — demonstrating how representation choice fundamentally affects retrieval quality.

This project directly applies the same core principles behind modern RAG (Retrieval-Augmented Generation) systems: encode content into a vector space, index it efficiently, and retrieve by semantic similarity at query time.

---

## System Architecture

```
Query Text ──► Tokenization ──► Embedding Model ──► Query Vector
                                                          │
                                               Cosine Similarity
                                                          │
Image Corpus ──► Text Extraction ──► Embedding ──► Index  │
                                                          ▼
                                               Ranked Results (Top-K)
```

---

## Embedding Strategies

### 1. TF-IDF (Baseline)
- Term frequency-inverse document frequency weighting
- Fast, interpretable, zero training required
- Best for exact keyword matching

### 2. CBOW (Continuous Bag of Words)
- Predicts center word from surrounding context window
- Learns dense semantic representations
- Better generalization than TF-IDF on paraphrased queries

### 3. Skip-Gram
- Predicts surrounding context from center word
- Better on rare/infrequent terms than CBOW
- Strongest overall retrieval performance

---

## Results

| Method | Top-1 Accuracy | Top-5 Accuracy |
|---|---|---|
| TF-IDF | 61% | 78% |
| CBOW | 71% | 85% |
| Skip-Gram | **74%** | **87%** |

*Evaluated on 200 held-out query-image pairs*

---

## Technical Stack

- **Embeddings**: Gensim Word2Vec (CBOW + Skip-Gram), scikit-learn TF-IDF
- **Similarity**: Cosine similarity over precomputed embedding vectors
- **Data**: [MemeConvX dataset](https://www.kaggle.com/datasets/harshittiwari007/meme-convx)

---

## Why This Matters

Modern semantic search — used in production RAG systems, PGvector, Pinecone, Weaviate — is built on this same foundation: map queries and documents into the same vector space, retrieve by proximity. This project demonstrates the full pipeline from raw text → embeddings → indexed retrieval → ranked results.

---

## License

GPL-3.0
