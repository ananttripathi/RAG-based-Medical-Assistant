# RAG-based Medical Assistant

**RAG-based medical Q&A over the Merck Manual (19th ed.) — ChromaDB, GTE-large embeddings, Mistral 7B (GGUF). Local, privacy-first, GPU-accelerated.**

[![Repository](https://img.shields.io/badge/GitHub-RAG--Medical--Assistant-blue)](https://github.com/ananttripathi/RAG-based-Medical-Assistant)

---

## About

This project implements a **Retrieval-Augmented Generation (RAG)** system that gives healthcare professionals instant, contextually accurate access to medical knowledge from the *Merck Manual of Diagnosis and Therapy (19th Edition)*. It reduces information overload and supports clinical decision-making with a local, privacy-first design.

### Key Features

- **Semantic search** — 1024-dimensional vector embeddings (GTE-large) for document retrieval  
- **LLM** — Mistral 7B Instruct v0.2 (GGUF) for answer generation  
- **Knowledge base** — 4,114 pages from the Merck Manual, chunked and indexed in ChromaDB  
- **Evaluation** — Groundedness and relevance checks on responses  
- **Privacy-first** — No external API calls; runs fully on your machine  
- **GPU-friendly** — CUDA acceleration for the language model (38 layers)

---

## Repository Contents

| File | Description |
|------|-------------|
| `RAG_medical_assistant.ipynb` | Jupyter notebook: data load, indexing, RAG pipeline, and evaluation |
| `RAG-Medical-Assistant.html` | Static HTML export of the notebook for viewing in a browser |

---

## Quick Start

```bash
git clone https://github.com/ananttripathi/RAG-based-Medical-Assistant.git
cd RAG-based-Medical-Assistant
pip install -r requirements.txt
```

1. Open `RAG_medical_assistant.ipynb` in Jupyter.
2. Set `merck_pdf_path` to the path of your Merck Manual PDF (or use the Google Drive setup in the notebook).
3. Run all cells. The first run will download the Mistral 7B GGUF model and build the ChromaDB index.

**View the notebook as HTML:**  
- **On GitHub:** [Preview rendered HTML](https://htmlpreview.github.io/?https://github.com/ananttripathi/RAG-based-Medical-Assistant/blob/main/RAG-Medical-Assistant.html)  
- **Locally:** Open `RAG-Medical-Assistant.html` in any modern browser (no server required).

---

## Requirements

- **Python** 3.10 or 3.11  
- **GPU** (optional): CUDA-capable GPU recommended for Mistral 7B; CPU is supported but slower  
- **Merck Manual** — PDF of *Merck Manual of Diagnosis and Therapy (19th Edition)*; update the path in the notebook

### Optional: GPU support for llama-cpp-python

```bash
# CUDA
CMAKE_ARGS="-DLLAMA_CUBLAS=on" pip install llama-cpp-python --force-reinstall --no-cache-dir

# CPU only
CMAKE_ARGS="-DLLAMA_CUBLAS=off" pip install llama-cpp-python --force-reinstall --no-cache-dir
```

---

## System Overview

- **Document load:** PyMuPDFLoader (LangChain)  
- **Chunking:** RecursiveCharacterTextSplitter, 512 tokens, 20 overlap  
- **Embeddings:** thenlper/gte-large (1024 dim)  
- **Vector DB:** ChromaDB (persistent, cosine similarity)  
- **LLM:** Mistral 7B Instruct v0.2, GGUF Q6_K, 2.3k context

Flow: **Query → embed → retrieve top-k chunks from ChromaDB → build context → Mistral generates answer.**

---

## License

This project is licensed under the [MIT License](LICENSE).

---

## Contact

- **Author:** [ananttripathiak](mailto:ananttripathiak@gmail.com)  
- **Repo:** [RAG-based-Medical-Assistant](https://github.com/ananttripathi/RAG-based-Medical-Assistant)

For questions or suggestions, open a [GitHub Issue](https://github.com/ananttripathi/RAG-based-Medical-Assistant/issues).
