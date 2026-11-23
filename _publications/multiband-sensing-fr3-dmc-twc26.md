---
title: "Multi-Band Sensing in FR3 with Background Dense Multipath Components"
collection: publications
permalink: /publication/multiband-sensing-fr3-dmc-twc26
excerpt: 'A novel ISAC channel analysis tailored to multi-band sensing in FR3 (7–24 GHz) with background dense multipath components (DMC), establishing fundamental CRB limits and a scalable estimator that resolves grating lobes with up to 37.4% delay RMSE reduction.'
date: 2026-02-01
venue: 'IEEE Transactions on Wireless Communications'
publisher: 'IEEE'
doi: "10.1109/TWC.2026.3754549"
arxiv_id: "2602.23539"
authors:
  - "Dexin Wang"
  - "Roberto Bomfin"
  - "Ahmad Bazzi"
  - "Marwa Chafii"
paperurl: 'https://arxiv.org/pdf/2602.23539'
keywords:
  - "Integrated Sensing and Communication"
  - "ISAC"
  - "Frequency Range 3"
  - "FR3"
  - "Dense Multipath Components"
  - "DMC"
  - "Multi-Band Sensing"
  - "Grating Lobes"
  - "Cramér-Rao Bound"
  - "CRB"
  - "Delay Estimation"
  - "6G Upper Mid-Band"
tldr: "Proposes a novel ISAC channel model and scalable multi-band estimator tailored for FR3 (7–24 GHz) that resolves grating-lobe angular ambiguities in the presence of background dense multipath components, achieving up to 37.4% delay estimation RMSE reduction."
citation: 'D. Wang, R. Bomfin, <b>A. Bazzi</b> and M. Chafii, &quot;Multi-Band Sensing in FR3 with Background Dense Multipath Components,&quot; in <i>IEEE Transactions on Wireless Communications</i>, 2026.'
---

## Key Highlights & Quantitative Findings
- **Grating Lobe Ambiguity Resolution:** Introduces a scalable multi-band estimator that resolves severe angular ambiguities caused by grating lobes across non-contiguous sub-bands in FR3 (7–24 GHz).
- **Substantial Accuracy Gains:** In representative test cases, the proposed estimator achieves **37.41%** and **17.04%** reductions in the root mean squared error (RMSE) of delay estimation compared to single-band estimators operating at 8.75 GHz and 21.7 GHz, respectively.
- **Dense Multipath Components (DMC) Modeling:** Formulates fundamental sensing trade-offs via Cramér-Rao lower bounds (CRB) under background clutter, diffraction, and diffuse scattering.

## Performance Benchmark & Quantitative Comparison

| Estimator Scheme | Operational Bandwidth | Grating Lobe Robustness | DMC / Clutter Modeling | Delay Estimation RMSE Reduction |
| :--- | :--- | :--- | :--- | :--- |
| **Single-Band Baseline (8.75 GHz)** | Contiguous narrow-band | Immune to cross-band grating lobes | Ignored (Specular only) | Baseline (0% reference) |
| **Single-Band Baseline (21.7 GHz)** | Contiguous narrow-band | High path loss; specular only | Ignored (AWGN only) | Higher delay variance |
| **Independent Multi-Band Fusion** | Disparate sub-bands | Severe false peaks from grating lobes | Unmodeled diffuse scattering | High false alarm rate |
| **Proposed Scalable Multi-Band Estimator** | **Disparate FR3 sub-bands (7–24 GHz)** | **Fully resolves periodic ambiguities** | **Rigorous spatio-temporal DMC model** | **37.41% RMSE reduction (vs 8.75 GHz)<br>17.04% RMSE reduction (vs 21.7 GHz)** |

## Abstract

Multi-band sensing has emerged as a key enabler of integrated sensing and communication (ISAC), one of the six primary usage scenarios defined for IMT-2030 (6G). The introduction of frequency range 3 (FR3, 7-24 GHz), comprising non-contiguous sub-bands across a wide frequency span, further reinforces the importance of multi-band operation. In such scenarios, frequency-dependent propagation effects that are collectively referred to as dense multipath components (DMC), including clutter, diffraction, and diffuse scattering, must be carefully considered. Building on prior literature and our experimental observations, this paper proposes a novel ISAC channel analysis tailored to multi-band sensing, based on a channel model with background DMCs. It also assesses the sensing trade-offs among sub-bands by analyzing Cramér-Rao bound (CRB)-based fundamental limits. Furthermore, a scalable multi-band estimator is proposed that resolves angular ambiguities arising from the grating lobes effect. Simulation results of the multi-band estimator demonstrate substantial gains in estimation accuracy and reductions in false alarm rate over single-band estimators operating on each constituent sub-band within the CRB-achieving regime. In a representative test case, the proposed estimator achieves reductions of 37.41% and 17.04% in the root mean squared error of delay estimation compared to single-band estimators operating at 8.75 GHz and 21.7 GHz, respectively.

## Technical Q&A & Research Takeaways

### Q1: What is Frequency Range 3 (FR3) and why is multi-band sensing necessary in 6G?
Frequency Range 3 (FR3, 7–24 GHz), often called the upper mid-band or "golden band" for 6G, offers a compromise between the wide coverage of sub-6 GHz and the high bandwidth of millimeter-wave (mmWave). However, spectrum allocations in FR3 are non-contiguous. To achieve high range and delay resolution, an ISAC system must coherently or jointly process multiple disparate sub-bands simultaneously rather than operating in isolation.

### Q2: Why do grating lobes occur in multi-band sensing and how are they eliminated?
When aggregating non-contiguous frequency bands across an array, the wide spectral gap between carriers acts similarly to spatial undersampling, giving rise to severe periodic ambiguities (grating lobes) in the delay-angle ambiguity function. These grating lobes cause false alarms and peak ambiguity. The proposed scalable multi-band estimator resolves these ambiguities by leveraging cross-band phase coherence and joint multi-dimensional search, suppressing sidelobes and ensuring unambiguous target localization.

### Q3: How do Dense Multipath Components (DMC) affect Cramér-Rao Lower Bounds (CRB)?
Conventional channel models only account for specular paths (specular multipath components, SMC). In realistic indoor and complex outdoor propagation, a significant fraction of received energy stems from diffuse scattering, rough surfaces, and unresolvable clutter—collectively termed Dense Multipath Components (DMC). By modeling DMC as a colored spatio-temporal Gaussian process, our derivation of the Cramér-Rao bound establishes the fundamental physical estimation limits under realistic background noise and diffuse clutter.


