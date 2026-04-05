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

---

## Advanced Alternatives: Enterprise-Grade & Specialized

### 10. Neo4j Visualization Library (NVL) -- Graph Database Native

- **npm**: `@neo4j-nvl/react` + `@neo4j-nvl/base`
- **GitHub**: neo4j (818 stars for browser)
- **Rendering**: WebGL + Canvas
- **License**: Free to use with Neo4j
- **Last updated**: 2026-03-31

**The official graph visualization library from Neo4j**, the world's most popular graph database. If your data lives in Neo4j, this is the most integrated option.

Features:
- Native Cypher query integration (run queries, visualize results)
- Schema-aware visualization (respects node labels and relationship types)
- Force-directed layout with incremental expansion
- Node/relationship styling by property values
- Double-click to expand neighborhoods
- Hover tooltips with property details
- Rule-based styling (conditional formatting)
- Zoom, pan, fit-to-screen
- Selection, multi-select, lasso
- Built for React

```bash
npm install @neo4j-nvl/react @neo4j-nvl/base neo4j-driver
```

```tsx
import { InteractiveNvlWrapper } from '@neo4j-nvl/react';
import neo4j from 'neo4j-driver';

// Query Neo4j and visualize
const driver = neo4j.driver('neo4j://localhost', neo4j.auth.basic('neo4j', 'password'));
const session = driver.session();
const result = await session.run('MATCH (n)-[r]->(m) RETURN n, r, m LIMIT 100');

<InteractiveNvlWrapper
  nodes={nodes}
  rels={relationships}
  nvlOptions={{ layout: 'force-directed' }}
/>
```

Best for: **When your graph data is in Neo4j and you want zero-friction visualization. Strongest for knowledge graphs, fraud detection, recommendation engines.**

---

### 11. Linkurious Ogma (Enterprise WebGL Engine)

- **npm**: `@linkurious/ogma-react`
- **Rendering**: WebGL
- **License**: Commercial (free for non-commercial use)
- **Last updated**: 2026-03-20

**The most feature-rich commercial graph visualization library.** Ogma is what powers Linkurious Enterprise, used by Interpol, Europol, and major banks for fraud investigation.

Features beyond Cosmograph:
- GPU-accelerated WebGL rendering (500k+ nodes)
- 20+ layout algorithms (force, hierarchical, radial, concentric, sequential, geographic, etc.)
- **Geo mode** (plot nodes on a map with Leaflet/Mapbox integration)
- **Grouping / aggregation** (collapse clusters into super-nodes)
- Edge bundling, curved edges, parallel edges
- Node/edge filtering with animated transitions
- **Lasso selection**, rectangle selection, marquee
- **Shortest path highlighting** with animated traversal
- **Rule-based styling engine** (conditional node/edge appearance)
- Text search across all properties
- Minimap, navigator, overview
- Undo/redo
- Export to PNG, SVG, JSON, GEXF, GraphML
- **Virtual nodes** (nodes that exist visually but not in data)
- Plugin architecture
- React wrapper with hooks

```bash
npm install @linkurious/ogma @linkurious/ogma-react
```

Best for: **Enterprise graph investigation (fraud, cybersecurity, intelligence), when you need the most polished UX and are OK with a commercial license for production.**

---

### 12. Rete.js (Visual Programming / Node Editor)

