# 🚗 DriveGraph: Explainable AI Autonomous Driving Simulator

![Project Status](https://img.shields.io/badge/Status-Active-brightgreen.svg)
![XAI Paradigm](https://img.shields.io/badge/Focus-Explainable_AI_(XAI)-red.svg)
![Technology Stack](https://img.shields.io/badge/Tech-Vanilla_JS_%7C_HTML5_Canvas-blue.svg)
![Dependencies](https://img.shields.io/badge/Dependencies-Zero_Runtime-success.svg)
![AI Framework](https://img.shields.io/badge/AI-Custom_Neural_Network_%2B_Genetic_Algorithm-purple.svg)
![GIS Integration](https://img.shields.io/badge/GIS-OpenStreetMap_(OSM)_Parser-orange.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)

**DriveGraph** is a high-performance, lightweight, end-to-end **Explainable AI (XAI) Autonomous Driving & Spatial Perception Simulator**. Built from first principles in pure Vanilla JavaScript and native HTML5 Canvas 2D, **DriveGraph** addresses the "black box" problem of autonomous vehicle control by combining real-time hyperplane decision boundary rendering, an interactive Graph Neural Network (GNN) visualizer/editor, ray-casting sensor perception, multi-agent genetic evolutionary learning, OpenStreetMap (OSM) GIS graph parsing, and a multimodal vehicle transformation framework.

---

## 📊 Key Repository Facts & Empirical Statistics

| Feature / Metric | Quantitative Value / Specification | Description |
| :--- | :--- | :--- |
| **XAI Inspection Depth** | `100% White-Box` Real-time Interpretability | Hyperplane decision boundaries & GNN live graph weight editor |
| **Core Runtime Dependencies** | `0` (Zero external frameworks) | 100% native Web APIs, ES6 Modules, Canvas 2D |
| **Total Source Code Base** | `40+` modular files (~6,800+ lines of JS) | Completely decoupled modular engineering |
| **Pre-baked Benchmark Map** | `~7.0 MB` (`many_targets_small.html`) | Complex city graph with hundreds of road segments & targets |
| **Target Frame Rate** | `60 FPS` deterministic execution | Smooth physics, ray-casting, and dynamic rendering loop |
| **Simulation Population** | `1` to `1,000+` parallel vehicle agents | Multi-agent genetic evolutionary learning in real-time |
| **Spatial Grid Cell Size** | `500px × 500px` spatial hashing | $O(1)$ dynamic spatial range queries for collision detection |
| **Sensor Ray Densities** | Up to `20` obstacle rays + `7` traffic light rays | Proximity radar, signal sensors, & target vector tracker |
| **Road Width Standard** | `100px` (Roundness: `10` vertices) | Minkowski sum polygon envelope generation |
| **Vehicle Scale** | `30px` (Width) × `50px` (Height) | Quad-vertex polygon physics bounds with rotational transform |
| **Multimodal Modes** | Ground Car 🚗, Aquatic Boat 🛥️, Aerial Helicopter 🚁 | Terrain-responsive vehicle kinematic transformations |

---

## 🏗 System Architecture & Pipeline Overview

```
+-----------------------------------------------------------------------------------+
|                                   DRIVEGRAPH ENGINE                               |
+-----------------------------------------------------------------------------------+

                                         |
     +-----------------------------------+-----------------------------------+
     |                                                                       |
+----v-----------------------------+                   +---------------------v-----------------------+
|          WORLD SUBSYSTEM         |                   |            CAR / AI SUBSYSTEM               |
|      (WORLD/js/ & Editor)        |                   |             (CAR/ & Submodules)             |
+----------------------------------+                   +---------------------------------------------+
| • Spatial Graph Core (Point/Seg) |                   | • Vehicle Kinematics Engine (Car/Boat/Heli) |
| • Minkowski Road Envelopes       |                   | • Multi-Ray Casting Sensors (Obstacles/Signs)|
| • Polygon Union & Cut Algorithms |                   | • Neural Network Feedforward Logic          |
| • Spatial Hashing Grid Indexing  |                   | • Genetic Evolutionary Mutation Engine      |
| • OpenStreetMap (OSM) Converter  |                   | • GNN Graph Neural Editor & Weights Tweaker |
| • Marking Editors (Light/Stop/..) |                   | • Hyperplane Decision Boundary Visualizer    |
| • Pseudo-3D Isometric Facades    |                   | • MiniMap & Target Vector Heading Tracker   |
+----------------------------------+                   +---------------------------------------------+
     |                                                                       |
     +-----------------------------------+-----------------------------------+
                                         |
                               +---------v---------+
                               | HTML5 CANVAS 2D   |
                               |  RENDER ENGINE    |
                               +-------------------+
```

---

## 🔬 Mathematical Foundations & Algorithmic Design

### 1. Vehicle Kinematics & Translational Motion
The vehicle position $(x, y)$ and heading angle $\theta$ are updated at each simulation tick based on acceleration $a$, maximum velocity $v_{\max}$, friction $\mu$, and steering differential $\Delta\theta$:

$$\text{Speed Update: } v_{t+1} = \text{clamp}\left( v_t + a_{\text{control}} - \text{sign}(v_t) \cdot \mu, \, -\frac{v_{\max}}{2}, \, v_{\max} \right)$$

$$\text{Heading Angle: } \theta_{t+1} = \theta_t + \text{sign}(v_t) \cdot \Delta\theta \cdot (\delta_{\text{left}} - \delta_{\text{right}})$$

$$\text{Position Coordinates: } x_{t+1} = x_t - \sin(\theta_{t+1}) \cdot v_{t+1}, \quad y_{t+1} = y_t - \cos(\theta_{t+1}) \cdot v_{t+1}$$

### 2. Sensor Ray-Casting & Line Segment Intersection
Intersection detection between sensor rays $R = (P_1, P_2)$ and road segment borders $S = (P_3, P_4)$ uses vector cross products:

$$t = \frac{(x_4 - x_3)(y_1 - y_3) - (y_4 - y_3)(x_1 - x_3)}{(y_4 - y_3)(x_2 - x_1) - (x_4 - x_3)(y_2 - y_1)}$$

$$u = \frac{(x_2 - x_1)(y_1 - y_3) - (y_2 - y_1)(x_1 - x_3)}{(y_4 - y_3)(x_2 - x_1) - (x_4 - x_3)(y_2 - y_1)}$$

A valid intersection occurs if and only if $0 \le t \le 1$ and $0 \le u \le 1$. The normalized reading distance returned to the network is $1 - \min(t)$.

### 3. Target Vector Heading Alignment Angle
The directional feature provided to the vehicle neural network (🎯 extra input feature) computes the normalized angle between the car's orientation vector $\vec{v}_{\text{car}}$ and the target destination vector $\vec{v}_{\text{target}}$:

$$\theta_{\text{target}} = \frac{\arccos\left(\frac{\vec{v}_{\text{car}} \cdot \vec{v}_{\text{target}}}{\|\vec{v}_{\text{car}}\| \|\vec{v}_{\text{target}}\|}\right) \cdot \text{sign}(\vec{v}_{\text{car}} \times \vec{v}_{\text{target}})}{\pi} \quad \in [-1, 1]$$

### 4. Neural Network & Genetic Mutation Engine
Each layer output $\vec{y}$ given input vector $\vec{x}$, weight matrix $\mathbf{W}$, and bias vector $\vec{b}$ is computed via binarized step thresholding or continuous activation:

$$y_i = \mathbb{I}\left( \sum_{j} x_j W_{ji} - b_i > 0 \right)$$

Genetic evolutionary mutation mutates weights and biases using linear interpolation ($\text{lerp}$) towards random uniform distribution $U(-1, 1)$:

$$W_{\text{new}} = \text{lerp}(W_{\text{old}}, \, U(-1, 1), \, \alpha), \quad \text{where } \text{lerp}(a, b, t) = a + (b - a) \cdot t$$

### 5. Spatial Graph Road Envelopes & Mercator GIS Projection
Road segments are extruded into 2D polygon envelopes using Minkowski distance offsets around segment vectors. OpenStreetMap (OSM) latitude/longitude coordinates $(\phi, \lambda)$ are projected into Cartesian simulation coordinates using Mercator projection equations:

$$x = R \cdot (\lambda - \lambda_0), \quad y = R \cdot \ln\left(\tan\left(\frac{\pi}{4} + \frac{\phi}{2}\right)\right)$$

---

## ⚡ Multimodal Vehicle Transformations

The simulator features adaptive environment-based vehicle mode transitions:

| Vehicle Mode | Trigger Condition | Visual Appearance | Kinematic & Collision Behavior |
| :--- | :--- | :--- | :--- |
| 🚗 **Car Mode** | Default ground surface | Red/Blue body tint mask | Standard road kinematics; collides with road borders & obstacles. |
| 🛥️ **Boat Mode** | Entering aquatic polygons (`Water`) | Vessel silhouette mask | Aquatic surface navigation with water friction characteristics. |
| 🚁 **Helicopter Mode** | Triggered flight state | Dynamic rotating rotor blade overlay | Aerial flight on Layer 1; **invulnerable to road borders** (`damaged = false`). |

---

## 🗂 Codebase Structure & Directory Layout

```
virtualworld/
├── index.html                       # Top-level viewport wrapper (iframe loader)
├── package.json                     # NPM project manifest & dependencies
├── CAR/                             # Autonomous Vehicle Controls Module
│   ├── index.html                   # Primary CAD & Vehicle Controls Dashboard
│   ├── style.css                    # Modern dark UI theme stylesheet
│   ├── main.js                      # Main loop, car inspector & simulation controller
│   ├── car.js                       # Car class (Kinematics, polygon bounds, rendering)
│   ├── carInfo.js                   # Pre-baked trained vehicle state benchmark
│   ├── sensor.js                    # Ray-casting sensor suite (Obstacles, Signals, Radar)
│   ├── network.js                   # Multilayer Feedforward Neural Network & Mutator
│   ├── visualizer.js                # Neural Network real-time Canvas renderer
│   ├── decisionBoundary.js          # Single Output Hyperplane Decision Boundary
│   ├── multiDecisionBoundary.js     # Multi-Class Hyperplane Decision Boundary
│   ├── miniMap.js                   # Real-time MiniMap radar & target path renderer
│   ├── controls.js                  # Keyboard (WASD/Arrows) & AI control interface
│   ├── road.js                      # Classic multi-lane straight road model
│   ├── utils.js                     # Geometric math, linear algebra, color helpers
│   ├── imgs/                        # Institutional & partner logo assets (14 PNGs)
│   └── new_nn/                      # Graph Neural Network (GNN) Submodule
│       ├── nn.js                    # Graph-based Neural Network topology
│       └── nnEditor.js              # Interactive drag-and-drop GNN editor
└── WORLD/                           # Spatial World & Map Editor Submodule
    ├── saves/                       # Saved spatial maps & benchmark HTML files
    │   └── many_targets_small.html  # ~7MB complex city graph benchmark map
    └── js/                          # Spatial GIS & Graph Engine
        ├── world.js                 # World orchestrator (Envelopes, 3D buildings, trees)
        ├── viewport.js              # Zoom, pan, coordinate system transformer
        ├── grid.js                  # Spatial Hashing Grid indexing ($O(1)$ lookups)
        ├── math/                    # Spatial Mathematics
        │   ├── graph.js             # Vertex/Edge Graph data structure
        │   ├── osm.js               # OpenStreetMap (OSM) XML parser & converter
        │   └── utils.js             # Nearest segment projection & distance algorithms
        ├── primitives/              # Geometric Primitives
        │   ├── point.js             # Point (x, y) primitive with equality checks
        │   ├── segment.js           # Line Segment primitive (p1, p2, layer, oneWay)
        │   ├── polygon.js           # Multi-vertex Polygon with union/intersection
        │   └── envelope.js          # Road Segment Envelope Minkowski extruder
        ├── items/                   # World Environment Decorators
        │   ├── building.js          # Extruded 3D Isometric Buildings & Facades
        │   ├── tree.js              # Canopy Trees with alpha-blended foliage
        │   └── water.js             # Polygonal Shoreline Water Bodies
        ├── markings/                # Dynamic Traffic Markings
        │   ├── marking.js           # Abstract Base Marking
        │   ├── light.js             # Animated 3-state Traffic Signal
        │   ├── stop.js              # Stop Sign Marking & Border
        │   ├── yield.js             # Yield Sign Marking & Border
        │   ├── crossing.js          # Zebra Pedestrian Crosswalk
        │   ├── parking.js           # Designated Parking Bays
        │   ├── start.js             # Simulation Spawn Marker
        │   └── target.js            # Target Waypoint Destination
        └── editors/                 # Interactive Spatial Graph Editors
            ├── graphEditor.js       # Main Graph Point/Segment Draw & Delete Editor
            ├── markingEditor.js     # Abstract Marking Editor base
            ├── lightEditor.js       # Traffic Light Placement Tool
            ├── stopEditor.js        # Stop Sign Placement Tool
            ├── yieldEditor.js       # Yield Sign Placement Tool
            ├── crossingEditor.js    # Pedestrian Crossing Placement Tool
            ├── parkingEditor.js     # Parking Bay Placement Tool
            ├── startEditor.js       # Vehicle Spawn Point Tool
            └── targetEditor.js      # Navigation Target Placement Tool
```

---

## ⌨️ User Controls & Keyboard Shortcuts

### Editor & Canvas Navigation
| Action | Key / Input |
| :--- | :--- |
| **Pan Canvas View** | Middle Click Drag or Right Click Drag |
| **Zoom In / Out** | Mouse Scroll Wheel |
| **Add Spatial Graph Vertex** | Left Click on Canvas |
| **Connect Graph Vertices** | Left Click on first point $\to$ Left Click on target point |
| **Remove Point / Segment** | Right Click on point or segment |

### Simulation Control Buttons (Dashboard UI)
| UI Icon / Button | Function |
| :--- | :--- |
| 💾 **Save (`save()`)** | Saves current best vehicle's neural network to `LocalStorage` |
| 🗑️ **Discard (`discard()`)** | Clears saved neural weights to restart evolutionary training |
| 📥 **Download (`download()`)** | Exports vehicle brain parameters as `.car` JSON file |
| 🚁 **Helicopter Flight** | Switches current active vehicle to aerial flight mode |
| 🛑 **Traffic Light Switch** | Manually toggles traffic light states (Red / Yellow / Green) |

---

## 🚀 Quickstart Guide

### Prerequisites
- Node.js `v18.0+` or `v20.0+`
- Modern web browser with HTML5 Canvas support (Chrome, Edge, Firefox, Safari)

### Installation & Local Execution

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/GOKULRAM-K/DriveGraph-Explainable-AI-Autonomous-Driving-Simulator.git
   cd DriveGraph-Explainable-AI-Autonomous-Driving-Simulator
   ```

2. **Install Dependencies:**
   ```bash
   npm install
   ```

3. **Launch Local Server:**
   ```bash
   npm start
   ```
   Open your browser and navigate to `http://localhost:3000`.

---

## 📜 Academic Attribution & Credits

Developed as part of research into autonomous vehicle control algorithms and spatial simulation modeling under **Dr. Vignesh Vehicle Controls Laboratory**.

- **Primary Author / Lab**: Dr. Vignesh Vehicle Controls Related Research Group
- **License**: [MIT License](LICENSE)

> [!TIP]
> For customized map imports, simply export map files from [OpenStreetMap.org](https://www.openstreetmap.org) as XML (`.osm`), and upload them directly into the World Editor!
