markdown
# OBCS: Open-source Below-Canopy Simulator

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)

**OBCS** (Open-source Below-Canopy Simulator) is a simulation environment for planning and validating autonomous UAV flights in semi-arid coppice forests, specifically designed for the Zagros oak (*Quercus brantii*) stands in western Iran.

It ingests a real photogrammetric point cloud and simulates a complete below‑canopy orbital inventory mission, integrating:

- 🧭 **Pure‑Python Feature‑Map SLAM** (ORB/SIFT, EKF, BoW loop closure, pose graph, bundle adjustment)
- 🎯 **Adaptive Dual‑mode Feature Detector (ADFD)** – dynamically weights ORB vs SIFT in real time
- 🚁 **Rotational Artificial Potential Field (R-APF)** with Simulated Annealing escape and Two-Phase Trajectory Anchoring (2PTA)
- 📊 **Downstream dendrometric extraction** – Diameter at Root Collar (DRC) and stem count

---

## 📦 Requirements

- Python 3.10 or higher
- Dependencies listed in [`requirements.txt`](requirements.txt)

Key libraries:
- `numpy`, `scipy`, `matplotlib`, `opencv-python`, `scikit-learn`, `imageio`, `open3d` (optional)

---

## 🛠️ Installation

### 1. Clone the repository
```bash
git clone https://github.com/mrzghasemiGit/OBCS.git
cd OBCS
2. Create and activate a virtual environment (recommended)
```bash
python -m venv venv
source venv/bin/activate   # On Windows: venv\Scripts\activate
3. Install dependencies
```bash
pip install -r requirements.txt
```
📂 Data
The simulator requires a PLY point cloud of a forest plot.
You can download the full dataset (the Zagros coppice plot used in the paper) from: (https://drive.iust.ac.ir/index.php/s/yBxsGFSBwKN83Rq)


🔗 Download final_combined_scene.ply

Place the file in the data/ folder and update the POINT_CLOUD_PATH variable in the notebook:

python
POINT_CLOUD_PATH = 'data/final_combined_scene.ply'
Note: If you want to test the code quickly, a downsampled version (10% of points) is available in the data/sample/ folder.

🚀 Usage
Launch Jupyter Notebook and run the main simulation:

bash
jupyter notebook notebooks/OBCS_simulator.ipynb
Run the cells sequentially. The notebook will:

Load and preprocess the point cloud (outlier removal, DTM construction, trunk-zone upsampling).

Plan a circular orbit around the plot with 2PTA pre‑flight deformation.

Execute the autonomous flight with real‑time SLAM, feature detection, and obstacle avoidance.

Record keyframes, depth maps, trajectory logs, and evaluation metrics.

Reconstruct a 3D point cloud from the keyframes (SfM).

Compute DRC and stem‑count for the plot.

All outputs (videos, keyframes, trajectory logs, evaluation figures) are saved in the uav_simulation_output/ folder.

📊 Example Results
On the full Zagros coppice point cloud, OBCS achieves:

Metric	Value
Orbit coverage	97.2%
Structural collisions	0
Height‑above‑terrain RMSE	0.045 m
RPE (1 m segments)	1.07 m
DRC estimation R²	0.92
Stem count exact match	82.9%
For detailed results, please refer to the paper (see Citation).

🖼️ Visualisation
Top‑down trajectory	Keyframe example	Feature detection
https://docs/images/trajectory.png	https://docs/images/keyframe.png	https://docs/images/features.png
More figures are generated automatically in uav_simulation_output/evaluation/.

📄 Citation
If you use OBCS in your research, please cite the following paper:

bibtex
@article{ghasemi2026obcs,
  title={OBCS: An Open-Source Simulator for Autonomous Below-Canopy UAV Inventory in Zagros Oak Coppice},
  author={Ghasemi, Marziye and Latifi, Hooman and Iranmanesh, Yaghoub},
  journal={},
  year={2026},
  note={Under review}
}
🤝 Contributing
Contributions are welcome! If you have suggestions, bug reports, or want to add new features:

Open an Issue to discuss the change.

Fork the repository and create a new branch.

Submit a Pull Request with a clear description of your changes.

Please ensure your code follows the existing style and passes the evaluation tests.

📜 License
This project is licensed under the MIT License – see the LICENSE file for details.

🙏 Acknowledgements
This work was supported by:

Department of Photogrammetry and Remote Sensing, Faculty of Geodesy and Geomatics Engineering, K. N. Toosi University of Technology, Tehran, Iran

School of Civil Engineering, Iran University of Science and Technology, Tehran, Iran

Iran National Science Foundation (INSF) under project No. 4028916.

The dataset was collected as part of the Zagros forest monitoring programme (Ghasemi et al., 2025).

📬 Contact
For questions or collaborations, please contact:

Marziye Ghasemi – mrzghasemi@iust.ac.ir


