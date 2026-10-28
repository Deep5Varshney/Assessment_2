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

3. import chromadb
from rdflib import Graph, Literal, Namespace, RDF, RDFS, URIRef
from sentence_transformers import SentenceTransformer

# 1. Build a basic RDF Knowledge Graph using rdflib
g = Graph()
EX = Namespace("http://example.org/")

alice = EX.Alice
bob = EX.Bob
acme = EX.AcmeCorp

# Add sample RDF triples
g.add((alice, RDF.type, EX.Person))
g.add((alice, EX.knows, bob))
g.add((bob, EX.worksAt, acme))
g.add((bob, RDF.type, EX.Person))

# 2. Convert RDF triples into simple text sentences
sentences = []
for s, p, o in g:
  s_name = s.split("/")[-1]
  p_name = p.split("/")[-1]
  o_name = o.split("/")[-1] if isinstance(o, URIRef) else str(o)

  # Form readable sentence format
  sentence = f"{s_name} {p_name} {o_name}"
  sentences.append(sentence)

print("Generated RDF Sentences:")
for s in sentences:
  print("-", s)

# 3. Embed text sentences and store in ChromaDB
client = chromadb.Client()
kg_collection = client.get_or_create_collection(name="knowledge_graph_search")

model = SentenceTransformer("all-MiniLM-L6-v2")
embeddings = model.encode(sentences).tolist()

ids = [f"triple_{i}" for i in range(len(sentences))]
kg_collection.add(documents=sentences, embeddings=embeddings, ids=ids)


# 4. Accept a user query and return relevant text from stored embeddings
def query_knowledge_graph(query_text):
  query_embedding = model.encode([query_text]).tolist()
  results = kg_collection.query(query_embeddings=query_embedding, n_results=1)
  return results["documents"][0][0]


# --- Test Run ---
user_query = "Who does Alice know?"
print(f"\nQuery: {user_query}")
print(f"Retrieved Answer: {query_knowledge_graph(user_query)}")
