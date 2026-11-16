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

## Abstract

In this letter, we investigate robust beamforming design for a movable antenna (MA)-enhanced secure integrated sensing and communications (ISAC) system with imperfect eavesdropping channel state information (CSI). To improve radar sensing performance, we formulate a radar signal-to-interference-plus-noise ratio (SINR) maximization problem by jointly optimizing the transmit beamforming and antenna placement while ensuring communication data security. However, the resulting optimization problem is inherently intractable due to the nonlinear mapping from antenna positions to channel coefficients, as well as the eavesdropper (Eve) channel uncertainty. To handle these challenges, we propose a block coordinate descent (BCD)-based algorithm incorporating successive convex approximation (SCA) and fractional programming (FP) techniques. Simulation results show that our proposed algorithm exhibits fast convergence and achieves a significant improvement in the radar SINR while guaranteeing communication security.
