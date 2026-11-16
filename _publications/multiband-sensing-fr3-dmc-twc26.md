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

## Abstract

Multi-band sensing has emerged as a key enabler of integrated sensing and communication (ISAC), one of the six primary usage scenarios defined for IMT-2030 (6G). The introduction of frequency range 3 (FR3, 7-24 GHz), comprising non-contiguous sub-bands across a wide frequency span, further reinforces the importance of multi-band operation. In such scenarios, frequency-dependent propagation effects that are collectively referred to as dense multipath components (DMC), including clutter, diffraction, and diffuse scattering, must be carefully considered. Building on prior literature and our experimental observations, this paper proposes a novel ISAC channel analysis tailored to multi-band sensing, based on a channel model with background DMCs. It also assesses the sensing trade-offs among sub-bands by analyzing Cramér-Rao bound (CRB)-based fundamental limits. Furthermore, a scalable multi-band estimator is proposed that resolves angular ambiguities arising from the grating lobes effect. Simulation results of the multi-band estimator demonstrate substantial gains in estimation accuracy and reductions in false alarm rate over single-band estimators operating on each constituent sub-band within the CRB-achieving regime. In a representative test case, the proposed estimator achieves reductions of 37.41% and 17.04% in the root mean squared error of delay estimation compared to single-band estimators operating at 8.75 GHz and 21.7 GHz, respectively.
