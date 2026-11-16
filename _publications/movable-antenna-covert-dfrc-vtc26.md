---
title: "Movable Antenna Enhanced Covert Dual-Functional Radar-Communication: Joint Beamforming and Antenna Position Optimization"
collection: publications
permalink: /publication/movable-antenna-covert-dfrc-vtc26
excerpt: 'Joint optimization of transmit beamforming vectors, receive filter, and antenna positions for movable antenna (MA) enhanced covert DFRC systems to maximize covert communication rate under radar SNR and covertness constraints.'
date: 2026-09-01
venue: '2026 IEEE 104th Vehicular Technology Conference (VTC2026-Fall)'
publisher: 'IEEE'
doi: "10.1109/VTC2026-Fall68024.2026.11758262"
arxiv_id: "2510.09949"
authors:
  - "Ran Yang"
  - "Zheng Dong"
  - "Lin Zhang"
  - "Wanting Lyu"
  - "Yue Xiu"
  - "Ning Wei"
  - "Ahmad Bazzi"
  - "Chadi Assi"
paperurl: 'https://ieeexplore.ieee.org/document/11758262'
keywords:
  - "Movable Antennas"
  - "Dual-Functional Radar-Communication"
  - "DFRC"
  - "Covert Communication"
  - "Low Probability of Detection"
  - "Joint Beamforming"
  - "Antenna Position Optimization"
  - "Lagrangian Dual Transformation"
  - "Block Coordinate Descent"
  - "Semidefinite Relaxation"
tldr: "Investigates movable antenna (MA)-enhanced covert dual-functional radar-communication (DFRC) to evade detection by an adversary warden while maximizing covert transmission rate subject to radar SNR constraints via BCD, SDR, and SCA."
citation: 'R. Yang, Z. Dong, L. Zhang, W. Lyu, Y. Xiu, N. Wei, <b>A. Bazzi</b> and C. Assi, &quot;Movable Antenna Enhanced Covert Dual-Functional Radar-Communication: Joint Beamforming and Antenna Position Optimization,&quot; in <i>2026 IEEE 104th Vehicular Technology Conference (VTC2026-Fall)</i>, Boston, MA, USA, 2026, pp. 1-7.'
---

## Key Highlights & Quantitative Findings
- **Covert DFRC with Movable Antennas:** Harnesses the spatial reconfigurability of movable antennas (MAs) to prevent transmission detection by an observant warden (adversary) while sustaining high-performance radar surveillance.
- **Joint Transceiver & Geometry Optimization:** Optimizes transmit beamforming vectors, receive filter coefficients, and continuous antenna placements simultaneously.
- **Optimization Strategy:** Employs Lagrangian dual transformation followed by block coordinate descent (BCD), integrating semidefinite relaxation (SDR), projected gradient descent (PGD), and successive convex approximation (SCA).
- **Substantial Covert Sum-Rate Gains:** Demonstrates significant throughput gains over conventional fixed-position antenna (FPA) arrays while satisfying strict covertness probabilities and radar SNR thresholds.

## Abstract

Movable antenna (MA) has emerged as a promising technology to flexibly reconfigure wireless channels by adjusting antenna placement. In this paper, we study a secured dual-functional radar-communication (DFRC) system enhanced by movable antennas. To ensure communication security, we aim to maximize the achievable sum rate by jointly optimizing the transmit beamforming vectors, receiving filter, and antenna placement, subject to radar signal-to-noise ratio (SNR) and transmission covertness constraints. To tackle this challenging optimization problem, we first employ a Lagrangian dual transformation process to reformulate it into a more tractable form. Subsequently, the problem is solved by employing a block coordinate descent (BCD) procedure, incorporating semidefinite relaxation (SDR), projected gradient descent (PGD), and successive convex approximation (SCA) techniques. Simulation results demonstrate that the proposed method can significantly improve the covert sum rate, and achieve a satisfactory balance between the communication and radar performance compared with existing benchmark schemes by leveraging the flexibility of movable antennas.
