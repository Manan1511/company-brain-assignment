# Graph Database (Neo4j)

> Component Report for Company Brain Architecture

## Proposed Technology

**Neo4j**

---

# 1. What Does This Component Do?

The graph database is the **relationship backbone** of the GraphRAG pipeline.

While a vector database answers:

> "What is similar?"

a graph database answers:

> "What is connected?"

It stores and traverses the network of relationships between entities across the system.

## Pipeline Flow

```text
User Query
    ↓
Embedding
    ↓
Vector Search
    ↓
Relevant Nodes
    ↓
Graph Expansion
    ↓
Context Assembly
    ↓
LLM
```

After vector search identifies semantically relevant nodes, the graph database expands outward through relationships to assemble richer context for the LLM.

---

## Nodes

The graph stores typed entities representing real-world objects:

- Employee
- Repository
- Issue
- Pull Request
- Technology
- Document
- Slack Thread
- Figma Design

---

## Relationships

Edges represent meaningful interactions and dependencies.

Examples:

- `AUTHORED`
- `WORKS_ON`
- `OWNS`
- `USES`
- `DEPENDS_ON`
- `CREATED`
- `REVIEWED`
- `COMMENTED_ON`
- `REFERENCES`

---

## Directed Graphs

Most relationships are directional because direction carries semantic meaning.

### Correct

```text
Rahul ──WORKS_ON──▶ Auth Service
```

Meaning:

> Rahul is working on Auth Service

### Incorrect

```text
Auth Service ──WORKS_ON──▶ Rahul
```

This direction does not make semantic sense.

---

## Graph Expansion

Once vector retrieval surfaces a relevant node, graph traversal expands the context.

Example:

```text
JWT Design Doc
        │
        ▼
   AUTHORED_BY
        │
        ▼
      Rahul
```

```text
JWT Design Doc
        │
        ▼
    REFERENCES
        │
        ▼
   Auth Service
```

A single retrieved document can automatically bring:

- The author
- Related services
- Connected repositories
- Relevant technologies

This context would not be available from vector search alone.

---

## Temporal Graphs

Relationships can contain time-based metadata.

Example:

```text
Rahul ──WORKS_ON──▶ Auth Service

start: 2025
end:   2026
```

This enables time-aware questions:

### Current Knowledge

```text
Who knows Auth today?
```

Returns only currently active contributors.

### Historical Knowledge

```text
Who knew Auth three years ago?
```

Returns historical contributors using temporal relationships.

---

## Inferred Relationships

The graph can derive implicit connections from existing edges.

### Existing Relationships

```text
Rahul ──WORKS_ON──▶ Auth

Auth ──USES──▶ JWT
```

### Inferred Relationship

```text
Rahul ──RELATED_TO──▶ JWT
```

No additional data ingestion is required.

---

## Edge Metadata

Relationships can store structured metadata.

Example:

```json
{
  "relation": "WORKS_ON",
  "confidence": 0.95,
  "timestamp": "2026-05-30",
  "source": "github"
}
```

Benefits:

- Auditability
- Confidence scoring
- Traceability
- Source attribution

---

# 2. Why Neo4j?

Neo4j is the most mature and widely adopted graph database.

It uses **Cypher**, a query language designed specifically for graph traversal, and supports the **Property Graph Model** required for this architecture.

### Key Reasons

- Native graph storage
- Purpose-built graph traversal engine
- Expressive Cypher query language
- Strong ecosystem support
- Production-grade clustering and replication
- Managed cloud offering through AuraDB

### Ecosystem

Supported integrations include:

- Node.js
- Python
- Java
- LangChain
- LlamaIndex

---

# 3. Advantages

### Relationship-First Queries

Multi-hop traversals are fast by design and avoid expensive SQL joins.

### Richer Context

Graph expansion provides context beyond what vector retrieval alone can offer.

### Temporal Intelligence

Time-aware edges enable historical and current-state reasoning.

### Inferred Knowledge

New insights emerge naturally through traversal paths.

### Human-Friendly Querying

Cypher queries map closely to how humans think about relationships.

Example:

> "Who worked on X with Y?"

### Complements Vector Search

The graph database is not a replacement for vector search.

| Vector Search | Graph Database |
|--------------|---------------|
| What matters? | What is connected? |
| Semantic similarity | Relationship traversal |
| Retrieves relevant content | Expands relevant context |

### Key Insight

> Vector search identifies what matters.  
> Graph traversal discovers what else is connected.  
> Both layers are necessary.

---

# 4. Limitations

### Operational Complexity

Graph schemas require careful upfront design and migrations can be difficult.

### Dependency on Entity Extraction

Poor entity extraction produces poor relationships and weakens traversal quality.

### Not Ideal for Analytics

Graph databases are not optimized for large-scale aggregate workloads such as:

- SUM
- AVG
- COUNT across massive datasets

A data warehouse is better suited for those tasks.

### Relationship Maintenance

Confidence-scored and inferred relationships require ongoing maintenance to prevent stale or inaccurate knowledge.

### Learning Curve

Teams unfamiliar with:

- Cypher
- Graph modeling
- Traversal patterns

will require onboarding time.

---

# 5. Would You Use It in Company Brain?

## Yes.

The graph database is a core component of Company Brain.

Employees, repositories, services, projects, and documents are inherently interconnected.

A vector database can identify relevant documents, but it cannot answer questions like:

- Who authored this document?
- What service does it reference?
- Is the author still active on this project?
- Is the information still current?

Neo4j enables traversal-based context expansion.

Example:

```text
Retrieved Document
        ↓
Author
        ↓
Current Projects
        ↓
Related Services
        ↓
Recent Activity
```

The resulting context is significantly more useful for an LLM than isolated documents.

### Temporal Knowledge Matters

One of the hardest challenges in institutional knowledge systems is distinguishing between:

```text
Who knows this today?
```

and

```text
Who knew this years ago?
```

Without temporal relationships, outdated expertise can easily be surfaced as current knowledge.

Neo4j provides a natural solution through temporal graph modeling.

---

# 6. References

- Neo4j Documentation  
  https://neo4j.com/docs/

- Neo4j AuraDB  
  https://neo4j.com/cloud/platform/aura-graph-database/

- Cypher Query Language Reference  
  https://neo4j.com/developer/cypher/

- GraphRAG: From Local to Global (Microsoft Research, 2024)

- LangChain Neo4j Integration  
  https://python.langchain.com/docs/integrations/graphs/neo4j_cypher/

- Property Graph Model Overview  
  https://neo4j.com/developer/graph-database/
