# Flourish.studio - Rendering Technology Stack Research

## Critical Finding: Flourish Does NOT Use React

Flourish.studio is **not built with React**. It uses **vanilla JavaScript** with a custom template system powered by **D3.js** as the primary rendering engine. Flourish templates are standalone JavaScript modules bundled with Rollup -- not React components.

The Flourish platform consists of:
- A **proprietary template engine** (closed-source) that manages visualization lifecycle
- An **open-source SDK** (`@flourish/sdk`) for building custom templates
- A collection of **open-source helper modules** (`@flourish/*`) published on npm
- Templates rendered via **SVG** (D3.js), **Canvas**, and **WebGL** (for 3D)

---

## Core Rendering Libraries

### D3.js (Primary Rendering Engine)

D3.js is the backbone of nearly every Flourish visualization. The following D3 modules are used across `@flourish/*` packages:

| D3 Module | Used In | Purpose |
|---|---|---|
| `d3-selection` | chart-layout, legend, controls, facets, info-popup, slider | DOM manipulation, bindind data to elements |
| `d3-scale` | chart-layout, colors, legend, facets, slider | Mapping data domains to visual ranges |
| `d3-transition` | chart-layout, facets, info-popup | Animated transitions between states |
| `d3-geo` | geo, geo-toolkit | Map projections, geographic path rendering |
| `d3-array` | legend, colors | Array utilities (min, max, extent, etc.) |
| `d3-interpolate` | colors | Color and value interpolation |
| `d3-scale-chromatic` | colors | Color schemes (sequential, diverging, categorical) |
| `d3-format` | data-popup, info-popup, slider | Number formatting |
| `d3-time-format` | chart-layout, layout | Date/time formatting |
| `d3-color` | geo, info-popup, layout | Color parsing and manipulation |
| `d3-axis` | slider | Axis rendering |
| `d3-collection` | colors | Grouping and nesting data |
| `d3-timer` | info-popup | Animation timing |
| `d3-dsv` | sdk | CSV/TSV parsing |

### Mapbox GL JS (3D Maps)

Flourish's 3D map templates (globe, extruded regions, point maps with base maps, satellite raster tiles) use **Mapbox GL JS** for WebGL-based map rendering. The `@flourish/geo-toolkit` package depends on `@mapbox/geojson-rewind` for GeoJSON processing, confirming integration with the Mapbox ecosystem.

### Three.js (3D Viewer / 3D Globe)

The "3D Viewer" templates (Area chart 3D, Flourish logo 3D, Underwater) and "3D Globe" templates use **Three.js** for WebGL 3D scene rendering. These dependencies are inside Flourish's closed-source template code, not in the public npm packages.

### deck.gl (3D Map Layers)

For advanced 3D map visualizations like extruded regions, heatmaps, and arc maps, Flourish uses **deck.gl** on top of Mapbox GL JS. This provides GPU-accelerated geospatial layers.

---

## Flourish Module Architecture

Flourish templates follow a specific lifecycle pattern (not React). Each template exports three functions:

```javascript
export var state = { /* bound settings */ };
export var data = { /* bound data */ };

export function draw() { /* initial render */ }
export function update() { /* re-render on state/data change */ }
```

### Published @flourish Modules (npm)

These are the building blocks that Flourish templates compose together:

#### Layout & Structure
| Package | Description | Key Dependencies |
|---|---|---|
| `@flourish/layout` | Master layout controller (header, footer, body) | d3-color, d3-time-format, fflate, file-saver-es |
| `@flourish/chart-layout` | Axes, scales, chart area management | d3-scale, d3-selection, d3-transition |
| `@flourish/facets` | Small-multiple grid layouts | d3-scale, d3-selection, d3-transition |
| `@flourish/header` | Chart header/title | (internal) |
| `@flourish/footer` | Chart footer/source/notes | (internal) |

