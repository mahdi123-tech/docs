# Open-Source Alternatives to Cosmograph for Graph Analytics

## What Is Cosmograph?

[Cosmograph](https://cosmograph.app) is a GPU-accelerated graph visualization tool built on their open-source library `@cosmograph/cosmos`. Key characteristics:

- **GPU-powered force layout** (WebGL compute shaders for force simulation)
- Renders **millions of nodes/edges** in real-time
- Interactive: zoom, pan, select, hover, search
- Node clustering and community detection
- Temporal graph playback (time-based filtering)
- Built-in analytics: degree distribution, centrality, connected components
- Embeddable widget and React wrapper (`@cosmograph/react`)
- Primarily a **hosted SaaS** with a freemium model

The open-source core (`@cosmograph/cosmos`) provides the GPU force layout and WebGL renderer. The analytics features, UI, temporal analysis, and hosted platform are proprietary.

---

## Alternatives Ranked by Feature Parity

### 1. Sigma.js + Graphology + @react-sigma/core (Best Overall Alternative)

| | Cosmograph | Sigma.js + Graphology |
|---|---|---|
| **Stars** | ~1k (cosmos) | 12k (sigma) + 1.6k (graphology) |
| **Rendering** | WebGL (GPU compute) | WebGL |
| **Max nodes** | 1M+ | 100k-500k |
| **Force layout** | GPU-accelerated | ForceAtlas2 (Web Worker) |
| **React wrapper** | @cosmograph/react | @react-sigma/core |
| **Graph algorithms** | Built-in (limited) | Full library (graphology-metrics) |
| **Community detection** | Yes | Louvain (graphology-communities-louvain) |
| **Centrality** | Degree | Degree, betweenness, closeness, eigenvector, PageRank |
| **Shortest path** | No | Dijkstra, BFS, A* |
| **Connected components** | Yes | Yes |
| **Clustering** | Yes | Yes (Louvain, label propagation) |
| **Temporal/timeline** | Yes | Manual (filter by attribute) |
| **Custom node shapes** | Limited | Full (custom WebGL programs) |
| **License** | Proprietary (cosmos: MIT-ish) | MIT |

**Why it wins**: Graphology provides the most comprehensive graph algorithm library in JavaScript. Combined with Sigma's WebGL renderer, you get near-Cosmograph performance with far more analytics capabilities. The ecosystem is mature with 50+ graphology plugins.

```bash
npm install sigma graphology @react-sigma/core
# Layouts
npm install graphology-layout-forceatlas2 graphology-layout-noverlap graphology-layout-circular
# Analytics
npm install graphology-metrics graphology-communities-louvain graphology-shortest-path
npm install graphology-components graphology-generators graphology-traversal
# Utilities
npm install graphology-gexf graphology-graphml  # import/export
```

**Analytics algorithms available via graphology plugins:**

| Category | Algorithms |
|---|---|
| Centrality | degree, betweenness, closeness, eigenvector, PageRank, HITS |
| Community | Louvain, label propagation |
| Components | connected components, strongly connected components |
| Shortest path | Dijkstra, unweighted BFS, A* |
| Metrics | density, diameter, modularity, clustering coefficient |
| Layout | ForceAtlas2, circular, random, noverlap |
| Traversal | BFS, DFS |
| Generators | complete, empty, ladder, path, star, caveman, Erdos-Renyi, Barabasi-Albert |

---

### 2. AntV G6 + Graphin (Best All-in-One Solution)

| | Cosmograph | G6 + Graphin |
|---|---|---|
| **Stars** | ~1k | 12k (G6) + 1k (Graphin) |
| **Rendering** | WebGL | Canvas + WebGL (GPU mode) |
| **Max nodes** | 1M+ | 10k-50k (Canvas), more with WebGL |
| **Force layout** | GPU-accelerated | GPU-accelerated (via @antv/layout-gpu) |
| **React wrapper** | @cosmograph/react | @antv/graphin |
| **Built-in analytics** | Limited | Extensive (@antv/algorithm) |
| **UI components** | Toolbar, search | Toolbar, minimap, context menu, search, legend, tooltip, filter panel |
| **License** | Proprietary | MIT |

**Why it's strong**: G6 is the most feature-complete graph visualization framework. It includes everything out of the box -- layouts, analytics, interactions, plugins -- without needing a separate algorithm library. Graphin adds a React-friendly API on top.

```bash
npm install @antv/g6 @antv/graphin
# GPU layout (for large graphs)
npm install @antv/layout-gpu
# Built-in algorithms
npm install @antv/algorithm
```

**Built-in features that match/exceed Cosmograph:**
- 15+ layout algorithms (force, dagre, radial, concentric, fruchterman, circular, grid, MDS, combo)
- Graph algorithms: shortest path, PageRank, community detection (Louvain, label propagation), connected components, cycle detection, degree centrality
- Combo nodes (grouped sub-graphs, expandable/collapsible)
- Fisheye lens distortion
- Edge bundling
- Minimap, toolbar, context menu, tooltip, legend
- Node/edge state machines (selected, highlighted, disabled, active)
- Custom node/edge shapes via Canvas/SVG/WebGL
- Animation system
- Temporal graph via timeline plugin
- Tree graph mode

---

### 3. Cytoscape.js + react-cytoscapejs (Best for Algorithms)

| | Cosmograph | Cytoscape.js |
|---|---|---|
| **Stars** | ~1k | 11k |
| **Rendering** | WebGL | Canvas |
| **Max nodes** | 1M+ | 10k-30k |
| **Force layout** | GPU-accelerated | CPU (cose, cola, euler) |
| **React wrapper** | @cosmograph/react | react-cytoscapejs |
| **Graph algorithms** | Limited | Most extensive (native) |
| **Plugin ecosystem** | None | 100+ extensions |
| **License** | Proprietary | MIT |

**Why it's strong**: Cytoscape has the richest built-in graph algorithm library of any JavaScript graph library. If your primary need is analytics (not just visualization), Cytoscape is unmatched.

```bash
npm install cytoscape react-cytoscapejs
# Layout plugins
npm install cytoscape-dagre cytoscape-cola cytoscape-cose-bilkent cytoscape-euler
npm install cytoscape-fcose cytoscape-elk cytoscape-spread
# Interaction plugins
npm install cytoscape-popper cytoscape-context-menus cytoscape-navigator
npm install cytoscape-edgehandles cytoscape-expand-collapse
```

**Native graph algorithms (no plugins needed):**
- BFS, DFS traversal
- Dijkstra's shortest path
- A* shortest path
- Kruskal's minimum spanning tree
- Karger-Stein minimum cut
- PageRank
- Betweenness centrality
- Closeness centrality
- Degree centrality
- Hop distance
- DegreeCentralityNormalized
- Floyd-Warshall all-pairs shortest paths

**Extension algorithms:**
- Community detection (Markov clustering via plugin)
- Hierarchical clustering
- Edge betweenness clustering

---

### 4. react-force-graph + 3d-force-graph (Best 3D/VR)

| | Cosmograph | react-force-graph |
|---|---|---|
| **Stars** | ~1k | 3k + 6k (3d-force-graph) |
| **Rendering** | WebGL (2D) | Canvas (2D) + WebGL/Three.js (3D) + WebXR (VR/AR) |
| **Max nodes** | 1M+ | 5k-20k |
| **Force layout** | GPU-accelerated | d3-force (CPU) / d3-force-3d |
| **3D** | No | Full 3D, VR, AR |
| **React wrapper** | @cosmograph/react | react-force-graph (native React) |
| **License** | Proprietary | MIT |

**Why it's strong**: The only library that offers 2D, 3D, VR, and AR in one package. If you need immersive graph exploration, nothing else comes close.

```bash
npm install react-force-graph-2d   # 2D canvas
npm install react-force-graph-3d   # 3D WebGL
npm install react-force-graph-ar   # AR
npm install react-force-graph-vr   # VR
npm install react-force-graph      # all-in-one
```

Features beyond Cosmograph:
- Full 3D navigation (orbit, rotate, zoom)
- VR/AR mode via WebXR
- Custom 3D objects as nodes (any Three.js geometry)
- Directional particles on links (animated flow)
- DAG mode (directed acyclic graph layouts)
- Node drag in 3D space
- Camera auto-orbit

---

### 5. Reagraph (Best React-Native Experience)

| | Cosmograph | Reagraph |
|---|---|---|
| **Stars** | ~1k | 1k |
| **Rendering** | WebGL | WebGL (Three.js + react-three-fiber) |
| **Max nodes** | 1M+ | 5k-10k |
| **Force layout** | GPU-accelerated | d3-force-3d |
| **React wrapper** | @cosmograph/react | Native React (built on R3F) |
| **License** | Proprietary | Apache 2.0 |

**Why it's strong**: Built entirely on react-three-fiber, making it the most "React-native" graph library. Clean, modern API. From the same team as REAVIZ (charts) and Reaflow (flow diagrams).

```bash
npm install reagraph
```

Features:
- 2D and 3D rendering
- Force-directed, radial, hierarchical, treemap-2D layouts
- Clustering with lensing (fisheye)
- Multi-select, context menus
- Path finding visualization
- Animated layout transitions
- Custom node/edge renderers (React components)

---

### 6. Gephi Lite (Best for Exploration)

| | Cosmograph | Gephi Lite |
|---|---|---|
| **Stars** | ~1k | 315 (lite) / 6.4k (desktop) |
| **Rendering** | WebGL | WebGL (Sigma.js) |
| **Max nodes** | 1M+ | 100k+ |
| **Platform** | Web (SaaS) | Web (self-hosted) |
| **License** | Proprietary | GPL-3.0 |

[Gephi Lite](https://github.com/gephi/gephi-lite) is the web version of the legendary Gephi desktop application. It's built on Sigma.js + Graphology under the hood.

Features:
- Full graph exploration UI (no code needed)
- ForceAtlas2 layout
- Community detection
- Filtering, searching
- Node/edge appearance mapping (size, color by metric)
- Statistics panel
- Import GEXF, GraphML, JSON
- Export PNG, SVG, GEXF

```bash
# Self-host: clone and run
git clone https://github.com/gephi/gephi-lite.git
cd gephi-lite && npm install && npm run dev
```

Best for: **Non-developer users who need Cosmograph-like exploration without writing code.**

---

### 7. Graphistry (Best for Big Data / GPU Analytics)

| | Cosmograph | Graphistry |
|---|---|---|
| **Rendering** | WebGL | WebGL (GPU-accelerated) |
| **Max nodes** | 1M+ | 10M+ |
| **GPU analytics** | Force layout only | Full GPU pipeline (layout, clustering, filtering) |
| **React wrapper** | @cosmograph/react | @graphistry/client-api-react |
| **License** | Proprietary | Open-source client, server needs license |

Graphistry is the closest competitor to Cosmograph in terms of GPU-accelerated graph analytics at scale. The JavaScript client (`@graphistry/client-api-react`) is open source; the GPU server can be self-hosted.

```bash
npm install @graphistry/client-api-react
```

Best for: **When you need to visualize 1M-10M+ node graphs with GPU acceleration on the server side.**

---

### 8. Memgraph Orb (Best for Graph Database Integration)

- **GitHub**: [memgraph/orb](https://github.com/memgraph/orb) -- 418 stars
- **Rendering**: Canvas (via D3) or WebGL (via Sigma.js backend)
- **License**: Apache 2.0

Built specifically as a graph visualization frontend for graph databases (Memgraph, Neo4j, etc.).

Features:
- Direct Cypher query result visualization
- Force-directed and custom layouts
- Node/edge styling via mappers
- Event handling (click, hover, drag)
- Canvas and WebGL rendering backends
- Designed for graph DB query results

```bash
npm install @memgraph/orb
```

Best for: **When your graph data comes from Memgraph/Neo4j and you need quick visualization.**

---

### 9. VivaGraphJS + ngraph ecosystem (Best for Custom Performance)

- **GitHub**: [anvaka/VivaGraphJS](https://github.com/anvaka/VivaGraphJS) -- 3,862 stars
- **Rendering**: SVG or WebGL
- **License**: MIT

A modular graph visualization library with interchangeable renderers and layout engines.

Related packages:
- `ngraph.graph` -- graph data structure
- `ngraph.forcelayout` -- CPU force layout (2D/3D)
- `ngraph.pixel` -- WebGL renderer via Three.js (343 stars)
- `ngraph.path` -- path finding (A*, NBA*, Dijkstra)

```bash
npm install vivagraphjs
# Or modular approach
npm install ngraph.graph ngraph.forcelayout ngraph.pixel
```

Best for: **When you want to build a custom graph renderer with swappable components.**

---

## Head-to-Head Feature Comparison

| Feature | Cosmograph | Sigma+Graphology | G6+Graphin | Cytoscape | react-force-graph | Reagraph | Gephi Lite |
|---|---|---|---|---|---|---|---|
| **WebGL rendering** | Yes | Yes | Partial | No (Canvas) | 3D only | Yes | Yes |
| **GPU force layout** | Yes | No (Web Worker) | Yes (plugin) | No | No | No | No (Worker) |
| **Max nodes (smooth)** | 1M | 100k | 50k | 30k | 20k | 10k | 100k |
| **React component** | Yes | Yes | Yes | Yes | Yes | Yes | No (standalone) |
| **3D rendering** | No | No | No | No | Yes | Yes | No |
| **VR/AR** | No | No | No | No | Yes | No | No |
| **Community detection** | Yes | Louvain, LP | Louvain, LP | Plugin | No | No | Yes |
| **Centrality metrics** | Degree | Degree, between, close, eigen, PR | Degree, PR | All types | No | No | Yes |
| **Shortest path** | No | Dijkstra, BFS, A* | Dijkstra | Dijkstra, A*, FW | No | No | No |
| **PageRank** | No | Yes | Yes | Yes | No | No | No |
| **Connected components** | Yes | Yes | Yes | Yes | No | No | Yes |
| **Edge bundling** | No | No | Yes | Plugin | No | No | No |
| **Fisheye lens** | No | Plugin | Yes | No | No | Yes | No |
| **Compound/nested nodes** | No | No | Yes (combo) | Yes | No | No | No |
| **Minimap** | No | Plugin | Yes | Plugin | No | No | No |
| **Temporal/timeline** | Yes | Manual | Plugin | Manual | No | No | No |
| **Export PNG/SVG** | Yes | Yes | Yes | Yes | No | No | Yes |
| **Graph import (GEXF)** | No | Yes | Yes | No | No | No | Yes |
| **Custom node rendering** | Limited | WebGL shaders | Canvas/SVG/React | CSS/Canvas | React/Three.js | React/R3F | No |
| **Directed graph** | Yes | Yes | Yes | Yes | Yes | Yes | Yes |
| **Self-hosted** | No (SaaS) | Yes | Yes | Yes | Yes | Yes | Yes |
| **License** | Proprietary | MIT | MIT | MIT | MIT | Apache 2.0 | GPL-3.0 |

---

## Recommended Picks

### "I want the most analytics features" (replacing Cosmograph analytics)
**Sigma.js + Graphology + @react-sigma/core**
- Most graph algorithms available via graphology plugins
- WebGL rendering handles 100k+ nodes
- Mature ecosystem, actively maintained

### "I want the easiest all-in-one setup"
**AntV G6 + Graphin**
- Everything built-in: layouts, algorithms, interactions, plugins
- React wrapper with pre-built UI components
- GPU layout available for large graphs

### "I want the most graph algorithms"
**Cytoscape.js + react-cytoscapejs**
- Richest native algorithm library
- 100+ extension plugins
- 15+ years of academic and industry use

### "I want 3D/VR/AR graph exploration"
**react-force-graph**
- 2D + 3D + VR + AR in one package
- Custom Three.js objects as nodes

### "I need 1M+ nodes (Cosmograph-scale)"
**Sigma.js + Graphology** for up to 500k, or **Graphistry** for 1M-10M+ with GPU server

### "I want a no-code Cosmograph alternative"
**Gephi Lite** -- self-hosted web app, no React code needed

---

## Quick Start: Building a Cosmograph-Like App in React

```bash
# Install the recommended stack
npm install sigma graphology @react-sigma/core
npm install graphology-layout-forceatlas2 graphology-layout-noverlap
npm install graphology-metrics graphology-communities-louvain
npm install graphology-shortest-path graphology-components
```

```tsx
import { SigmaContainer, ControlsContainer, ZoomControl, SearchControl } from "@react-sigma/core";
import Graph from "graphology";
import forceAtlas2 from "graphology-layout-forceatlas2";
import louvain from "graphology-communities-louvain";
import { degreeCentrality } from "graphology-metrics/centrality/degree";

// Create graph
const graph = new Graph();
graph.addNode("a", { x: 0, y: 0, size: 10, label: "Node A", color: "#f00" });
graph.addNode("b", { x: 1, y: 1, size: 10, label: "Node B", color: "#00f" });
graph.addEdge("a", "b");

// Run analytics
const communities = louvain(graph);           // community detection
const centrality = degreeCentrality(graph);   // centrality metrics

// Apply force layout
forceAtlas2.assign(graph, { iterations: 100 });

// Size nodes by centrality
graph.forEachNode((node) => {
  graph.setNodeAttribute(node, "size", 5 + centrality[node] * 20);
});

// Color by community
graph.forEachNode((node) => {
  const colors = ["#e41a1c", "#377eb8", "#4daf4a", "#984ea3", "#ff7f00"];
  graph.setNodeAttribute(node, "color", colors[communities[node] % colors.length]);
});

function App() {
  return (
    <SigmaContainer graph={graph} style={{ height: "100vh" }}>
      <ControlsContainer position="bottom-right">
        <ZoomControl />
      </ControlsContainer>
      <ControlsContainer position="top-right">
        <SearchControl />
      </ControlsContainer>
    </SigmaContainer>
  );
}
```

This gives you a Cosmograph-like experience with WebGL rendering, force layout, community detection, centrality-based sizing, search, and zoom -- all open source.
