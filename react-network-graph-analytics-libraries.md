# Professional Open-Source React Libraries for Network Graphs and Full Analytics

A comprehensive guide to open-source React libraries for network graph visualization, chart/plot rendering, and data analytics.

---

## Network Graph Libraries (React)

### Tier 1: Full-Featured Network Graph Analytics

#### 1. AntV G6 + Graphin (React wrapper)
- **GitHub**: [antvis/G6](https://github.com/antvis/G6) -- 12,044 stars
- **React wrapper**: `@antv/graphin` (npm)
- **Rendering**: Canvas + WebGL (via GPU)
- **License**: MIT

**The most feature-rich open-source graph analytics toolkit.** Built by Ant Group (Alibaba).

Features:
- Force-directed, dagre, radial, concentric, fruchterman, circular, grid layouts
- Graph analytics: shortest path, PageRank, community detection, centrality, clustering
- Expand/collapse sub-graphs, combo (grouped) nodes
- Edge bundling, fisheye lens, minimap, toolbar, context menu
- Node/edge filtering, searching, highlighting
- Animated transitions between layouts
- Custom node/edge shapes (SVG or Canvas)
- Huge graph support (10k+ nodes via WebGL)
- Timeline playback for temporal graphs
- Built-in graph algorithms library (`@antv/algorithm`)

```bash
npm install @antv/g6 @antv/graphin
```

Best for: **Enterprise-grade graph analytics dashboards, knowledge graphs, fraud detection, social network analysis.**

---

#### 2. Cytoscape.js + react-cytoscapejs
- **GitHub**: [cytoscape/cytoscape.js](https://github.com/cytoscape/cytoscape.js) -- 10,926 stars
- **React wrapper**: `react-cytoscapejs` (npm)
- **Rendering**: Canvas
- **License**: MIT

**The gold standard for computational graph analysis.** Originally from bioinformatics research (University of Toronto).

Features:
- 20+ layout algorithms (cola, dagre, cose-bilkent, euler, spread, etc.) via plugins
- Graph theory algorithms: BFS, DFS, Dijkstra, A*, Kruskal, PageRank, betweenness centrality, degree centrality
- Compound/nested nodes (hierarchical grouping)
- Selectors (CSS-like query syntax for graph elements)
- Animation API
- Extensions ecosystem (100+ plugins)
- Export to PNG/JPG/SVG/JSON
- Touch support, pinch-to-zoom
- Handles 10,000+ elements efficiently

```bash
npm install cytoscape react-cytoscapejs
# Layout plugins
npm install cytoscape-dagre cytoscape-cola cytoscape-cose-bilkent
```

Best for: **Scientific/research graph analysis, bioinformatics, complex graph algorithms, when you need the richest plugin ecosystem.**

---

#### 3. Sigma.js + @react-sigma/core + Graphology
- **GitHub**: [jacomyal/sigma.js](https://github.com/jacomyal/sigma.js) -- 11,966 stars
- **Graph model**: [graphology](https://github.com/graphology/graphology) -- 1,626 stars
- **React wrapper**: `@react-sigma/core` (npm)
- **Rendering**: WebGL
- **License**: MIT

**The best performer for massive graphs (100k+ nodes).** WebGL rendering makes it the fastest option.

Features:
- WebGL rendering (handles 100,000+ nodes smoothly)
- Graphology provides: shortest path, centrality, community detection (Louvain), PageRank, connected components, layout algorithms (ForceAtlas2, circular, random)
- Node/edge hover, click, drag interactions
- Custom node/edge renderers (WebGL shaders)
- Minimap, search, filter
- Force-directed layout running in Web Worker (non-blocking)
- Export capabilities

```bash
npm install sigma graphology @react-sigma/core
# Analytics
npm install graphology-metrics graphology-communities-louvain graphology-shortest-path
# Layouts
npm install graphology-layout-forceatlas2 graphology-layout-noverlap
```

Best for: **Large-scale network visualization (social networks, citation networks), when performance with 50k-500k nodes is critical.**

---

### Tier 2: React-Native Graph Components

#### 4. react-force-graph
- **GitHub**: [vasturiano/react-force-graph](https://github.com/vasturiano/react-force-graph) -- 3,050 stars
- **Rendering**: SVG (2D), WebGL via Three.js (3D), WebXR (VR/AR)
- **License**: MIT

Features:
- 2D, 3D, VR, and AR force-directed graph rendering
- Custom node/link rendering (HTML, SVG, Three.js objects)
- Node/link click, hover, drag
- Directional arrows and particles on links
- DAG mode (tree layouts)
- Zoom, pan, auto-fit
- Node clustering
- JSON-based graph data

```bash
npm install react-force-graph-2d  # 2D only
npm install react-force-graph-3d  # 3D only
npm install react-force-graph     # All variants
```

Best for: **3D graph visualization, VR/AR network exploration, visually impressive demos.**

---

#### 5. Reagraph
- **GitHub**: [reaviz/reagraph](https://github.com/reaviz/reagraph) -- 1,003 stars
- **Rendering**: WebGL (via Three.js + react-three-fiber)
- **License**: Apache 2.0

Features:
- 3D and 2D WebGL graph rendering
- Force-directed, radial, hierarchical, treemap-2D layouts
- Node/edge selection, multi-select
- Clustering, lensing (fisheye)
- Animated layout transitions
- Custom node/edge renderers
- Built with React Three Fiber (fully React-native)
- Path finding visualization
- Context menus

```bash
npm install reagraph
```

Best for: **React-first 3D graph visualization with clean API, when you want a modern React-native experience.**

---

## Full Analytics Chart Libraries (React)

These libraries cover the broad range of chart types (line, bar, scatter, pie, area, heatmap, treemap, etc.) alongside network graphs.

### Tier 1: Most Comprehensive

#### 6. Apache ECharts + echarts-for-react
- **GitHub**: [apache/echarts](https://github.com/apache/echarts) -- 66,068 stars
- **React wrapper**: `echarts-for-react` (npm)
- **Rendering**: Canvas + SVG
- **License**: Apache 2.0

**The most complete charting library in existence.** Covers virtually every chart type.

Chart types (40+):
- Line, bar, scatter, pie, radar, treemap, sunburst, parallel, sankey, funnel, gauge, candlestick, boxplot, heatmap, map, graph/network, tree, themeRiver, calendar, custom series, pictorial bar, lines (geo), effect scatter, and more

Analytics features:
- Built-in graph/network visualization with force layout
- Data zoom, brush selection, visual mapping
- Universal transitions between chart types
- Large dataset rendering (million+ points via progressive rendering)
- Built-in data transforms (filter, sort, aggregate, regression)
- Geographic map support (GeoJSON)
- 3D charts via echarts-gl (globe, scatter3D, bar3D, surface, map3D)
- Accessibility (screen reader support)
- Server-side rendering

```bash
npm install echarts echarts-for-react
# For 3D
npm install echarts-gl
```

Best for: **Enterprise dashboards needing every chart type imaginable, especially when you need network graphs AND standard charts in one library.**

---

#### 7. Plotly.js + react-plotly.js
- **GitHub**: [plotly/plotly.js](https://github.com/plotly/plotly.js) -- 18,174 stars
- **React wrapper**: `react-plotly.js` (npm)
- **Rendering**: SVG + WebGL
- **License**: MIT

**The most scientifically-oriented charting library.** Came from the data science / Python ecosystem.

Chart types (50+):
- All standard charts plus: contour, violin, waterfall, ternary, polar, carpet, OHLC, cone, streamtube, isosurface, mesh3d, scatter3D, surface3D, choropleth (map), scattergeo, scattermapbox, densitymapbox, network graph (via scatter + lines), Sankey, treemap, sunburst, icicle, funnel, indicator, table

Analytics features:
- Statistical traces (histogram2d, histogram2dcontour, violin, box)
- WebGL traces for millions of points (scattergl, heatmapgl)
- Mapbox integration for geographic data
- 3D surface, scatter, mesh plots
- Animations and frame-based transitions
- Cross-filtering via `plotly_selected` events
- Export to PNG, SVG, PDF, WebP
- Subplots, multiple axes, mixed chart types

```bash
npm install plotly.js-dist-min react-plotly.js
```

Best for: **Scientific/statistical analytics, when you need 3D plots, statistical traces, and publication-quality output.**

---

### Tier 2: React-First Libraries

#### 8. Nivo
- **GitHub**: [plouc/nivo](https://github.com/plouc/nivo) -- 14,006 stars
- **Rendering**: SVG + Canvas + HTML
- **License**: MIT

**The best pre-styled React charting library.** Beautiful defaults, minimal config.

Chart types (30+):
- Line, bar, scatter, pie, radar, chord, sankey, treemap, sunburst, circle packing, heatmap, calendar heatmap, waffle, funnel, marimekko, stream, bump, swarmplot, network, voronoi, parallel coordinates, geo (choropleth)

Features:
- Server-side rendering support
- Built-in responsive containers
- Rich theming system
- Animation via react-spring
- Accessibility (ARIA)
- Canvas rendering for large datasets
- Patterns and gradients

```bash
npm install @nivo/core @nivo/line @nivo/bar @nivo/network @nivo/chord @nivo/sankey
```

Best for: **Beautiful dashboards with minimal configuration, when you want React-native components with great defaults.**

---

#### 9. Recharts
- **GitHub**: [recharts/recharts](https://github.com/recharts/recharts) -- 26,944 stars
- **Rendering**: SVG
- **License**: MIT

**The most popular React charting library by downloads.** Declarative, composable API.

Chart types:
- Line, area, bar, scatter, pie, radar, radial bar, treemap, funnel, sankey, composed (mixed)

Features:
- Fully declarative (JSX-based)
- Composable components (mix chart types freely)
- Responsive containers
- Custom tooltips, legends, labels
- Animation via react-smooth
- Reference lines, reference areas
- Brush (zoom/filter)

```bash
npm install recharts
```

Best for: **Standard business dashboards, when you want the simplest React API for common chart types. Does NOT have network graph support.**

---

#### 10. visx (by Airbnb)
- **GitHub**: [airbnb/visx](https://github.com/airbnb/visx) -- 20,714 stars
- **Rendering**: SVG
- **License**: MIT

**The most flexible low-level React + D3 toolkit.** Maximum control, no opinions.

Packages (30+):
- `@visx/shape`, `@visx/scale`, `@visx/axis`, `@visx/grid`, `@visx/geo`, `@visx/hierarchy` (treemap, pack, tree, cluster), `@visx/network`, `@visx/chord`, `@visx/heatmap`, `@visx/stats` (boxplot, violin), `@visx/wordcloud`, `@visx/voronoi`, `@visx/threshold`, `@visx/pattern`, `@visx/gradient`, and more

Features:
- Unopinionated -- you compose D3 primitives as React components
- `@visx/network` for graph visualization
- Every D3 capability wrapped in React
- Tree shaking (only import what you need)
- Full TypeScript support

```bash
npm install @visx/network @visx/shape @visx/scale @visx/hierarchy
```

Best for: **When you need full control over every pixel, custom/novel visualizations, or want to build your own chart library on top of D3+React.**

---

#### 11. Victory
- **GitHub**: [FormidableLabs/victory](https://github.com/FormidableLabs/victory) -- 11,267 stars
- **Rendering**: SVG
- **License**: MIT

Chart types:
- Line, area, bar, scatter, pie, polar, voronoi, histogram, boxplot, candlestick, error bar

Features:
- Shared animations system
- Works on React Native
- Composable chart components
- Built-in themes
- Brush and zoom containers
- Cross-platform (web + mobile)

```bash
npm install victory
```

Best for: **Cross-platform (web + React Native) chart needs.**

---

## Comparison Matrix

| Library | Stars | Network Graph | Standard Charts | 3D | Analytics Algorithms | Max Nodes | React Native |
|---|---|---|---|---|---|---|---|
| **AntV G6 + Graphin** | 12k | Full (primary focus) | No | No | PageRank, centrality, community, shortest path | 10k+ | No |
| **Cytoscape.js** | 11k | Full (primary focus) | No | No | BFS, DFS, Dijkstra, A*, PageRank, centrality | 10k+ | No |
| **Sigma.js + Graphology** | 12k | Full (primary focus) | No | No | Louvain, centrality, shortest path, components | 100k+ | No |
| **react-force-graph** | 3k | Full (primary focus) | No | Yes (3D, VR, AR) | Basic (force simulation) | 5k | No |
| **Reagraph** | 1k | Full (primary focus) | No | Yes (WebGL) | Basic (layouts) | 5k | No |
| **Apache ECharts** | 66k | Yes (built-in graph type) | 40+ types | Yes (echarts-gl) | Data transforms, regression | 1M+ | No |
| **Plotly.js** | 18k | Partial (scatter+lines) | 50+ types | Yes (native) | Statistical traces | 1M+ (WebGL) | No |
| **Nivo** | 14k | Yes (@nivo/network) | 30+ types | No | No | Medium | No |
| **Recharts** | 27k | No | 12+ types | No | No | Medium | No |
| **visx** | 21k | Yes (@visx/network) | 30+ packages | No | No | Medium | No |
| **Victory** | 11k | No | 12+ types | No | No | Medium | Yes |

---

## Additional Professional Libraries

### Node-Based Editors & Flow Diagrams

#### 12. React Flow (@xyflow/react)
- **GitHub**: [xyflow/xyflow](https://github.com/xyflow/xyflow) -- 35,963 stars
- **Rendering**: SVG + HTML (DOM-based nodes)
- **License**: MIT (with pro features under paid license)

**The most popular node-based editor library.** Not a traditional graph analytics tool, but essential for building interactive flow diagrams, pipelines, and workflow editors.

Features:
- Drag-and-drop node creation
- Custom node and edge types (render any React component as a node)
- Multiple edge types (bezier, step, smoothstep, straight)
- Nested/grouped sub-flows
- Minimap, controls, background grid
- Copy/paste, undo/redo
- Viewport controls (zoom, pan, fit)
- Touch/mobile support
- Fully controlled or uncontrolled mode
- Handles (connection ports on nodes)
- Auto-layout integration via dagre/elkjs

```bash
npm install @xyflow/react
# For auto-layout
npm install @dagrejs/dagre  # or elkjs
```

Best for: **Workflow editors, pipeline builders, visual programming, node-based UIs (like n8n, Node-RED, Figma-style tools).**

---

#### 13. AntV X6
- **GitHub**: [antvis/X6](https://github.com/antvis/X6) -- 6,513 stars
- **Rendering**: SVG + HTML
- **License**: MIT

**Professional diagramming engine** from the Ant Group ecosystem. Think of it as an open-source alternative to JointJS/GoJS.

Features:
- Built-in graph editing: create, move, resize, rotate, connect nodes
- 100+ built-in shapes (flowchart, UML, BPMN, ER diagram, circuit)
- Ports (connection points) with validation rules
- Hierarchical groups and embedding
- Undo/redo, clipboard, snapline alignment
- Grid snapping, scroller, minimap
- Auto-layout algorithms (dagre, elk)
- Edge routing (manhattan, metro, orth)
- Custom rendering with React/Vue/Angular components inside nodes
- Stencil panel (drag shapes from palette)
- Export to SVG/PNG/JSON

```bash
npm install @antv/x6 @antv/x6-react-shape
```

Best for: **Diagramming applications (Visio alternatives), BPMN/flowchart editors, ER diagram tools.**

---

#### 14. Reaflow
- **GitHub**: [reaviz/reaflow](https://github.com/reaviz/reaflow) -- 2,479 stars
- **Rendering**: SVG
- **License**: Apache 2.0

Features:
- Automatic layout via elkjs
- Nested/compound nodes
- Custom node/edge renderers (React components)
- Port-based connections
- Drag-and-drop, selection, undo/redo
- Edge label support
- Built for React (from the same team as Reagraph)

```bash
npm install reaflow
```

Best for: **Workflow/pipeline visualization with automatic layout, when you want something simpler than React Flow.**

---

### Geospatial Analytics

#### 15. AntV L7
- **GitHub**: [antvis/L7](https://github.com/antvis/L7) -- 3,980 stars
- **Rendering**: WebGL
- **License**: MIT

**Large-scale geospatial data visualization engine.** The geographic counterpart to G6 in the Ant ecosystem.

Features:
- Point, line, polygon, heatmap, hexbin, arc, trip, wind layers
- 3D extrusion, building rendering
- GPU-accelerated rendering for millions of data points
- Mapbox GL, Google Maps, AMap base map support
- Spatial analysis (buffer, voronoi, kriging, IDW interpolation)
- Animated layers (trip, flow, scatter pulse)
- Custom shaders

```bash
npm install @antv/l7 @antv/l7-react
```

Best for: **Large-scale geospatial analytics, location intelligence dashboards, urban data visualization.**

---

### Tabular / Pivot Analytics

#### 16. AntV S2
- **GitHub**: [antvis/S2](https://github.com/antvis/S2) -- 1,675 stars
- **Rendering**: Canvas
- **License**: MIT

**Spreadsheet-style pivot table and cross-tab visualization engine.**

Features:
- Pivot table (cross-tab) with drill-down
- Table/sheet mode and tree hierarchy mode
- Conditional formatting (data bars, color scales, icon sets)
- Mini charts inside cells (sparklines, bullet charts, progress bars)
- Frozen rows/columns
- Custom cell renderers
- Adaptive layout
- High performance (Canvas rendering, handles 100k+ cells)
- Tooltip, sort, filter, copy/export

```bash
npm install @antv/s2 @antv/s2-react
```

Best for: **Pivot tables, spreadsheet analytics, BI-style tabular reports.**

---

### Data Streaming & Real-Time Analytics

#### 17. Semiotic
- **GitHub**: [nteract/semiotic](https://github.com/nteract/semiotic) -- 2,578 stars
- **Rendering**: SVG
- **License**: Apache 2.0

**React data visualization framework with built-in MCP server for AI-assisted chart generation.**

Features:
- Network frames (force, sankey, arc, chord, adjacency matrix)
- XY frames (line, area, scatter, bar, point density, contour)
- Ordinal frames (bar, timeline, swarm, violin, ridgeline, waterfall)
- Annotation layer (callouts, highlights, enclose)
- Responsive containers
- Data streaming support
- Brushing and filtering
- MCP server for AI agent integration

```bash
npm install semiotic
```

Best for: **Exploratory data analysis, when you want network + standard charts in one API, AI-assisted chart generation.**

---

### Financial / Time Series Charts

#### 18. TradingView Lightweight Charts
- **GitHub**: [tradingview/lightweight-charts](https://github.com/tradingview/lightweight-charts) -- 14,240 stars
- **Rendering**: Canvas
- **License**: Apache 2.0

Features:
- Candlestick, bar, line, area, histogram, baseline charts
- Real-time streaming data
- Time scale with timezone support
- Crosshair, price lines, markers
- Multiple panes and series
- Lightweight (45kb gzipped)
- GPU-accelerated canvas rendering

```bash
npm install lightweight-charts
```

Best for: **Financial dashboards, stock/crypto charts, real-time time series.**

---

### General Purpose Charts (Additional)

#### 19. Chart.js + react-chartjs-2
- **GitHub**: [chartjs/Chart.js](https://github.com/chartjs/Chart.js) -- 67,329 stars
- **Rendering**: Canvas
- **License**: MIT

The most popular charting library overall. Simple, fast, Canvas-based.

Chart types: line, bar, radar, doughnut, pie, polar area, bubble, scatter

```bash
npm install chart.js react-chartjs-2
```

---

#### 20. ApexCharts + react-apexcharts
- **GitHub**: [apexcharts/apexcharts.js](https://github.com/apexcharts/apexcharts.js) -- 15,089 stars
- **Rendering**: SVG
- **License**: MIT

Modern, interactive charts with built-in features that require plugins in other libraries.

Chart types: line, area, bar, column, mixed, range bar (Gantt), timeline, candlestick, boxplot, heatmap, treemap, pie, radial, radar, polar, scatter, bubble, slope, funnel, pyramid

Features:
- Built-in annotations, zoom, pan, data labels
- Real-time data updates
- Synchronized charts (linked axes)
- Dark mode
- Localization support
- Toolbar (zoom, pan, reset, download)

```bash
npm install apexcharts react-apexcharts
```

---

#### 21. Carbon Charts (IBM)
- **GitHub**: [carbon-design-system/carbon-charts](https://github.com/carbon-design-system/carbon-charts) -- 1,025 stars
- **Rendering**: SVG (via D3)
- **License**: Apache 2.0

IBM's enterprise charting library built on the Carbon Design System.

Chart types: line, area, bar, grouped bar, stacked bar, scatter, bubble, pie, donut, gauge, meter, treemap, circle pack, network, alluvial, wordcloud, radar, heatmap, combo, histogram, lollipop, bullet, boxplot, thematic map, choropleth

```bash
npm install @carbon/charts-react
```

Best for: **Enterprise IBM/Carbon Design System projects, when you want design-system-aligned charts.**

---

#### 22. Tremor
- **GitHub**: [tremorlabs/tremor](https://github.com/tremorlabs/tremor) -- 3,351 stars
- **Rendering**: SVG (built on Recharts internally)
- **License**: Apache 2.0

**Dashboard component library** with pre-built chart + UI components. Tailwind CSS based.

Components: area chart, bar chart, line chart, donut chart, scatter chart, funnel chart, tracker, category bar, delta bar, progress bar, spark chart, number, badge delta, KPI cards, tables, lists

```bash
npm install @tremor/react
```

Best for: **Rapid dashboard building with Tailwind CSS, when you want pre-styled analytics components out of the box.**

---

### Dashboard Layout

#### 23. react-grid-layout
- **GitHub**: [react-grid-layout/react-grid-layout](https://github.com/react-grid-layout/react-grid-layout) -- 22,162 stars
- **License**: MIT

**Draggable, resizable grid layout for building dashboard shells.** Not a chart library, but essential for building analytics dashboards.

Features:
- Drag-and-drop widget repositioning
- Resize handles
- Responsive breakpoints
- Serializable layout (save/load dashboard configs)
- Static widgets (non-draggable)
- Bounded containers

```bash
npm install react-grid-layout
```

Best for: **Building the dashboard container that holds your charts/graphs.**

---

## Extended Comparison Matrix

| Library | Stars | Type | Network Graph | Charts | 3D | Geo/Maps | Tables | Flow/Diagram | Performance |
|---|---|---|---|---|---|---|---|---|---|
| **AntV G6 + Graphin** | 12k | Graph | Full | No | No | No | No | No | 10k+ nodes |
| **Cytoscape.js** | 11k | Graph | Full | No | No | No | No | No | 10k+ nodes |
| **Sigma.js + Graphology** | 12k | Graph | Full | No | No | No | No | No | 100k+ nodes |
| **react-force-graph** | 3k | Graph | Full | No | 3D/VR/AR | No | No | No | 5k nodes |
| **Reagraph** | 1k | Graph | Full | No | WebGL 3D | No | No | No | 5k nodes |
| **React Flow (@xyflow)** | 36k | Flow | Partial | No | No | No | No | Full | 10k+ nodes |
| **AntV X6** | 7k | Diagram | Partial | No | No | No | No | Full | 10k+ nodes |
| **Reaflow** | 2.5k | Flow | Partial | No | No | No | No | Full | 1k nodes |
| **Apache ECharts** | 66k | Charts | Built-in | 40+ | echarts-gl | GeoJSON | No | No | 1M+ points |
| **Plotly.js** | 18k | Charts | Partial | 50+ | Native | Mapbox | No | No | 1M+ (WebGL) |
| **Chart.js** | 67k | Charts | No | 8 | No | No | No | No | Medium |
| **Recharts** | 27k | Charts | No | 12+ | No | No | No | No | Medium |
| **visx** | 21k | Charts | @visx/network | 30+ pkg | No | @visx/geo | No | No | Medium |
| **Nivo** | 14k | Charts | @nivo/network | 30+ | No | @nivo/geo | No | No | Medium |
| **ApexCharts** | 15k | Charts | No | 20+ | No | No | No | No | Medium |
| **Victory** | 11k | Charts | No | 12+ | No | No | No | No | Medium |
| **Semiotic** | 2.6k | Charts | Network frames | 15+ | No | No | No | No | Medium |
| **Carbon Charts** | 1k | Charts | network/alluvial | 20+ | No | choropleth | No | No | Medium |
| **Tremor** | 3.4k | Dashboard | No | 8+ | No | No | tables | No | Medium |
| **Lightweight Charts** | 14k | Financial | No | 5 | No | No | No | No | High (Canvas) |
| **AntV L7** | 4k | Geo | No | No | 3D extrude | Full | No | No | Millions |
| **AntV S2** | 1.7k | Tables | No | sparklines | No | No | Full (pivot) | No | 100k+ cells |
| **react-grid-layout** | 22k | Layout | No | No | No | No | No | No | N/A |

## Recommended Combinations

### For Full Network Graph Analytics + Dashboard Charts

```
Network graphs: @antv/g6 + @antv/graphin (or cytoscape + react-cytoscapejs)
Standard charts: Apache ECharts + echarts-for-react (or recharts for simpler needs)
```

### For Maximum Performance (Large Graphs)

```
Network graphs: sigma + graphology + @react-sigma/core
Standard charts: Apache ECharts (Canvas mode) or Plotly (WebGL mode)
```

### For 3D + Network + Charts

```
Network graphs: react-force-graph-3d (or reagraph)
Standard charts: Plotly.js + react-plotly.js (has native 3D)
Maps: react-map-gl + deck.gl
```

### For React-First Simplicity

```
Network graphs: @nivo/network (simple) or visx/network (flexible)
Standard charts: recharts (simple) or nivo (beautiful defaults)
```

### For Scientific / Statistical Analytics

```
Charts + stats: Plotly.js + react-plotly.js
Network graphs: Cytoscape.js + react-cytoscapejs
Graph algorithms: graphology + graphology-metrics
```

---

## Quick Install Guide

### Option A: ECharts (everything in one library)
```bash
npm install echarts echarts-for-react echarts-gl
```
Covers: line, bar, pie, scatter, radar, treemap, sunburst, sankey, chord, heatmap, calendar, map, network graph, parallel, funnel, gauge, candlestick, boxplot, 3D scatter, 3D bar, 3D surface, globe

### Option B: Specialized stack
```bash
# Network graph analytics
npm install @antv/g6 @antv/graphin
# or
npm install cytoscape react-cytoscapejs cytoscape-dagre cytoscape-cola

# Standard charts
npm install recharts
# or
npm install @nivo/core @nivo/line @nivo/bar @nivo/pie @nivo/heatmap @nivo/treemap @nivo/sankey

# Maps
npm install react-map-gl mapbox-gl

# 3D
npm install @react-three/fiber @react-three/drei three
```

### Option C: Maximum flexibility (D3-based)
```bash
# Low-level React + D3
npm install @visx/network @visx/shape @visx/scale @visx/axis @visx/hierarchy @visx/geo @visx/chord @visx/heatmap
```
