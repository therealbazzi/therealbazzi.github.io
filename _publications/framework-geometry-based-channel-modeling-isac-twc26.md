---
title: "A Framework for Geometry-based Statistical Channel Modeling in ISAC Systems"
collection: publications
permalink: /publication/framework-geometry-based-channel-modeling-isac-twc26
excerpt: 'A comprehensive geometry-based statistical channel modeling (GBSM) framework for bistatic ISAC, decomposing channels into target and background environment multipath components with unified spatial consistency extending 3GPP TR 38.901.'
date: 2026-01-01
venue: 'IEEE Transactions on Wireless Communications'
volume: "25"
firstpage: "19773"
lastpage: "19790"
publisher: 'IEEE'
doi: "10.1109/TWC.2026.3703753"
arxiv_id: "2511.23201"
authors:
  - "Ali Waqar Azim"
  - "Ahmad Bazzi"
  - "Theodore S. Rappaport"
  - "Marwa Chafii"
paperurl: 'https://ieeexplore.ieee.org/document/11574587/'
keywords:
  - "Integrated Sensing and Communications"
  - "ISAC"
  - "Geometry-Based Statistical Channel Model"
  - "GBSM"
  - "Bistatic ISAC"
  - "3GPP TR 38.901"
  - "Dual-Component Channel"
  - "Spatial Consistency"
  - "Delay and Doppler Drift"
  - "Urban Macro"
  - "Urban Micro"
  - "Indoor Factory"
tldr: "Extends 3GPP TR 38.901 into a unified bistatic ISAC geometry-based statistical channel model, decoupling the channel into target-specific and background multipath components to preserve channel reciprocity, absolute delay alignment, and spatial consistency."
citation: 'A. Azim, <b>A. Bazzi</b>, T. S. Rappaport and M. Chafii, &quot;A Framework for Geometry-based Statistical Channel Modeling in ISAC Systems,&quot; in <i>IEEE Transactions on Wireless Communications</i>, vol. 25, pp. 19773-19790, 2026.'
---

## Key Highlights & Quantitative Findings
- **Dual-Component ISAC Channel Decomposition:** Separates the wireless channel into a target channel (governed by target RCS and scattering centers) and a background clutter channel (comprising non-target interacting propagation paths).
- **Extension of 3GPP TR 38.901:** Incorporates a hybrid clustering methodology combining spatiotemporally consistent deterministic clusters with stochastic clusters, preserving phase reciprocity and absolute delay alignment.
- **Full Standard Parity:** Validated across Urban Macro (UMa), Urban Micro (UMi), and Indoor Factory (InF) scenarios, proving communication parity (BER and channel capacity) while enabling precise radar sensing evaluation (ranging error and ROC curves).

## Abstract

This paper proposes a comprehensive framework for a geometry-based statistical model for integrated sensing and communication (ISAC) tailored for bistatic systems. Our dual-component model decomposes the ISAC channel into a target channel encompassing all multipath components produced by a sensing target parameterized by the target's radar cross-section and scattering points, and a background channel comprising all other propagation paths that do not interact with the sensing target. The framework extends TR38.901 via a hybrid clustering approach, integrating spatiotemporally consistent deterministic clusters with stochastic clusters to preserve channel reciprocity and absolute delay alignment for sensing parameter estimation. Extensive simulations across urban macro, urban micro, and indoor factory scenarios demonstrate that the model maintains communication performance parity with the standard TR38.901, validated through bit-error rate analysis obtained via simulated and measured ISAC channels and channel capacity assessment, while enabling sensing performance evaluation, such as target ranging error for localization and receiver operating characteristic curves for detection probability.