#### Data & Color
| Package | Description | Key Dependencies |
|---|---|---|
| `@flourish/colors` | Color scale settings and generation | d3-scale, d3-interpolate, d3-scale-chromatic |
| `@flourish/color-generator` | Programmatic color generation | (internal) |
| `@flourish/interpreter` | Auto-detect data types (numeric, date, string) | (internal) |
| `@flourish/transform-data` | Reshape/pivot data | (internal) |
| `@flourish/filter` | Data filtering and aggregation | (internal) |
| `@flourish/stats` | Statistical functions | (internal) |
| `@flourish/formatters` | Number and datetime formatting | (internal) |
| `@flourish/number-formatter` | Number formatting | (internal) |
| `@flourish/number-localization` | Locale-aware number separators | (internal) |

#### Interactivity & UI
| Package | Description | Key Dependencies |
|---|---|---|
| `@flourish/controls` | Dropdown/buttons/slider controls | d3-selection, @flourish/slider |
| `@flourish/slider` | Range slider component | d3-axis, d3-scale, d3-selection |
| `@flourish/popup` | Tooltip/popup container | terser (build only) |
| `@flourish/data-popup` | Data-bound popup | d3-format, @flourish/popup |
| `@flourish/info-popup` | Rich info popup | d3-selection, d3-transition, d3-timer |
| `@flourish/legend` | Legend component | d3-array, d3-scale, d3-selection |
| `@flourish/search` | Searchable data filtering | (internal) |
| `@flourish/axes-highlights` | Axis hover highlighting | (internal) |
| `@flourish/url-state` | URL hash state management | (internal) |

#### Geographic
| Package | Description | Key Dependencies |
|---|---|---|
| `@flourish/geo` | Geographic rendering primitives | d3-geo, d3-color |
| `@flourish/geo-toolkit` | Geographic analysis utilities | d3-geo, @mapbox/geojson-rewind |

#### Utilities
| Package | Description |
|---|---|
| `@flourish/pocket-knife` | General-purpose utility functions |
| `@flourish/js2css` | Convert JS style objects to CSS |
| `@flourish/ui-styles` | Shared UI styling |
| `@flourish/utils-color` | Color utility functions |
| `@flourish/utils-env` | Environment detection |
| `@flourish/enhanced-arrays` | Immutable array-like objects with helper methods |
| `@flourish/store` | State store with change tracking |
| `@flourish/font-watcher` | Trigger re-render when web fonts load |
| `@flourish/smooth-resize` | Animated container resizing |

#### SDK & API
| Package | Description |
|---|---|
| `@flourish/sdk` | CLI for developing custom Flourish templates |
| `@flourish/live-api` | Embed and control Flourish visualizations programmatically |

---

## How Each Visualization Category Maps to Technology

