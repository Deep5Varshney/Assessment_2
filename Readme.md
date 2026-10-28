# Knowledge Graph with Semantic Search and Query Answering

A basic Knowledge Graph built using `rdflib`, converted into natural language sentences, and indexed with `ChromaDB` for semantic search and query answering.

## Features
- **RDF Knowledge Graph:** Constructs an RDF graph containing entities, types, and relationships using `rdflib`.
- **Triple-to-Text Conversion:** Translates RDF triples (Subject-Predicate-Object) into readable natural language sentences.
- **Semantic Indexing:** Embeds the text sentences using Hugging Face's `sentence-transformers` (`all-MiniLM-L6-v2`).
- **Query Answering:** Stores embeddings in `ChromaDB` and performs semantic search to answer natural language queries (e.g., "Who does Alice know?").

## Tech Stack
- Python
- Google Colab
- RDFLib
- ChromaDB
- Sentence Transformers

## How to Run
1. Open Google Colab and create a new notebook.
2. Install dependencies:
   ```bash
   pip install rdflib chromadb sentence-transformers
