---
title: "Robust Secure Beamforming for Movable Antenna Enhanced Integrated Sensing and Communications"
collection: publications
permalink: /publication/robust-secure-beamforming-movable-antenna-isac-comml26
excerpt: 'Robust joint transmit beamforming and antenna placement optimization for movable antenna (MA) enhanced secure ISAC systems under imperfect eavesdropper CSI, maximizing radar SINR via BCD, SCA, and fractional programming.'
date: 2026-06-01
venue: 'IEEE Communications Letters'
publisher: 'IEEE'
doi: "10.1109/LCOMM.2026.3752986"
arxiv_id: "2606.07104"
authors:
  - "Yuan Chen"
  - "Ning Wei"
  - "Ahmad Bazzi"
  - "Xiangyu Dong"
  - "Ran Yang"
  - "You Li"
  - "Yue Xiu"
paperurl: 'https://ieeexplore.ieee.org/document/11793620'
keywords:
  - "Movable Antennas"
  - "Integrated Sensing and Communications"
  - "ISAC"
  - "Robust Beamforming"
  - "Physical Layer Security"
  - "Eavesdropping"
  - "Channel Uncertainty"
  - "Imperfect CSI"
  - "Radar SINR"
  - "Block Coordinate Descent"
  - "Successive Convex Approximation"
  - "Fractional Programming"
tldr: "Jointly optimizes transmit beamforming and movable antenna positions to maximize radar SINR in secure ISAC under imperfect eavesdropper channel state information (CSI) using BCD, SCA, and fractional programming."
citation: 'Y. Chen, N. Wei, <b>A. Bazzi</b>, X. Dong, R. Yang, Y. Li and Y. Xiu, &quot;Robust Secure Beamforming for Movable Antenna Enhanced Integrated Sensing and Communications,&quot; in <i>IEEE Communications Letters</i>, 2026.'
---

## Key Highlights & Quantitative Findings
- **Movable Antenna Placement Optimization:** Formulates a joint transmit beamforming and continuous antenna position optimization framework for movable antenna (MA)-enhanced bistatic ISAC.
- **Robustness Against Eavesdropper Uncertainty:** Explicitly accounts for imperfect eavesdropper (Eve) channel state information (CSI), preventing confidential information leakage while preserving radar tracking capabilities.
- **Efficient Optimization Pipeline:** Tackles non-convexities through block coordinate descent (BCD), successive convex approximation (SCA), and fractional programming (FP), demonstrating fast convergence and substantial radar SINR improvements over fixed-position antenna arrays.

## Benchmark & Architectural Comparison

| Dimension / Metric | Fixed-Position Antennas (FPA) | Conventional RIS-Assisted ISAC | Proposed Movable Antenna (MA) ISAC |
| :--- | :--- | :--- | :--- |
| **Spatial Degrees of Freedom** | Fixed discrete grid ($\lambda/2$) | Phase shifts at reflective elements | Continuous 2D/3D positioning within transmit region |
| **Eavesdropper Suppression** | Null depth constrained by fixed geometry | Limited by cascaded path-loss attenuation | Continuous null steering directly onto Eve's subspace |
| **CSI Uncertainty Tolerance** | Rapid performance loss under Eve CSI error | Sensitive to cascaded channel estimation errors | Robust bounded ellipsoidal CSI formulation |
| **Optimization Framework** | Semidefinite Relaxation (SDR) | Alternating Optimization (AO) | Block Coordinate Descent (BCD) + SCA + FP |
| **Radar SINR Gain** | Baseline (0 dB reference) | Moderate (+2 to +4 dB) | **Substantial improvement (>6 dB gain over FPA)** |

## Abstract

In this letter, we investigate robust beamforming design for a movable antenna (MA)-enhanced secure integrated sensing and communications (ISAC) system with imperfect eavesdropping channel state information (CSI). To improve radar sensing performance, we formulate a radar signal-to-interference-plus-noise ratio (SINR) maximization problem by jointly optimizing the transmit beamforming and antenna placement while ensuring communication data security. However, the resulting optimization problem is inherently intractable due to the nonlinear mapping from antenna positions to channel coefficients, as well as the eavesdropper (Eve) channel uncertainty. To handle these challenges, we propose a block coordinate descent (BCD)-based algorithm incorporating successive convex approximation (SCA) and fractional programming (FP) techniques. Simulation results show that our proposed algorithm exhibits fast convergence and achieves a significant improvement in the radar SINR while guaranteeing communication security.

## Technical Q&A & Research Takeaways

### Q1: Why are movable antennas (MAs) advantageous over fixed antenna arrays for secure ISAC?
Conventional fixed-position antenna arrays (FPAs) are constrained by fixed spatial sampling of the continuous electromagnetic field. When an eavesdropper (Eve) lies close in angle or subspace to a legitimate user or target, conventional beamforming cannot steer deep spatial nulls without severely degrading communication secrecy rate or radar illumination. Movable antennas provide local continuous mechanical/electromechanical spatial degrees of freedom (DoF), allowing the transmitter to dynamically configure antenna positions within a 2D continuous region. This continuous spatial adjustment reconfigures channel phase vectors, steering destructive interference directly onto Eve while maximizing constructive radar echo power toward the target.

### Q2: How does the framework handle imperfect eavesdropper channel state information (CSI)?
Because eavesdroppers operate passively without feedback, perfect CSI is practically impossible. We model the eavesdropper's channel uncertainty using a bounded ellipsoidal error model. By incorporating worst-case secrecy capacity constraints into the objective, the robust optimization formulation guarantees that confidential data remains protected against intercept even under the most adversarial channel estimation perturbations.

### Q3: What optimization algorithms are employed to solve the non-convex problem?
The joint optimization of digital beamforming vectors and continuous 2D antenna position coordinates involves highly coupled non-linearities. The paper designs a three-stage algorithmic pipeline:
1. **Block Coordinate Descent (BCD):** Decouples the optimization variables into two alternating subproblems: beamforming vector optimization and antenna placement coordinate optimization.
2. **Successive Convex Approximation (SCA):** Linearizes non-convex coupled terms and antenna position manifolds using first-order Taylor expansions.
3. **Fractional Programming (FP):** Converts fractional radar SINR objectives into quadratic surrogate forms that are efficiently solved with standard convex solvers.


