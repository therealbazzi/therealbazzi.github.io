---
title: "Deep Learning for High-Resolution Sensing Parameter Estimation in Bistatic ISAC"
collection: publications
permalink: /publication/deep-learning-high-resolution-sensing-bistatic-isac-icmlcn26
excerpt: 'A deep learning framework for high-resolution sensing parameter estimation in bistatic ISAC, achieving near-optimal angle and delay estimation accuracy with drastic latency reductions compared to iterative algorithms.'
date: 2026-05-01
venue: 'IEEE International Conference on Machine Learning for Communication and Networking (ICMLCN)'
publisher: 'IEEE'
authors:
  - "Salmane Naoumi"
  - "Kevin Mutuwira"
  - "Roberto Bomfin"
  - "Ahmad Bazzi"
  - "Marwa Chafii"
keywords:
  - "Deep Learning"
  - "Integrated Sensing and Communications"
  - "ISAC"
  - "Bistatic ISAC"
  - "High-Resolution Estimation"
  - "Parameter Estimation"
  - "Channel State Information"
  - "CSI"
  - "Angle of Arrival"
  - "AoA"
  - "Angle of Departure"
  - "AoD"
  - "Time of Arrival"
  - "Cramér-Rao Lower Bound"
tldr: "Develops deep learning architectures for high-resolution sensing parameter estimation (AoA, AoD, delay) in bistatic ISAC systems using communication CSI, achieving near-CRLB performance with orders-of-magnitude reduction in execution latency."
citation: 'S. Naoumi, K. Mutuwira, R. Bomfin, <b>A. Bazzi</b>, and M. Chafii, &quot;Deep Learning for High-Resolution Sensing Parameter Estimation in Bistatic ISAC,&quot; accepted to <i>IEEE International Conference on Machine Learning for Communication and Networking (ICMLCN)</i>, 2026.'
---

## Key Highlights & Quantitative Findings
- **Real-Time Bistatic Sensing:** Bypasses computationally expensive iterative parameter-scanning algorithms (such as 2D-MUSIC or maximum likelihood) by mapping communication channel state information (CSI) directly to target parameters using deep learning.
- **Joint Super-Resolution Estimation:** Estimates Angle of Arrival (AoA), Angle of Departure (AoD), and Time of Arrival (ToA) simultaneously with resolution exceeding the Fourier limit.
- **Near-Optimal Estimation Accuracy:** Numerical simulations show estimation variance approaching the theoretical Cramér-Rao Lower Bound (CRLB) even in low-to-moderate SNR regimes, with orders-of-magnitude faster online inference suitable for real-time 6G networks.

## Abstract

Bistatic integrated sensing and communication (ISAC) offers substantial coverage and interference advantages over monostatic architectures by physically separating the transmitter and receiver. However, extracting high-resolution sensing parameters—such as angle of arrival (AoA), angle of departure (AoD), and propagation delay—from communication-centric reference symbols presents severe computational challenges under low signal-to-noise ratio (SNR) conditions and real-time latency constraints. In this paper, we propose a deep learning framework for high-resolution sensing parameter estimation in bistatic ISAC systems. By processing complex-valued channel state information (CSI) acquired from standard communication waveforms, our neural network architecture learns the underlying spatial-temporal multipath representations, bypassing the computational bottleneck of high-resolution parametric scanning methods (e.g., 2D-MUSIC or maximum likelihood). Extensive numerical simulations demonstrate that the proposed deep learning approach achieves super-resolution parameter estimation accuracy approaching theoretical Cramér-Rao lower bounds (CRLB) with orders-of-magnitude reduction in online execution time, enabling real-time sensing in 6G bistatic networks.
