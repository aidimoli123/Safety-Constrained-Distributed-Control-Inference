# Safety-Constrained-Distributed-Control-Inference
Simulation results and supplementary materials for the paper "Safety-Constrained Distributed Control Inference for Multi-ASV Collision Avoidance" (Source code to be released upon acceptance).
# Safety-Constrained Distributed Control Inference for Multi-ASV Collision Avoidance

This repository hosts the simulation results, ablation study data, and supplementary materials for the manuscript **"Safety-Constrained Distributed Control Inference for Multi-ASV Collision Avoidance"**.

> **📢 Note on Source Code:** 
> This repository currently provides the complete simulation results, quantitative evaluation metrics, and comparative figures for review purposes. **The full Python implementation (`GC01_TwoStage_HardMAP.py`) will be made publicly available upon the acceptance of the paper.**

---

## 1. Framework Overview

We propose a two-stage **Safety-Constrained Distributed Factor Graph Inference (SC-DFGI)** framework for multi-agent collision avoidance of underactuated Autonomous Surface Vehicles (ASVs):
- **Stage I (Distributed Factor Graph Variational Inference):** Infers nominal control beliefs via variational importance sampling and Gaussian moment matching over a local prediction horizon, integrating goal-tracking priors, 3-DOF nonlinear hydrodynamic transitions (Fossen model), static obstacle soft repulsion, and COLREGs-inspired inter-ASV interaction factors.
- **Stage II (Safety-Constrained MAP / Second-Order HOCBF-QP):** Enforces hard pairwise inter-ASV and obstacle collision avoidance constraints on a look-ahead point ($l = 0.50\text{ m}$, relative degree 2) via symmetric responsibility splitting and a shared fixed Gaussian metric.

---

## 2. Ablation Study & Controller Modes

Three controller modes are evaluated under identical initial conditions, physical actuator saturation bounds ($\tau_u \in [-35, 50]\text{ N}$, $\tau_r \in [-18, 18]\text{ N}\cdot\text{m}$), and fixed safety sets ($d_{\text{safe, ASV}} = 1.25\text{ m}$, $d_{\text{safe, obs}} = 0.58\text{ m}$ surface clearance):
1. **`Nominal_Only`**: Distributed factor-graph variational inference (FG-VI) nominal control only (without Stage-II safety filtering).
2. **`Goal_HOCBF`**: Bounded goal-directed control prior filtered directly by the second-order HOCBF-QP (without Stage-I cooperative inference).
3. **`Full_Method`**: The proposed two-stage framework combining FG-VI nominal belief generation with the second-order HOCBF-QP safety filter.

---

## 3. Benchmark Scenarios & Simulation Results

The benchmark evaluates a 4-ASV antipodal swap task obstructed by central static circular obstacles across multiple random seeds (`[0, 7, 21, 42, 84]`) and geometric configurations:
- **`baseline`**: Circle radius $R = 7.5\text{ m}$, initial surge speed $0.8\text{ m/s}$.
- **`compact_5` / `compact_4`**: Compact initial radii ($R = 5.0\text{ m}$ and $4.0\text{ m}$) with higher initial surge speed ($1.25\text{ m/s}$).
- **`oblique_5` / `oblique_4`**: Asymmetric initial angular skew ($0.35\text{ rad}$).
- **`fast_5`**: High-speed scenario ($R = 5.0\text{ m}$, initial speed $1.6\text{ m/s}$) with vertically aligned initial positions for ASV 2 & 4.
- **`wide_obstacles`**: Scaled static obstacle positions ($1.3\times$).

### Included Result Files
- **`<scenario>_seed<seed>.png`**: 3x3 comparative figures illustrating 2D trajectories, sampled inter-ASV distances, obstacle-center distances, surge speeds, surge forces ($\tau_u$), yaw moments ($\tau_r$), and cumulative speed deficits.
- **`<scenario>_results.json`**: Complete quantitative metrics across all seeds, including task completion status, arrival times, minimum inter-ASV and obstacle clearances, QP feasibility diagnostics, and control intervention norms.
- **`<scenario>_<mode>_<seed>.npz`** *(if uploaded)*: Compressed NumPy archives containing raw state trajectories and control histories.

---

## 4. Release Plan

- [x] Upload multi-scenario ablation figures (`.png`) and quantitative metric logs (`.json`).
- [ ] Release full Python simulation engine (`GC01_TwoStage_HardMAP.py`) and reproduction scripts *(upon paper acceptance)*.

## License

This project is licensed under the MIT License.