- **GitHub**: [retejs/rete](https://github.com/retejs/rete) -- 11,980 stars
- **Rendering**: HTML + SVG (React/Vue/Angular/Svelte renderers)
- **License**: MIT

**A framework for building visual programming interfaces**, like Unreal Engine Blueprints, ComfyUI, or Blender's node editor.

Features:
- Dataflow and control flow graph execution
- Type-safe connections (typed input/output sockets)
- Minimap, reroute pins, auto-arrange
- Zoom, pan, selection
- Connection validation rules
- Custom node UI (render any React component)
- Undo/redo
- Import/export JSON
- Plugin system
- Built-in layout via elk.js

```bash
npm install rete rete-react-plugin rete-area-plugin rete-connection-plugin rete-render-utils
```

Best for: **Building visual programming tools, AI/ML pipeline editors, shader editors, automation workflow builders.**

---

### 13. LiteGraph.js (GPU Node Graph Engine)

- **GitHub**: [jagenjo/litegraph.js](https://github.com/jagenjo/litegraph.js) -- 7,955 stars
- **Rendering**: HTML5 Canvas
- **License**: MIT

**Canvas-based node graph editor and runtime engine**, similar to what powers ComfyUI (Stable Diffusion). Includes a graph execution engine, not just visualization.

Features:
- Graph execution engine (nodes process data in real-time)
- Built-in node types: math, logic, audio, MIDI, WebGL
- Subgraph support (graphs within graphs)
- Live data preview on connections
- Custom widgets inside nodes (sliders, dropdowns, color pickers)
- Search bar for adding nodes
- Group boxes
- Serialization to/from JSON
- Very fast Canvas rendering

```bash
npm install litegraph.js
```

Best for: **Real-time signal processing, audio/visual pipelines, shader graphs, AI workflow editors (like ComfyUI).**

---

### 14. vis-network (Mature Graph Visualization)

- **GitHub**: [visjs/vis-network](https://github.com/visjs/vis-network) -- 3,545 stars
- **Rendering**: Canvas + HTML
- **License**: Apache 2.0

The continuation of the original vis.js library. Mature, battle-tested, widely used.

Features:
- Force-directed, hierarchical, user-defined layouts
- Clustering (visual grouping of nodes)
- Physics engine (Barnes-Hut, repulsion, force-directed)
- Edge types: dynamic, continuous, discrete, cubicBezier
- Shadow, dashes, arrows, labels
- Groups and group styling
- Navigation buttons, keyboard navigation
- Manipulation mode (add/edit/delete nodes and edges interactively)
- Hierarchical layout (tree structures)
- Configure panel (live settings editor)
- Handles thousands of nodes

```bash
npm install vis-network vis-data
```

Best for: **Quick prototyping, when you need a stable library with good documentation and don't need WebGL performance.**

---

### 15. GoJS (Enterprise Diagramming)

- **GitHub**: [NorthwoodsSoftware/GoJS](https://github.com/NorthwoodsSoftware/GoJS) -- 8,423 stars
- **Rendering**: Canvas + SVG
- **License**: Commercial (free for evaluation/development)

**The most complete diagramming SDK.** Powers Lucidchart-style applications.

Features beyond any open-source option:
- 150+ interactive sample diagrams
- Force-directed, tree, layered-digraph, circular, grid layouts
- Swimlanes, groups, subgraphs
- Link routing (orthogonal, AvoidsNodes, Bezier)
- Real-time collaboration support
- Undo/redo, copy/paste, drag-and-drop from palette
- Data binding (model-view separation)
- Overview panel, context menus
- Export to SVG, PNG, PDF
- Built-in React component
- Excellent documentation
- Virtualization (render only visible nodes for huge diagrams)

```bash
npm install gojs gojs-react
```

Best for: **Commercial diagramming apps, flowchart builders, org charts, floor plans, BPMN, when you need the most polished out-of-box experience.**

---

### 16. JointJS / Rappid (Open-Source Diagramming)

- **GitHub**: [clientIO/joint](https://github.com/clientIO/joint) -- 5,227 stars
- **Rendering**: SVG
- **License**: MPL-2.0 (open-source core), commercial for Rappid

Features:
- Built-in shapes: flowchart, UML, BPMN, ER diagram, Petri net, logic circuits
- Custom shapes via SVG markup
- Link routing (manhattan, metro, orthogonal)
- Port-based connections with validation
- Hierarchical groups and embedding
- Built-in paper scroller, minimap, navigator
- Undo/redo, clipboard, selection
- Import/export to JSON
- Rappid (commercial) adds: stencil, inspector, toolbar, keyboard shortcuts

```bash
npm install jointjs
```

Best for: **Open-source diagramming applications, UML/BPMN editors, when you need SVG-based rendering.**

---

### 17. maxGraph (Open-Source mxGraph Successor)

- **GitHub**: [maxGraph/maxGraph](https://github.com/maxGraph/maxGraph) -- 1,104 stars
- **Rendering**: SVG + HTML
- **License**: Apache 2.0

The open-source continuation of mxGraph (which powered draw.io / diagrams.net). Fully rewritten in TypeScript.

Features:
- Hierarchical, organic, circle, tree, compact tree, partition, stack layouts
- Swimlanes, layers, groups
- Edge routing (orthogonal, entity-relation)
- Cell folding (expand/collapse groups)
- Connection constraints and validation
- Stencils (shape libraries)
- XML-based graph serialization
- Undo/redo, clipboard
- Customizable selection, rubberband
- Overlay badges on nodes

```bash
npm install @maxgraph/core
```

Best for: **Building draw.io-like diagramming tools, when you want the mxGraph architecture in modern TypeScript.**

---

### 18. Flume (React Node Editor for Business Logic)

- **GitHub**: [chrisjpatty/flume](https://github.com/chrisjpatty/flume) -- 1,616 stars
- **Rendering**: HTML + SVG (React)
- **License**: MIT

**Purpose-built React node editor for extracting business logic.** Unlike generic graph editors, Flume is designed for non-developers to build logic flows.

Features:
- Type-safe ports with color coding
- Root node engine (resolve logic graphs to values)
- Built-in port types: string, number, boolean, custom
- Dynamic ports (add/remove based on configuration)
- Comments on nodes
- Built entirely in React (no Canvas dependency)

```bash
npm install flume
```

Best for: **Business rule engines, form builders, pricing calculators, when non-technical users need to configure logic visually.**

---

### Layout Algorithm Libraries (Pair With Any Renderer)

These are standalone layout engines you can combine with any graph renderer:

| Library | Stars | Algorithm | Best For |
|---|---|---|---|
| **elkjs** | (Eclipse) | Sugiyama/layered, force, tree, radial, stress | Most advanced automatic layout, port-aware |
| **@dagrejs/dagre** | 5,586 | Sugiyama/layered | DAG/tree layout, simple API |
| **d3-dag** | 1,506 | Sugiyama, Zherebko, topological | DAG layout with D3 integration |
| **webcola** | 2,090 | Constraint-based, force-directed | Constraints (alignment, grouping, non-overlap) |
| **d3-force** | (D3) | Velocity Verlet force simulation | Classic force-directed (d3 ecosystem) |
| **graphology-layout-forceatlas2** | (Graphology) | ForceAtlas2 (Gephi's algorithm) | Large-scale force layout in Web Worker |

```bash
# Install layout engines
npm install elkjs                              # Most powerful
npm install @dagrejs/dagre @dagrejs/graphlib   # Simple DAG layout
npm install d3-dag                             # DAG + D3
npm install webcola                            # Constraint-based
```

---

### Graph Databases (Backend for Graph Analytics)

If you need serious graph analytics beyond what client-side JavaScript can handle, pair your visualization with a graph database:

| Database | Stars | License | Query Language | Best For |
|---|---|---|---|---|
| **Neo4j** | 16k | GPL-3.0 (Community) | Cypher | Most popular, richest ecosystem, ACID |
| **Dgraph** | 22k | Apache 2.0 | GraphQL/DQL | Distributed, native GraphQL |
| **ArangoDB** | 14k | Business Source | AQL | Multi-model (graph + document + key-value) |
| **JanusGraph** | 5.8k | Apache 2.0 | Gremlin/TinkerPop | Distributed, pluggable storage (Cassandra/HBase) |
| **OrientDB** | 5k | Apache 2.0 | SQL-like + Gremlin | Multi-model with SQL compatibility |

---

## Ultimate Feature Comparison (All 18 Libraries)

| Library | Stars | Rendering | Max Nodes | React | Graph Algorithms | Diagram/Flow | Visual Programming | Geo/Map | License |
|---|---|---|---|---|---|---|---|---|---|
| **Sigma+Graphology** | 12k+1.6k | WebGL | 100k+ | @react-sigma | Full (50+ plugins) | No | No | No | MIT |
| **G6+Graphin** | 12k+1k | Canvas/WebGL | 50k | @antv/graphin | Full (built-in) | No | No | No | MIT |
| **Cytoscape.js** | 11k | Canvas | 30k | react-cytoscapejs | Most extensive | No | No | No | MIT |
| **react-force-graph** | 3k+6k | Canvas/WebGL | 20k | Native | Basic | No | No | No | MIT |
| **Reagraph** | 1k | WebGL (R3F) | 10k | Native | Basic | No | No | No | Apache 2.0 |
| **Gephi Lite** | 315 | WebGL | 100k+ | No | ForceAtlas2+metrics | No | No | No | GPL-3.0 |
| **Graphistry** | 2.5k | WebGL (GPU) | 10M+ | Client API | GPU-accelerated | No | No | No | BSD-3 |
| **Memgraph Orb** | 418 | Canvas/WebGL | 10k | No | Via Memgraph DB | No | No | No | Apache 2.0 |
| **VivaGraphJS** | 3.9k | SVG/WebGL | 50k | No | ngraph plugins | No | No | No | MIT |
| **Neo4j NVL** | -- | WebGL | 30k | @neo4j-nvl/react | Via Neo4j DB | No | No | No | Free w/Neo4j |
| **Ogma (Linkurious)** | -- | WebGL | 500k+ | @linkurious/ogma-react | Built-in + geo | No | No | Yes | Commercial |
| **React Flow** | 36k | SVG/HTML | 10k+ | Native | No | Full | No | No | MIT |
| **Rete.js** | 12k | HTML/SVG | 5k | Plugin | No | Full | Full | No | MIT |
| **LiteGraph.js** | 8k | Canvas | 5k | No | Graph execution | Full | Full | No | MIT |
| **vis-network** | 3.5k | Canvas | 5k | Manual | Basic | No | No | No | Apache 2.0 |
| **GoJS** | 8.4k | Canvas/SVG | 10k+ | gojs-react | No | Full | No | No | Commercial |
| **JointJS** | 5.2k | SVG | 5k | No | No | Full | No | No | MPL-2.0 |
| **maxGraph** | 1.1k | SVG/HTML | 5k | No | No | Full | No | No | Apache 2.0 |
| **Flume** | 1.6k | HTML/SVG | 1k | Native | Logic resolver | Full | Yes | No | MIT |

---

## Decision Tree

```
What do you need?
|
|-- Graph ANALYTICS (algorithms, metrics, community detection)?
|   |-- Need 100k+ nodes? --> Sigma.js + Graphology
|   |-- Need all-in-one? --> AntV G6 + Graphin
|   |-- Need most algorithms? --> Cytoscape.js
|   |-- Need 1M+ nodes? --> Graphistry (GPU server)
|   |-- Need graph DB integration? --> Neo4j NVL + Neo4j
|
|-- Graph VISUALIZATION (interactive exploration)?
|   |-- Need 3D/VR/AR? --> react-force-graph
|   |-- Need React-native DX? --> Reagraph
|   |-- Need no-code? --> Gephi Lite
|   |-- Enterprise (500k+ nodes)? --> Ogma (commercial)
|
|-- FLOW DIAGRAMS / NODE EDITORS?
|   |-- Workflow/pipeline builder? --> React Flow (@xyflow)
|   |-- Diagramming app (Visio-like)? --> AntV X6 or GoJS
|   |-- Visual programming (Blueprints)? --> Rete.js or LiteGraph.js
|   |-- Business logic editor? --> Flume
|   |-- Open-source draw.io? --> maxGraph
|
|-- Need BOTH charts AND graphs?
|   --> Apache ECharts (has built-in graph type) + Cytoscape/G6 for advanced analytics
```