| Visualization Category | Primary Rendering | Libraries Used |
|---|---|---|
| **Line/Area/Bar/Column charts** | SVG via D3.js | d3-selection, d3-scale, d3-transition, @flourish/chart-layout |
| **Pie/Donut charts** | SVG via D3.js | d3-shape (arc generator), d3-selection |
| **Scatter/Bubble plots** | SVG via D3.js | d3-selection, d3-scale, d3-force (beeswarm) |
| **Projection maps (2D)** | SVG via D3.js | d3-geo, @flourish/geo, @flourish/geo-toolkit |
| **3D Maps/Globe** | WebGL | Mapbox GL JS, deck.gl, Three.js |
| **Marker maps** | WebGL + HTML overlays | Mapbox GL JS |
| **Network graphs** | SVG + Canvas via D3.js | d3-force, d3-selection |
| **Sankey/Alluvial** | SVG via D3.js | d3-sankey (or custom), d3-selection |
| **Treemap/Sunburst/Hierarchy** | SVG via D3.js | d3-hierarchy, d3-selection |
| **Radar/Radial charts** | SVG via D3.js | d3-selection, trigonometric math |
| **Heatmaps** | SVG/Canvas via D3.js | d3-selection, d3-scale (color) |
| **Tables** | HTML DOM | Vanilla JS, CSS |
| **Cards/Profiles** | HTML DOM | Vanilla JS, CSS |
| **Pictograms/Icons** | SVG | d3-selection or inline SVG |
| **Bar chart race / Line chart race** | SVG via D3.js + animation | d3-selection, d3-transition, d3-timer, requestAnimationFrame |
| **Election results** | SVG via D3.js | d3-selection, custom parliament layouts |
| **Chord diagrams** | SVG via D3.js | d3-chord, d3-ribbon, d3-selection |
| **Slope/Parallel coordinates** | SVG via D3.js | d3-selection, d3-scale |
| **Marimekko** | SVG via D3.js | d3-selection, d3-scale (partitioned) |
| **Timeline** | HTML + SVG | Vanilla JS, d3-selection |
| **Interactive SVG** | SVG DOM manipulation | d3-selection or vanilla JS |
| **Photo slider** | HTML + CSS | Vanilla JS |
| **Calculator/Quiz** | HTML DOM | Vanilla JS |
| **Gantt chart** | SVG via D3.js | d3-selection, d3-scale (time) |
| **Word cloud** | SVG/Canvas | d3-cloud (Jason Davies), d3-selection |
| **Sports visualizations** | SVG + Canvas | d3-selection, custom coordinate systems |
| **Audio player** | HTML5 Audio API | Vanilla JS |
| **3D Viewer** | WebGL | Three.js |
| **Connections Globe** | WebGL | Three.js, custom globe geometry |
| **Arc/Flow maps** | WebGL layers on map | Mapbox GL JS, deck.gl (ArcLayer) |
| **Gauge** | SVG via D3.js | d3-selection, d3-arc |
| **Tournament bracket** | SVG/HTML | d3-selection or vanilla JS |
| **Calendar** | HTML DOM / SVG | d3-selection, d3-time |
| **Number ticker** | HTML DOM + CSS animation | Vanilla JS |
| **Data explorer** | HTML + SVG composite | Multiple @flourish modules |
| **Survey charts** | SVG via D3.js | d3-selection, d3-scale |
| **Draw the line** | SVG + Canvas | d3-selection, pointer events |
| **Parliament chart** | SVG via D3.js | d3-selection, custom seat layout algorithm |
| **Countdown** | HTML DOM + CSS | Vanilla JS |
| **Text annotator** | HTML DOM | Vanilla JS |

---

## Embedding: The @flourish/live-api

When Flourish visualizations are embedded on external websites, they run inside **iframes**. The `@flourish/live-api` package provides a JavaScript API to:
- Dynamically create and update Flourish visualizations
- Change data and settings programmatically
- Listen for events from the visualization

This is NOT a React component -- it's a vanilla JS library that creates/manages iframes.

There are community wrappers for frameworks:
- `flourish-sdk-react-native` -- React Native wrapper
- `flourish-web-sdk-react` -- React web wrapper
- `flourish-web-sdk-angular` -- Angular wrapper

These wrappers simply wrap the iframe-based `@flourish/live-api` in framework-specific components.

---

## Summary

**Flourish does not use React for rendering visualizations.** The entire rendering stack is:

1. **D3.js** -- Core rendering for all SVG/Canvas-based 2D charts, maps, and diagrams
2. **Mapbox GL JS** -- WebGL map rendering (tile maps, satellite, markers)
3. **deck.gl** -- GPU-accelerated geospatial layers (3D maps, arcs, heatmaps)
4. **Three.js** -- 3D scene rendering (3D viewer, 3D globe)
5. **Vanilla JavaScript** -- DOM manipulation for tables, cards, HTML-based templates
6. **HTML5 Canvas** -- High-performance rendering for dense visualizations (network graphs, large scatters)
7. **CSS Animations** -- Transitions and visual effects

The `@flourish/sdk` uses **Rollup** (not webpack) for bundling templates. The template system is a custom lifecycle model (`draw`/`update`) -- not a component-based framework like React, Vue, or Svelte.

If you want to replicate Flourish's capabilities in a React application, you would use these equivalent React-compatible libraries:
- **recharts** or **visx** (React + D3 wrappers) for standard charts
- **react-map-gl** (React wrapper for Mapbox GL JS) for maps
- **@react-three/fiber** (React wrapper for Three.js) for 3D
- **deck.gl** with `@deck.gl/react` for 3D map layers
- **nivo** for pre-built D3-based React chart components
- **react-force-graph** for network visualizations
