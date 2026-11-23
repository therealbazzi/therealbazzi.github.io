---
title: "Compressed Multiband Sensing in FR3 Using Alternating Direction Method of Multipliers"
collection: publications
permalink: /publication/compressed-multiband-sensing-fr3-admm-wcnc26
excerpt: 'An ADMM-assisted compressed multiband sensing (ADMM-CMS) framework in FR3 (7–24 GHz) that efficiently resolves angular ambiguities from grating lobes across disparate sub-bands, yielding 34 dB transmit power gain and over 34% delay RMSE reduction.'
date: 2026-04-01
venue: 'IEEE Wireless Communications and Networking Conference (WCNC)'
publisher: 'IEEE'
arxiv_id: "2510.03055"
authors:
  - "Dexin Wang"
  - "Isha Jariwala"
  - "Ahmad Bazzi"
  - "Sundeep Rangan"
  - "Theodore S. Rappaport"
  - "Marwa Chafii"
paperurl: 'https://arxiv.org/pdf/2510.03055'
keywords:
  - "Compressed Sensing"
  - "Multi-Band Sensing"
  - "Frequency Range 3"
  - "FR3"
  - "Alternating Direction Method of Multipliers"
  - "ADMM"
  - "Integrated Sensing and Communication"
  - "ISAC"
  - "Grating Lobes"
  - "Upper Mid-Band 6G"
  - "Pilot Symbols"
tldr: "Introduces ADMM-assisted compressed multiband sensing (ADMM-CMS) in FR3 (7–24 GHz) using QAM pilot symbols, achieving a 34 dB gain in per-antenna transmit power and over 34% reduction in delay RMSE over single-band compressed sensing."
citation: 'D. Wang, I. Jariwala, <b>A. Bazzi</b>, S. Rangan, T. S. Rappaport, and M. Chafii, &quot;Compressed Multiband Sensing in FR3 Using Alternating Direction Method of Multipliers,&quot; accepted by <i>IEEE Wireless Communications and Networking Conference (WCNC)</i>, Kuala Lumpur, Malaysia, Apr. 2026, pp. 1–6.'
---

## Key Highlights & Quantitative Findings
- **Overcoming Grating Lobes in FR3:** Solves the critical angular ambiguity challenge arising from disparate non-contiguous sub-bands in Frequency Range 3 (FR3, 7–24 GHz) using compressed sensing with standard uplink QAM pilots.
- **Adaptive ADMM Optimization:** Develops an adaptive ADMM algorithm that dynamically balances dual ascent with augmented Lagrangian stabilization, automatically halting upon convergence.
- **34 dB Transmit Power Gain:** Achieves a **34 dB gain** in per-antenna transmit power compared to Bartlett-type beamforming for achieving a 0.9 successful recovery probability (SRP).
- **Substantial Delay Estimation Improvement:** Achieves **34.46%** and **40.76%** reductions in delay root mean squared error (RMSE) compared to separate compressed sensing on constituent 7 GHz and 10 GHz sub-bands at -41 dBm per-antenna power.

## Abstract

Joint detection and localization of users and scatterers in multipath-rich channels on multiple bands is critical for integrated sensing and communication (ISAC) in 6G. Existing multiband sensing methods are limited by classical beamforming or computationally expensive approaches. This paper introduces alternating direction method of multipliers (ADMM)-assisted compressed multiband sensing (CMS), hereafter referred to as ADMM-CMS, which is a novel framework for multiband sensing using uplink quadrature amplitude modulation-modulated pilot symbols. To solve the CMS problem, we develop an adaptive ADMM algorithm that adjusts to noise and ensures automatic stopping if converged. ADMM combines the decomposability of dual ascent with the robustness of augmented Lagrangian methods, making it suitable for large-scale structured optimization. Simulations show that ADMM-CMS achieves higher spatial resolution and improved denoising compared to Bartlett-type beamforming, yielding a 34 dB gain in per-antenna transmit power for achieving a 0.9 successful recovery probability (SRP). Moreover, compared to performing compressed sensing separately on the constituent 7 GHz and 10 GHz sub-bands, ADMM-CMS achieves reductions in delay root mean squared error of 34.46% and 40.76%, respectively, at -41 dBm per-antenna transmit power, while also yielding improved SRP. Our findings demonstrate ADMM-CMS as an efficient enabler of ISAC in frequency range 3 (FR3, 7-24 GHz) for 6G systems.

## Technical Q&A & Research Takeaways

### Q1: What makes ADMM uniquely suitable for compressed multi-band sensing?
Compressed sensing across multiple disparate frequency bands results in massive, highly structured dictionary matrices. Solving such large-scale convex l1-minimization problems via interior-point methods is computationally prohibitive. ADMM (Alternating Direction Method of Multipliers) decomposes the large joint optimization problem into small, parallel subproblems with closed-form proximal updates (soft-thresholding) and augmented Lagrangian stabilization, enabling fast convergence and scalable implementation on modern DSP hardware.

### Q2: How does standard uplink QAM pilot modulation enable sensing without dedicated radar waveforms?
In typical ISAC deployments, dedicated sensing waveforms consume precious spectrum and power. ADMM-CMS leverages standard communication uplink pilot symbols (such as QAM pilots used for channel estimation). By formulating channel estimation and target detection into a unified sparse recovery framework, the receiver extracts high-resolution delay and angle information directly from the communication frames without altering the communication standard.

### Q3: What is the primary quantitative advantage over Bartlett beamforming?
Classical Bartlett beamforming suffers from high sidelobes and severe performance degradation under low SNR. ADMM-CMS achieves a remarkable **34 dB gain** in per-antenna transmit power required to reach a 0.9 successful recovery probability (SRP), alongside >34% reductions in delay root-mean-squared error compared to single-band compressed sensing.


