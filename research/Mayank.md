-Component
Vector Database

-Proposed Technology
Qdrant

-What does this component do?
The Vector Database is responsible for storing and searching embeddings like high-dimensional numerical representations of meaning derived from text like Slack discussions, PR descriptions, incident reports, architecture docs, and migration RFCs.

In Company Brain, when human-written content is processed by the Semantic Intelligence Layer, it gets converted into embedding vectors. These vectors are stored in Qdrant along with metadata payloads. When a developer asks a question, the query is converted into an embedding and Qdrant retrieves the semantically closest stored content, even if the exact words don't match.

This powers the Hybrid Retrieval Engine, enabling semantic search to work alongside keyword search and graph traversal.
Why did you choose this technology?
Qdrant is a Rust-based, high-performance vector database that offers superior scalability and efficiency, making it well suited for RAG systems and AI agents. Since Company Brain will continuously ingest events and serve real-time queries, low-latency retrieval is critical.
Qdrant supports named vectors, allowing a collection to hold both a dense HNSW index and a sparse inverted index. Qdrant handles IDF computation server-side, which means it can do semantic + keyword search natively and directly matching what the project needs in its Hybrid Retrieval Engine.
Qdrant offers fast filtered search with excellent metadata filtering, making it the best balance of performance and cost for most mid-scale RAG applications. This is essential for scoping queries by service, team, date range, or source platform.
Qdrant can be self-hosted via Docker or Kubernetes, which aligns with the project's security philosophy, sensitive engineering data like incident reports and architecture discussions never needs to leave your own infrastructure.


-Advantages
Qdrant uses Hierarchical Navigable Small World (HNSW) graphs for efficient Approximate Nearest Neighbor search with low latency and high recall.
You can filter by metadata while simultaneously running vector similarity, very important for scoped retrieval in Company Brain.
Qdrant runs bare-metal, in Kubernetes, or on Qdrant Cloud, making it easy to start locally during development and scale to production.
The Maximal Marginal Relevance feature helps return diverse results rather than near-duplicate chunks, crucial when retrieving from many Slack threads or PRs that discuss the same topic.

-Limitations
Distributed mode requires careful shard planning, and RBAC (Role-Based Access Control) is enterprise-only. The access control at the vector DB level is limited unless you build it in the application layer.
Where Qdrant handles systems like Milvus are routinely deployed at hundreds of millions to billions of vectors. 
Unlike Weaviate, Qdrant doesn't auto-generate embeddings from text. You must generate embeddings externally (e.g., using an embedding model via the Anthropic API or OpenAI) before storing them. This adds an integration step.

-Would you use it in Company Brain?
Yes, I would definitely use this in the system as the Semantic Intelligence Layer needs to store embeddings from Slack messages, PRs, incident reports, migration RFCs, and design documents, retrieving them with both semantic meaning and filtered context. It is open-source and self-hostable, which directly supports the project's security of keeping sensitive engineering data in-house. Its hybrid search (dense + sparse vectors in the same collection) is a direct match to the Hybrid Retrieval Engine described in the project guide. For the scope of this project, Qdrant is the right starting point.

-References
Qdrant Official Documentation 
Vector Databases Compared: Pinecone vs Qdrant vs Weaviate vs Milvus — Let's Data Science 
Qdrant Hybrid Search Docs 
Deep Dive into Qdrant for AI Agents — Sparkco 
