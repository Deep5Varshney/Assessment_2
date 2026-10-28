## Repository 2: Knowledge Graph Semantic Search (`knowledge-graph-semantic-search`)

### 1. Create a file named `README.md` with this content:
```markdown
# Knowledge Graph with Semantic Search and Query Answering

A basic Knowledge Graph built using `rdflib`, converted into natural language sentences, and indexed with `ChromaDB` for semantic search.

## Features
- **RDF Knowledge Graph:** Constructs an RDF graph containing entities, types, and relationships using `rdflib`.
- **Triple-to-Text Conversion:** Translates RDF triples (Subject-Predicate-Object) into readable natural language sentences.
- **Semantic Indexing:** Embeds the sentences using `sentence-transformers` and stores them in `ChromaDB`.
- **Query Answering:** Performs semantic search against natural language user queries (e.g., *"Who does Alice know?"*).

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
