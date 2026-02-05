# Knowledge Graph Architecture

## Overview

The **Big Book of Computing** is structured as a **hierarchical tree embedded within a richly connected graph**. This architecture enables both linear pedagogical learning paths and exploratory knowledge discovery across the entire computational domain.

## Graph Structure

### Dual Nature: Tree + Graph

The knowledge graph maintains two complementary structures:

1. **Tree Backbone** — A strict hierarchical organization for pedagogical flow
2. **Cross-Connections** — Thousands of edges linking related concepts across the tree

```
Root (Big Book of Computing)
│
├─ Volume I: Foundations
│  ├─ Chapter 1: Numerical Methods
│  │  ├─ Section 1.1: Root Finding
│  │  │  ├─ Subsection 1.1.1: Newton-Raphson Method
│  │  │  │  ├─ 📄 Text: Algorithm Description
│  │  │  │  ├─ 📊 Figure: Convergence Plot
│  │  │  │  ├─ 💻 Code: Python Implementation
│  │  │  │  ├─ ❓ Quiz: Complexity Analysis
│  │  │  │  └─ 📝 Note: Practical Considerations
│  │  │  └─ Subsection 1.1.2: Bisection Method
│  │  └─ Section 1.2: Integration
│  └─ Chapter 2: Linear Algebra
│
├─ Volume II: Simulation
├─ Volume III: Optimization & ML
└─ Volume IV: Quantum Computing
```

## Node Classification

### Hierarchy Levels

| Level | Type | Count | Purpose | Example |
|-------|------|-------|---------|---------|
| 0 | Root | 1 | Entry point | Big Book of Computing |
| 1 | Volume | 4 | Top-level organization | Volume I: Foundations |
| 2 | Chapter | ~60 | Major topic areas | Numerical Methods |
| 3 | Section | ~400 | Subtopics | Root Finding |
| 4 | Subsection | ~1,200 | Detailed concepts | Newton-Raphson Method |
| 5 | Leaf | ~13,000 | Content atoms | Text, Code, Figures, etc. |

**Total Tree Depth:** 5 levels  
**Total Nodes:** 14,678

### Leaf Node Types

Leaf nodes represent atomic content units. Each subsection contains multiple leaf nodes of different types:

| Icon | Type | Purpose | Count |
|------|------|---------|-------|
| 📄 | **Text** | Explanations, derivations, intuition | ~6,000 |
| 📊 | **Figure** | Plots, visualizations, diagrams | ~2,500 |
| 💻 | **Code** | Runnable implementations (Python, JAX, etc.) | ~1,526 |
| ❓ | **Question** | Practice problems, quizzes | ~534 |
| 📝 | **Note** | Insights, warnings, best practices | ~1,800 |
| 🔗 | **Reference** | Citations, external links, papers | ~640 |

## Edge Taxonomy

### 1. Hierarchical Edges (Parent-Child)

**Purpose:** Define the tree structure  
**Direction:** Unidirectional (parent → child)  
**Count:** ~14,674 (one per non-root node)

```
Volume I → Chapter 1 → Section 1.1 → Subsection 1.1.1 → Text Node
```

**Properties:**
- `edge_type`: `"parent_child"`
- `weight`: 1.0 (immutable)
- `pedagogical_order`: integer (defines sibling sequence)

### 2. Prerequisite Edges

**Purpose:** Define learning dependencies ("learn X before Y")  
**Direction:** Unidirectional (prerequisite → dependent)  
**Count:** ~8,200

**Examples:**
- `Linear Algebra → Eigenvalue Problems`
- `Newton's Method → Optimization Algorithms`
- `ODEs → Molecular Dynamics`

**Properties:**
- `edge_type`: `"prerequisite"`
- `strength`: `"required" | "recommended" | "helpful"` (enum)
- `justification`: text explanation

### 3. Related Concept Edges

**Purpose:** "See also" connections across the graph  
**Direction:** Bidirectional  
**Count:** ~12,000

**Examples:**
- `FFT ↔ Quantum Fourier Transform`
- `Monte Carlo Integration ↔ Quantum Monte Carlo`
- `Gradient Descent ↔ Variational Quantum Eigensolver`

**Properties:**
- `edge_type`: `"related"`
- `relationship`: `"analogous" | "generalizes" | "special_case" | "complements"`
- `cross_volume`: boolean (true if connecting different volumes)

### 4. Application Edges

**Purpose:** Connect theory to practice/applications  
**Direction:** Unidirectional (theory → application)  
**Count:** ~5,800

