# Safety-Constrained Distributed Control Inference for Multi-ASV Collision Avoidance

This repository hosts the numerical simulation results, high-fidelity Gazebo physical validation videos, and supplementary materials for the manuscript **"Safety-Constrained Distributed Control Inference for Multi-ASV Collision Avoidance"**.

> **📢 Note on Source Code:** 
> This repository currently provides visual demonstrations (numerical & Gazebo simulations), quantitative ablation metrics, and comparative figures for review purposes. **The full Python/ROS implementation will be made publicly available upon the acceptance of the paper.**

---

## 1. Visual Demonstrations

We validate the proposed **Safety-Constrained Distributed Factor Graph Inference (SC-DFGI)** framework across both high-fidelity 3D physical simulation environments (ROS / Gazebo) and numerical dynamic simulations[cite: 1].

### 1.1 High-Fidelity Gazebo Physical Validation
The video below demonstrates the real-time execution of our framework in a 3D Gazebo marine environment, accounting for realistic wave/hydrodynamic disturbances, physical hull geometries, and asynchronous distributed computation:

<!-- 👇 请直接用鼠标把你的 Gazebo验证.mp4 拖拽到下面这行空白处 👇 -->



### 1.2 Numerical Simulation & Ablation Animation
4 underactuated ASVs performing an antipodal swap in a workspace obstructed by static circular obstacles under exact 3-DOF nonlinear Fossen hydrodynamics[cite: 1]:

<!-- 👇 如果你的纯数值仿真也是 .mp4 或 .gif，直接用鼠标拖拽到下面这行空白处 👇 -->



---

## 2. Framework Overview

We propose a two-stage **Safety-Constrained Distributed Factor Graph Inference (SC-DFGI)** framework for multi-agent collision avoidance of underactuated Autonomous Surface Vehicles (ASVs)[cite: 1]:
- **Stage I (Distributed Factor Graph Variational Inference):** Infers nominal control beliefs via variational importance sampling and Gaussian moment matching over a local prediction horizon, integrating goal-tracking priors, 3-DOF nonlinear hydrodynamic transitions, static obstacle soft repulsion, and COLREGs-inspired inter-ASV interaction factors[cite: 1].
- **Stage II (Safety-Constrained MAP / Second-Order HOCBF-QP):** Enforces hard pairwise inter-ASV and obstacle collision avoidance constraints on a look-ahead point ($l = 0.50\text{ m}$, relative degree 2) via symmetric responsibility splitting and a shared fixed Gaussian metric[cite: 1].

---

## 3. Ablation Study & Quantitative Results

Three controller modes are evaluated under identical initial conditions, physical actuator saturation bounds ($\tau_u \in [-35, 50]\text{ N}$, $\tau_r \in [-18, 18]\text{ N}\cdot\text{m}$), and fixed safety sets ($d_{\text{safe, ASV}} = 1.25\text{ m}$, $d_{\text{safe, obs}} = 0.58\text{ m}$ surface clearance)[cite: 1]:
1. **`Nominal_Only`**: Distributed factor-graph variational inference (FG-VI) nominal control only (without Stage-II safety filtering)[cite: 1].
2. **`Goal_HOCBF`**: Bounded goal-directed control prior filtered directly by the second-order HOCBF-QP (without Stage-I cooperative inference)[cite: 1].
3. **`Full_Method`**: The proposed two-stage framework combining FG-VI nominal belief generation with the second-order HOCBF-QP safety filter[cite: 1].

### Comparative Trajectories & Safety Profiles
<!-- 👇 你也可以直接把生成的 baseline_seed42.png 静态对比图拖拽到下面这行空白处 👇 -->



---

## 4. Benchmark Scenarios

The numerical benchmark evaluates the 4-ASV system across multiple random seeds (`[0, 7, 21, 42, 84]`) and geometric configurations[cite: 1]:
- **`baseline`**: Circle radius $R = 7.5\text{ m}$, initial surge speed $0.8\text{ m/s}$[cite: 1].
- **`compact_5` / `compact_4`**: Compact initial radii ($R = 5.0\text{ m}$ and $4.0\text{ m}$) with higher initial surge speed ($1.25\text{ m/s}$)[cite: 1].
- **`oblique_5` / `oblique_4`**: Asymmetric initial angular skew ($0.35\text{ rad}$)[cite: 1].
- **`fast_5`**: High-speed scenario ($R = 5.0\text{ m}$, initial speed $1.6\text{ m/s}$) with vertically aligned initial positions for ASV 2 & 4[cite: 1].
- **`wide_obstacles`**: Scaled static obstacle positions ($1.3\times$)[cite: 1].

---

## 5. Release Plan

- [x] Upload numerical simulation and high-fidelity Gazebo validation videos.
- [x] Upload multi-scenario ablation figures (`.png`) and quantitative metric logs (`.json`)[cite: 1].
- [ ] Release full Python simulation engine (`GC01_TwoStage_HardMAP.py`) and ROS/Gazebo packages *(upon paper acceptance)*[cite: 1].

## License

This project is licensed under the MIT License.
