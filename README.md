<div align="center">

# 🚗 DriveGraph
### *Interactive Autonomous Driving Simulation & Explainable AI Platform*

<br/>

[![Version: 1.0.0](https://img.shields.io/badge/Version-1.0.0-00E676?style=for-the-badge&logo=semver&logoColor=white)](#)
[![Runtime: Vanilla JS](https://img.shields.io/badge/Stack-Vanilla_JS_%7C_Canvas_2D-00B0FF?style=for-the-badge&logo=javascript&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API)
[![Dependencies: Zero](https://img.shields.io/badge/Dependencies-Zero_External_Libs-7C4DFF?style=for-the-badge&logo=npm&logoColor=white)](#-quickstart)
[![Perception: Raycasting](https://img.shields.io/badge/Perception-Raycasting_Radar-FF9100?style=for-the-badge&logo=radar&logoColor=white)](#-core-features)
[![Explainability: XAI](https://img.shields.io/badge/XAI-Hyperplane_Decision_Bounds-FF1744?style=for-the-badge&logo=target&logoColor=white)](#-core-features)
[![License: MIT](https://img.shields.io/badge/License-MIT-00E5FF?style=for-the-badge&logo=open-source-initiative&logoColor=white)](LICENSE)

<br/>

**DriveGraph** is a high-performance, lightweight, zero-dependency autonomous vehicle simulation platform and Explainable AI (XAI) cockpit. Built entirely in modern Vanilla JavaScript and native HTML5 Canvas 2D, DriveGraph delivers a fully interactive sandbox for training, inspecting, and visualizing neural-controlled autonomous vehicles navigating complex OpenStreetMap GIS urban environments in real time.

<br/>

<img src="Satellite%20Map%20View.jpeg" alt="DriveGraph Autonomous Vehicle Simulation Viewport" width="100%" style="border-radius: 12px; box-shadow: 0 12px 36px rgba(0, 0, 0, 0.45); border: 1px solid rgba(255,255,255,0.1);" />

*DriveGraph Simulation Engine: Live multi-ray perception, Minkowski road envelopes, traffic light coordination, and 3D isometric urban architecture.*

</div>

---

## 🌟 Product Overview

DriveGraph bridges the gap between autonomous vehicle policy training and visual interpretability. Rather than treating vehicle control as a black box, DriveGraph exposes every layer of the intelligence pipeline in real time:

- **Full-Stack Simulation in the Browser:** Zero installation, zero heavy C++ dependencies, and zero GPU configuration. Runs at a smooth 60 FPS in any modern web browser.
- **True White-Box Explainability:** Inspect live synaptic activations, weight potentials, and 2D hyperplane decision boundaries as the vehicle negotiates intersections, pedestrians, and traffic signals.
- **Real-World GIS Virtual Worlds:** Ingest real OpenStreetMap (OSM) cartographic road networks, extruded automatically into navigable polygon road meshes with Minkowski sum geometry.
- **Autonomous Evolutionary Learning:** Train vehicle brains directly in the browser using multi-agent evolutionary algorithms with instant weight saving, exporting, and reloading.

---

## 📸 Product Interface & Visual Intelligence

<table align="center" width="100%">
  <tr>
    <th width="50%" align="center"><b>🧠 Live Neural Policy Inspector</b></th>
    <th width="50%" align="center"><b>🗺️ Tactical Radar MiniMap & Path Planner</b></th>
  </tr>
  <tr>
    <td align="center">
      <img src="Neural%20Architecture%20Working.jpeg" width="100%" alt="Neural Architecture Working" style="border-radius: 8px; border: 1px solid rgba(255,255,255,0.1);" />
    </td>
    <td align="center">
      <img src="Route%20Map%20View.jpeg" width="100%" alt="Route Map View" style="border-radius: 8px; border: 1px solid rgba(255,255,255,0.1);" />
    </td>
  </tr>
  <tr>
    <td align="justify">
      <b>Interactive Neural Dashboard:</b> Displays real-time feedforward neuron signals, synaptic weight connections, threshold biases, and directional control outputs (<code>🠉</code> Throttle, <code>🠈</code> Steer Left, <code>🠊</code> Steer Right, <code>🠋</code> Reverse). Allows direct manual tuning, parameter freezing, and zeroing.
    </td>
    <td align="justify">
      <b>Global Spatial Navigation:</b> Real-time circular radar HUD tracking the complete city road graph, target destinations, surrounding traffic, and active Dijkstra shortest-path navigation corridors guiding the autonomous agent to designated waypoints.
    </td>
  </tr>
</table>

---

## ⚡ Core Features

### 📡 Multi-Ray Perception Suite
- **Proximity Radar:** Casts customizable angular fans of rangefinder rays ($N=3\text{--}5$, length $250\text{px}$) that calculate ray-segment intersections against road boundaries and surrounding vehicles using 2D parametric vector cross products.
- **Semantic Sign Detectors:** Dedicated perception channels for detecting Stop Signs, Traffic Lights, Yield Markings, and Pedestrian Crosswalks.
- **Destination Heading Vector:** Computes the normalized signed angular misalignment ($\theta_{\text{target}} \in [-1, 1]$) between the vehicle's heading vector and target destination.

### 🧠 White-Box Explainable AI (XAI)
- **Live Decision Boundary Visualizer:** Computes high-resolution ($300 \times 300$) 2D hyperplane slices across user-selected sensor input dimensions. Regions are dynamically color-coded by the activated vehicle control command, visualizing decision margins and policy boundaries in real time.
- **Dynamic Synapse Flow:** Visualizes directional signal pulses along neural connections synchronized with the simulation clock.

### 🗺️ GIS Road Mesh & Spatial Engine
- **OpenStreetMap (OSM) Ingestion:** Parses Overpass API JSON road and building data into simulation coordinates.
- **Minkowski Road Envelopes:** Automatically dilates 1D road centerlines into 2D polygon road surfaces with smooth, rounded junction caps.
- **Spatial Grid Indexing:** Utilizes a $500\text{px} \times 500\text{px}$ spatial hashing grid for $O(1)$ collision checks and viewport rendering optimization.
- **Dijkstra Waypoint Routing:** Computes optimal route corridors across the road network to user-selected destination targets.

### 🧬 Evolutionary Multi-Agent Training
- **Population Evaluation:** Spawns parallel vehicle agents ($N=4$ to $10$) competing across urban traffic scenarios.
- **Parameter Mutation:** Evolves synaptic weights and bias thresholds using linear interpolation (`lerp`) toward random parameter distributions.
- **One-Click State Management:** Save the best-performing vehicle brain to browser `localStorage` or export as a lightweight `.car` JSON file for sharing.

### 🛞 Seamless Manual Override
- Switch instantly between autonomous AI neural control and manual human keyboard driving with the click of a button.

---

## 🏗 Software Pipeline

```
+-----------------------------------------------------------------------------------------+
|                                  DRIVEGRAPH RUNTIME LOOP                                |
+-----------------------------------------------------------------------------------------+
                                             │
      ┌──────────────────────────────────────┴──────────────────────────────────────┐
      │                                                                             │
+-----▼------------------------------------+   +------------------------------------▼-----+
|           PERCEPTION ENGINE              |   |          SPATIAL GIS ENGINE              |
+------------------------------------------+   +------------------------------------------+
| • Ray-cast Obstacle Intersections        |   | • Spatial Grid Range Lookups (O(1))      |
| • Semantic Sign Sensors (Stop/Light/..)  |   | • Minkowski Polygon Road Envelopes       |
| • Destination Heading Angle Calculation  |   | • Dijkstra Shortest Path Corridors       |
+------------------------------------------+   +------------------------------------------+
      │                                                                             │
      └──────────────────────────────────────┬──────────────────────────────────────┘
                                             │ [Normalized Input Vector]
                                   +---------▼---------+
                                   | NEURAL CONTROLLER |
                                   | (Feedforward MLP) |
                                   +---------┬---------+
                                             │ [Directional Control Signals]
      ┌──────────────────────────────────────┴──────────────────────────────────────┐
      │                                                                             │
+-----▼------------------------------------+   +------------------------------------▼-----+
|           KINEMATICS ENGINE              |   |          EXPLAINABILITY (XAI)            |
+------------------------------------------+   +------------------------------------------+
| • Euler Position & Heading Integration   |   | • 2D Hyperplane Decision Boundary Grid   |
| • Velocity Clamping & Friction Drag      |   | • Dynamic Neural Activation Graph        |
| • Quad-Vertex Polygon Collision Checks   |   | • Real-time Radar MiniMap HUD            |
+------------------------------------------+   +------------------------------------------+
                                             │
                                   +---------▼---------+
                                   |  HTML5 CANVAS 2D  |
                                   | 60 FPS RENDER LOOP|
                                   +-------------------+
```

---

## 🚀 Quickstart

DriveGraph requires **no build step, no bundler, and zero runtime dependencies**.

### Prerequisites
- Any modern web browser (Google Chrome, Microsoft Edge, Mozilla Firefox, Safari).
- Node.js (v16+) **or** Python (3.8+) for hosting local static files.

### Method 1: Node.js (Recommended)
```bash
# 1. Install local development server
npm install

# 2. Launch DriveGraph on port 3000
npm start
```
Open **`http://localhost:3000`** in your browser.

### Method 2: Python HTTP Server (Zero Install)
```bash
# Launch lightweight HTTP server directly
python -m http.server 3000
```
Open **`http://localhost:3000`** in your browser.

### Method 3: Direct Browser Launch
Double-click `index.html` or open it directly in your browser. Running through a local server (Methods 1 or 2) is recommended for unrestricted browser `localStorage` persistence.

---

## ⌨️ User Controls & Dashboard Guide

Developed as part of research into autonomous vehicle control algorithms and spatial simulation modeling.

### Canvas Viewport Navigation

| Action | Input |
|---|---|
| **Pan Canvas** | Middle Mouse Button + Drag or Right Mouse Button + Drag |
| **Zoom View** | Mouse Scroll Wheel |

### Dashboard Toolbar

| Control | Tooltip | Action |
|---|---|---|
| 📁 | `Load .car` | Imports and loads an existing vehicle neural-brain file. |
| 💾 | `Save` | Saves the best-performing vehicle's neural weights to `localStorage`. |
| ⬇️ | `Download` | Exports the active vehicle state as a `.car` JSON file. |
| 🗑️ | `Discard` | Clears saved neural-network parameters from `localStorage`. |
| 💀 | `Damage` | Marks the active car as damaged to trigger a respawn. |
| 0️⃣ | `Zero` | Resets neural-network weights and biases to zero. |
| ✅ | `Mark All` | Selects weights and biases for evolutionary mutation. |
| ⬜ | `Unmark All` | Excludes selected parameters from mutation. |
| ❌ | `Remove` | Clears connection segments in the interactive neural editor. |
| ⚙️ | `Options` | Opens configuration options for sensors and inputs. |
| 🌎 | `Load World` | Imports a custom `.world` map file. |
| ⚡ | `Optimize` | Activates the parallel vehicle population for evolutionary optimization. |
| 🔎 | `Reset / Test` | Reloads the simulation environment. |

### Driving & Navigation

| Control | Type | Function |
|---|---|---|
| 🛞 | Manual Override | Toggles between autonomous neural control and manual keyboard control. |
| Arrow Keys | Keyboard | Up: accelerate; Down: reverse; Left/Right: steer. |
| 🎯 Going To | Dropdown | Selects a navigation destination, such as Wärtsilä, Solenovo, Karelics, or UEF. |

---

## 🗺️ Custom Environments & GIS Map Ingestion

DriveGraph includes a spatial world editor and GIS conversion functionality:

1. Obtain urban road-network data from [OpenStreetMap](https://www.openstreetmap.org/) using supported Overpass API queries.
2. The built-in parser converts OSM nodes and highway ways into graph segments with road metadata.
3. Road segments are converted into polygonal road geometry.
4. Place traffic signals, stop signs, crosswalks, parking stalls, and destination waypoints using the world editor.

---

## 🛠️ Product Customization & Configuration

The in-app Options Panel and source code provide configuration options, depending on the active implementation:

- **Sensor tuning:** Configure ray count, ray length, spread angle, and offset where supported.
- **Network architecture:** Configure hidden-layer sizes where supported by the network implementation.
- **Sensor features:** Select available inputs such as speed, traffic-control cues, crosswalks, and target heading.
- **Mutation rate:** Adjust mutation intensity to influence evolutionary exploration.

---

## 📜 Open-Source Lineage & Credits

DriveGraph builds upon and extends the educational simulation work of **Dr. Radu Mariescu-Istodor**, associated with Karelia University of Applied Sciences, Joensuu, Finland:

- *Self-Driving Car with JavaScript*
- *Virtual World Simulation Engine*

The project retains foundational simulation components and adds or integrates features including:

- 2D hyperplane decision-boundary visualization for inspecting neural-network behavior.
- Semantic perception detectors for traffic signals, stop signs, and crosswalks.
- Destination-heading calculations for goal-oriented navigation.
- Interactive visualization and dashboard tools.

The precompiled city environment represents **Joensuu, North Karelia, Finland**. Geographic data is associated with [OpenStreetMap](https://www.openstreetmap.org/), which distributes data under the Open Database License (ODbL), subject to its attribution requirements.

See the project license and upstream sources for the applicable licensing and attribution terms.

---

## 📄 License

DriveGraph is distributed under the **MIT License**, subject to verification of the applicable license and attribution requirements for inherited components. See the [`LICENSE`](LICENSE) file for details.