**Examples:**
- `Laplace Equation → Electrostatics Simulation`
- `Eigenvalue Decomposition → PCA`
- `Hamiltonian Simulation → Drug Discovery`

**Properties:**
- `edge_type`: `"application"`
- `domain`: `"physics" | "finance" | "biology" | "chemistry" | "general"`
- `practical_importance`: float [0.0, 1.0]

### 5. Research Frontier Edges

**Purpose:** Link established content to cutting-edge research  
**Direction:** Unidirectional (foundation → frontier)  
**Count:** ~2,000

**Examples:**
- `Quantum Gates → NISQ Algorithms for Chemistry`
- `Graph Neural Networks → Protein Folding`
- `Simulated Annealing → Quantum Annealing`

**Properties:**
- `edge_type`: `"research"`
- `maturity`: `"active_research" | "emerging" | "established"`
- `arxiv_refs`: list of arXiv identifiers
- `last_updated`: timestamp

## Graph Statistics

### Connectivity Metrics

- **Total Nodes:** 14,678
- **Total Edges:** ~28,000
  - Hierarchical (parent-child): ~14,674
  - Cross-connections: ~13,326
- **Average Node Degree:** 3.8 (including hierarchical edges)
- **Average Cross-Connection Degree:** 1.9 (excluding parent-child edges)
- **Graph Diameter:** ~14 (max shortest path between any two nodes)
- **Clustering Coefficient:** 0.31 (moderate clustering)

### Volume Distribution

| Volume | Chapters | Sections | Subsections | Leaf Nodes |
|--------|----------|----------|-------------|------------|
| I: Foundations | 17 | 102 | 340 | ~3,800 |
| II: Simulation | 14 | 98 | 310 | ~3,200 |
| III: Optimization & ML | 15 | 112 | 320 | ~3,600 |
| IV: Quantum | 14 | 88 | 230 | ~2,400 |

## Multi-Agent Graph Construction

### Agent Roles in Graph Building

#### 1. Research Agents
**Graph Operations:**
- Scan external sources (arXiv, PubMed, CrossRef)
- Identify new concepts → propose new nodes
- Detect relationships → suggest new edges

**Output:** Candidate nodes and edges (unapproved)

#### 2. Concept Extraction Agents
**Graph Operations:**
- Parse research papers
- Extract entities (equations, algorithms, concepts)
- Build local subgraphs from each paper

**Output:** Entity subgraphs for integration

#### 3. Graph Architect Agents
**Graph Operations:**
- Design global tree structure (levels 0-4)
- Assign nodes to hierarchy positions
- Enforce tree constraints (single parent, depth limits)
- Optimize branching factor for pedagogical flow

**Output:** Complete hierarchical tree (parent-child edges)

#### 4. Content Generation Agents
**Graph Operations:**
- Create leaf nodes (level 5)
- Populate node content (text, code, figures)
- Generate multi-modal representations

**Output:** Populated leaf nodes attached to subsections

#### 5. Knowledge Weaving Agents
**Graph Operations:**
- Identify prerequisite relationships → create prerequisite edges
- Find conceptual analogies → create related edges
- Connect theory to applications → create application edges
- Link to research frontiers → create research edges

**Output:** Cross-connection edges (non-hierarchical)

#### 6. Quality Assurance Agents
**Graph Operations:**
- Validate node content for correctness
- Check edge validity (no cycles in prerequisite DAG)
- Verify cross-references point to existing nodes
- Enforce schema constraints

**Output:** Validation reports, corrected edges

#### 7. Update & Versioning Agents
**Graph Operations:**
- Monitor research feeds for new content
- Identify affected nodes when concepts evolve
- Incrementally add new nodes and edges
- Maintain version snapshots of graph state

**Output:** Graph deltas and version tags

## Graph Traversal Algorithms

### 1. Linear Learning Path (DFS on Tree)

**Purpose:** Generate a sequential reading order for a volume

```python
def generate_learning_path(start_volume):
    path = []
    def dfs(node):
        path.append(node)
        for child in sorted(node.children, key=lambda c: c.pedagogical_order):
            dfs(child)
    dfs(start_volume)
    return path
```

### 2. Prerequisite-Aware Path (Topological Sort)

**Purpose:** Find optimal learning order respecting prerequisites

```python
def prerequisite_aware_path(target_concept):
    # Build prerequisite DAG
    prereq_graph = build_prereq_subgraph(target_concept)
    # Topological sort
    return topological_sort(prereq_graph)
```

