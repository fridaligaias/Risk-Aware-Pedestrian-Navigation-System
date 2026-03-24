# 🚶‍♀️ SafeWalk: Risk-Aware Pedestrian Navigation System
### Safety-Optimized Pathfinding | Custom A* Implementation | **Applied AI (6COSC020W)**

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![OpenStreetMap](https://img.shields.io/badge/Data-OpenStreetMap-74BC1F?style=for-the-badge&logo=openstreetmap&logoColor=white)](https://www.openstreetmap.org/)
[![Pandas](https://img.shields.io/badge/Pandas-2.0-150458?style=for-the-badge&logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)](https://jupyter.org/)

---

## 🚀 Quick Access
For a deep dive into the code and live visualizations, check out the [Jupyter Notebook](./Cw1_w1905050_FridaliGaias.ipynb). For a 2-minute technical overview of the system architecture and results, read on below.

<p align="left">
  <a href="./Cw1_w1905050_FridaliGaias.ipynb">
    <img src="https://img.shields.io/badge/Open_Implementation_Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white" alt="Jupyter Notebook" />
  </a>
  <a href="https://data.police.uk/">
    <img src="https://img.shields.io/badge/Source_Crime_Data-blue?style=for-the-badge&logo=google-maps&logoColor=white" alt="Police.uk Data" />
  </a>
</p>

---

## 📌 My Project Overview
While AI has revolutionized vehicular transportation through autonomous driving and global logistics, there is a notable disparity in pedestrian safety. **SafeWalk** is a navigation prototype designed to calculate optimal walking routes by balancing physical distance with personal security risks derived from historical crime data.

### 🕵️ Application Area Review
Current transportation research often prioritizes operational speed over pedestrian security. SafeWalk fills this gap by shifting the focus toward urban mobility safety. The project utilizes **Convolutional Neural Networks (CNNs)** for environmental perception in the broader domain, but focuses on **Route Optimisation** using search techniques and predictive machine learning to model dynamic road conditions.

---

## 🧠 AI Technique Evaluation
To develop the "SafeWalk" system, three core AI methodologies were evaluated:

| Technique | Role in SafeWalk | Verdict |
| :--- | :--- | :--- |
| **A* Search** | Core pathfinding engine that balances distance and risk. | **Selected:** Optimal, complete, and mathematically transparent. |
| **K-Means Clustering** | Used to identify "danger zone" hotspots by grouping crime coordinates. | **Secondary:** Good for description, but cannot calculate valid paths. |
| **Neural Networks (ANN)** | Capable of modeling complex non-linear crime risk factors. | **Rejected:** Suffers from the "black box" problem, lacking decision transparency. |

---

## 🏗️ System Architecture & Data
The system is built on a modular architecture that integrates geospatial mapping with massive tabular datasets.

### 1. Input Data Sources
* **Street Network:** Retrieved via **OSMnx**, representing the environment as a `NetworkX MultiDiGraph` with nodes (coordinates) and edges (length).
* **Crime Statistics:** A tabular dataset of **1,000,000+ records** from Police.uk, containing coordinates and categorical crime types (e.g., "Theft", "Violence and sexual offences").

### 2. Pre-processing Pipeline
* **Bounding Box Filtering:** Optimizes memory by isolating crimes within the specific map area.
* **Severity Mapping:** Categorical labels are transformed into numerical weights via a severity dictionary.
* **Spatial Node Matching:** Utilizes **cKDTree** spatial indexing to map crime coordinates to the nearest graph intersections.

---

## Mathematical Heuristic
The pathfinding engine employs a weighted heuristic that penalizes high-risk edges. The total cost $f(n)$ for a node $n$ is defined as:

$$f(n) = g(n) + h(n)$$

#### Path Cost ($g(n)$)
The cost of the path from the start to node $n$ incorporates a safety penalty:
$$g(n) = \text{Distance} + (\text{Risk Score} \times \alpha)$$
* **$\alpha$ (Alpha):** A user-controlled parameter (0–100) used to trade efficiency for safety.
* **Risk Score:** The aggregated severity weight of all crimes associated with that node.

#### Heuristic 
The straight-line "best first" estimate to the goal is calculated using the Haversine/Geodesic formula to ensure the search remains admissible:

$$h(n) = \text{geodesic distance}(n, \text{goal})$$

---

## 📊 Testing & Evaluation
The system was verified through rigorous comparative testing to ensure both mathematical correctness and practical effectiveness.

* **Logic Verification:** Setting $\alpha = 0$ resulted in the "Safe Route" overlapping perfectly with the standard shortest path, confirming the admissibility of the heuristic.
* **Algorithmic Effectiveness:** Increasing Alpha successfully diverted paths away from high-density crime clusters (identified via heatmaps) in favor of longer, safer alternatives.
* **Performance:** Utilizing **vectorized operations** in Pandas and **cKDTree** indexing reduced processing time for 1M+ records from hours to seconds.

---


## Context
* **Institution:** University of Westminster
* **Module:** Applied AI
* **Date:** January 2026