### 3. Concept Similarity Search (BFS with Edge Weights)

**Purpose:** Find related concepts for "see also" suggestions

```python
def find_related_concepts(concept, max_distance=2):
    visited = {concept}
    related = []
    queue = [(concept, 0)]
    
    while queue:
        node, dist = queue.pop(0)
        if dist == max_distance:
            continue
        for neighbor in node.related_edges:
            if neighbor not in visited:
                visited.add(neighbor)
                related.append((neighbor, dist + 1))
                queue.append((neighbor, dist + 1))
    
    return sorted(related, key=lambda x: x[1])
```

### 4. Application Discovery (Edge Type Filtering)

**Purpose:** Find practical applications of a theory node

```python
def find_applications(theory_node, domain=None):
    applications = []
    for edge in theory_node.outgoing_edges:
        if edge.edge_type == "application":
            if domain is None or edge.domain == domain:
                applications.append(edge.target)
    return applications
```

## Schema Definition

### Node Schema

```json
{
  "node_id": "string (UUID)",
  "node_type": "root | volume | chapter | section | subsection | leaf",
  "leaf_type": "text | figure | code | question | note | reference",
  "title": "string",
  "content": "object (varies by leaf_type)",
  "parent_id": "string (UUID) | null",
  "children_ids": ["string (UUID)"],
  "pedagogical_order": "integer",
  "metadata": {
    "created_at": "timestamp",
    "last_updated": "timestamp",
    "agent_author": "string",
    "version": "string"
  }
}
```

### Edge Schema

```json
{
  "edge_id": "string (UUID)",
  "source_id": "string (UUID)",
  "target_id": "string (UUID)",
  "edge_type": "parent_child | prerequisite | related | application | research",
  "properties": "object (varies by edge_type)",
  "metadata": {
    "created_at": "timestamp",
    "agent_author": "string",
    "justification": "string"
  }
}
```

## Version Control & Updates

### Version Strategy

The graph uses **semantic versioning** with snapshots:

- **Major versions** (e.g., v2.0.0) — Significant restructuring of hierarchy
- **Minor versions** (e.g., v1.3.0) — New chapters or major content additions
- **Patch versions** (e.g., v1.2.7) — Leaf node updates, bug fixes, new cross-connections

### Incremental Updates

When new research appears:

1. **Update Agents** scan the affected region of the graph
2. Identify nodes requiring content updates
3. Create **graph delta** (added/modified/removed nodes and edges)
4. Apply delta with rollback capability
5. Publish new patch version

### Graph Integrity Constraints

- **Tree Constraint:** Every non-root node has exactly one parent
- **Depth Constraint:** Maximum tree depth is 5
- **Cycle Constraint:** Prerequisite edges must form a DAG (no cycles)
- **Reference Constraint:** All edge endpoints must exist
- **Orphan Constraint:** All nodes must be reachable from root

## Example Graph Queries

### Query 1: Find all prerequisites for learning Quantum ML

```cypher
MATCH path = (start)-[:PREREQUISITE*]->(target)
WHERE target.title = "Quantum Machine Learning"
RETURN path
ORDER BY length(path) DESC
```

### Query 2: Find cross-volume connections from Volume I to Volume IV

```cypher
MATCH (v1:Volume {number: 1})-[*]->(n1)-[r:RELATED|APPLICATION]-(n2)<-[*]-(v4:Volume {number: 4})
WHERE r.cross_volume = true
RETURN n1, r, n2
```

### Query 3: What applications exist in biology for SVD?

```cypher
MATCH (svd:Subsection {title: "Singular Value Decomposition"})-[a:APPLICATION]->(app)
WHERE a.domain = "biology"
RETURN app
```

## Graph Storage & Deployment

### Storage Options

1. **Neo4j** — Native graph database with Cypher query language
2. **NetworkX** — Python library for in-memory graph operations
3. **JSON Export** — Flat-file representation for git versioning

### Current Implementation

- **Primary:** JSON files in GitHub repository
- **Query Layer:** Python scripts using NetworkX
- **Visualization:** Mermaid diagrams in markdown

### Future Enhancements

- Migrate to Neo4j for production-scale queries
- Build interactive graph explorer web UI
- Enable community contributions to cross-connections
- Machine learning for automatic edge suggestion

---

**Document Version:** 1.0.0  
**Last Updated:** February 2026  
**Maintained by:** Graph Architect Agents
