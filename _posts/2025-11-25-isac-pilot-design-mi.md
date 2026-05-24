---
layout: single
title: "Mutual Information: A Unifying Metric for Pilot Design in Integrated Sensing and Communication (ISAC)"
date: 2025-11-25
permalink: /posts/2024/07/isac-pilot-design-mi/
author_profile: true
read_time: true
share: true
tags:
  - ISAC
  - 6G
  - Mutual Information
  - Pilot Design
  - Stiefel Manifold
  - Optimization
description: "How we used mutual information as a unifying currency — bits — to design orthogonal pilot signals that simultaneously serve channel estimation for multi-user communication and target detection for radar sensing in ISAC systems. A walkthrough of our IEEE Transactions on Communications paper."
---

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Article",
  "@id": "{{ site.url }}{{ site.baseurl }}{{ page.permalink }}#article",
  "headline": {{ page.title | jsonify }},
  "datePublished": "{{ page.date | date_to_xmlschema }}",
  "dateModified": "{{ page.date | date_to_xmlschema }}",
  "inLanguage": "en",
  "isAccessibleForFree": true,
  "url": "{{ site.url }}{{ site.baseurl }}{{ page.permalink }}",
  "author": { "@id": "{{ site.url }}{{ site.baseurl }}/#person" },
  "publisher": { "@id": "{{ site.url }}{{ site.baseurl }}/#person" },
  "description": {{ page.description | jsonify }},
  "about": {
    "@type": "ScholarlyArticle",
    "@id": "{{ site.url }}{{ site.baseurl }}/publication/mutual-information-pilot-design-isac-tcom25",
    "headline": "Mutual Information Based Pilot Design for ISAC",
    "url": "{{ site.url }}{{ site.baseurl }}/publication/mutual-information-pilot-design-isac-tcom25",
    "sameAs": "https://doi.org/10.1109/TCOMM.2025.3545658",
    "author": [
      { "@type": "Person", "name": "Ahmad Bazzi", "sameAs": "https://orcid.org/0000-0002-7645-352X" },
      { "@type": "Person", "name": "Marwa Chafii" }
    ],
    "isPartOf": { "@type": "Periodical", "name": "IEEE Transactions on Communications" }
  },
  "keywords": "ISAC, integrated sensing and communication, pilot design, mutual information, Stiefel manifold, projected gradient descent, channel estimation, target detection, 6G",
  "mainEntityOfPage": "{{ site.url }}{{ site.baseurl }}{{ page.permalink }}"
}
</script>

> A walkthrough of our paper *"Mutual Information Based Pilot Design for ISAC"*, recently accepted at *IEEE Transactions on Communications* ([DOI: 10.1109/TCOMM.2025.3545658](https://doi.org/10.1109/TCOMM.2025.3545658), [arXiv preprint](https://arxiv.org/pdf/2306.13003)). Full structured citation, BibTeX, and metadata are on the [paper page](/publication/mutual-information-pilot-design-isac-tcom25/).

## The dual problem ISAC has always had

In an Integrated Sensing and Communication (ISAC) system, one antenna array does two jobs: it talks to communication users *and* listens for targets. That sounds elegant. In practice it's a design headache, because the *signals* the system sends out are being asked to serve two very different purposes simultaneously:

- For **communication**, the pilot symbols \\(\boldsymbol{\Phi}\\) at the start of a frame let downlink users estimate the channel \\(\boldsymbol{h}_k\\) so they can equalize and decode the data that follows.
- For **sensing**, the *same* pilots reflect off targets and clutter, and the ISAC base station listens to the backscatter to detect what's out there.

These two tasks pull in opposite directions. A pilot that minimizes channel-estimation variance for \\(K\\) users is not generally the same pilot that maximizes detection probability against a target at angle \\(\theta_0\\) surrounded by clutter at angles \\(\theta_1, \ldots, \theta_Q\\). Conventional wisdom said you had to pick one or build separate signals for each — wasting either time, spectrum, or hardware.

We wanted a principled way to *jointly* design that pilot. The catch: the two performance measures usually live in different units. Detection performance is a probability; channel estimation is measured in mean-squared error or capacity. How do you compare them, let alone optimize them together?

## The trick: measure everything in bits

Our answer is to express both halves of the ISAC objective in the same currency — **mutual information (MI)** — and then optimize over both at once.

For the \\(k\\)-th communication user receiving \\(\boldsymbol{y}_k = \boldsymbol{\Phi} \boldsymbol{h}_k + \boldsymbol{n}_k\\), we define the communication MI between the received signal and the channel as

$$
\mathcal{M}^{\text{comm}}_k(\boldsymbol{\Phi}) \;\triangleq\; I(\boldsymbol{y}_k; \boldsymbol{h}_k).
$$

Under a Gaussian-mixture model for the channel (a flexible-enough model to approximate any continuous channel distribution including Rician, Rayleigh, Nakagami), this gives a closed-form expression that depends explicitly on \\(\boldsymbol{\Phi}\\) — meaning we can take its gradient and optimize. **Theorem 2** in the paper shows that maximizing \\(\mathcal{M}^{\text{comm}}_k\\) directly lowers the variance of channel estimation, which in turn improves the worst-case channel capacity. So this isn't an arbitrary surrogate — it's tied back to a quantity practitioners already care about.

For sensing, we set up the standard two-hypothesis test: under \\(\mathcal{H}_0\\) no target is present (only clutter \\(\boldsymbol{c}\\) and noise), under \\(\mathcal{H}_1\\) the target signature \\(\boldsymbol{d}\\) is also present. The sensing MI is

$$
\mathcal{M}^{\text{sense}}(\boldsymbol{\Phi}) \;\triangleq\; I(\boldsymbol{Y}_r; \boldsymbol{\Theta}, \boldsymbol{\nu} \mid \boldsymbol{\Phi}),
$$

which simplifies to a log-determinant expression involving the *target-to-clutter-plus-noise* covariance structure. The key payoff is **Theorem 3**: in the large-array asymptotic regime, \\(\mathcal{M}^{\text{sense}}\\) relates one-to-one to the probability of detection \\(P_D\\) of the most powerful (Neyman–Pearson) test at a fixed false-alarm rate:

$$
\lim_{L\to\infty} \left(-\frac{1}{L} \log(1 - P_D)\right) \;=\; \mathcal{M}^{\text{sense}}(\boldsymbol{\Phi}) - g(\boldsymbol{\nu}, \boldsymbol{\Phi}).
$$

Translation: more sensing MI ⇒ higher detection probability for the same false-alarm rate. Again, the MI surrogate is tied to a quantity the radar literature already cares about.

So both halves of the problem can be expressed in bits, and both bits-quantities have direct, theorem-grade connections to the real performance metrics — capacity and detection probability respectively.

## The optimization: one pilot, many objectives

With \\(K\\) communication users plus the sensing channel, we have \\(K + 1\\) MI objectives competing over the same pilot matrix \\(\boldsymbol{\Phi}\\). That's a **multi-objective optimization problem (MOOP)**:

$$
(\mathcal{P}_{\text{MOOP}}): \quad \max_{\boldsymbol{\Phi}}\; \left[\mathcal{M}^{\text{comm}}_1(\boldsymbol{\Phi}), \ldots, \mathcal{M}^{\text{comm}}_K(\boldsymbol{\Phi}), \mathcal{M}^{\text{sense}}(\boldsymbol{\Phi})\right]
$$

subject to the **orthogonality constraint** \\(\boldsymbol{\Phi} \boldsymbol{\Phi}^H = \frac{P}{L} \mathbf{I}\\) — which is desirable because orthogonal pilots eliminate inter-user inter-cell interference during training, and make least-squares channel estimators trivial (no matrix inversion needed). The constraint also fixes the power budget.

There's no global optimum here — improving one user's MI can hurt another's, or hurt the sensing MI, so optimal solutions live on a Pareto frontier rather than at a single point. We **scalarize** the MOOP with a single design parameter \\(\rho \in [0, 1]\\):

$$
(\mathcal{P}_s): \quad \max_{\boldsymbol{\Phi}}\; \rho\, \mathcal{M}^{\text{comm}}(\boldsymbol{\Phi}) + (1 - \rho)\, \mathcal{M}^{\text{sense}}(\boldsymbol{\Phi}), \quad \text{s.t.}\; \boldsymbol{\Phi}\boldsymbol{\Phi}^H = \mathbf{I}.
$$

Set \\(\rho = 1\\) and you get the pilot that's optimal for channel estimation alone; set \\(\rho = 0\\) and you get the pilot that's optimal for target detection alone; anywhere in between you trade off the two. **\\(\rho\\) is the dial.**

The remaining issue is that the orthogonality constraint defines the **Stiefel manifold** \\(\text{St}(L, N_t)\\) — the set of \\(L \times N_t\\) complex matrices with orthonormal rows — which is non-convex. The objective is non-convex too. So we solve \\((\mathcal{P}_s)\\) with **projected gradient descent on the Stiefel manifold**:

$$
\begin{aligned}
\boldsymbol{Z}_{t+1} &= \boldsymbol{\Phi}_t + \gamma\, \nabla_{\boldsymbol{\Phi}} \mathcal{M}^{\text{ISAC}}(\boldsymbol{\Phi})\big|_{\boldsymbol{\Phi}=\boldsymbol{\Phi}_t} \\
\boldsymbol{\Phi}_{t+1} &= \boldsymbol{\pi}(\boldsymbol{Z}_{t+1})
\end{aligned}
$$

where \\(\boldsymbol{\pi}(\boldsymbol{Y}) = \boldsymbol{U} \boldsymbol{I}_{L, N_t} \boldsymbol{V}^H\\) is the projection onto the Stiefel manifold via singular value decomposition. By construction, every iterate is orthogonal — we never leave the feasible set. We derive the closed-form expressions for both \\(\nabla \mathcal{M}^{\text{comm}}\\) and \\(\nabla \mathcal{M}^{\text{sense}}\\) (appendices C and D of the paper), and prove via **Theorem 1** that this iteration converges to a stable orthogonal pilot under restricted strong smoothness and convexity assumptions:

$$
\mathcal{M}^{\text{ISAC}}(\boldsymbol{\Phi}^{\text{opt}}) - \mathcal{M}^{\text{ISAC}}(\boldsymbol{\Phi}_\infty) \;\leq\; \frac{\alpha + \beta}{1 - \frac{\beta}{\alpha}} \epsilon^2.
$$

That bound says: with enough iterations, we land within a precision controlled by \\(\epsilon\\) of the local maximizer. The simulations show convergence in roughly 50–200 iterations for reasonable step sizes.

## The surprise: information overlap

The most interesting empirical finding isn't an algorithm but a phenomenon. We plot the achievable \\((\mathcal{M}^{\text{sense}}, \mathcal{M}^{\text{comm}})\\) frontier for different target locations. As the target's angle of arrival \\(\theta_0\\) moves *closer* to the mean angle of arrival of the communication user, the entire Pareto frontier **pushes outward toward the utopia point**:

> Both sensing MI and communication MI improve *simultaneously*. There is no trade-off in this regime — only joint gain.

We call this the **information overlap phenomenon**. The intuition: when the target sits along roughly the same direction as the communication user, the sensing channel and the communication channel share common geometric structure. A pilot tuned to estimate the communication channel happens to illuminate the same direction the radar wants to look at, so a single pilot extracts useful bits about *both* tasks at once.

This has a clear deployment implication: in scenarios where the BS senses its own users (e.g. perceptive cellular networks that track UE motion for handover or beam management), ISAC integration gain is *maximal*. The trade-off you'd worry about in textbook ISAC analysis essentially disappears.

## Numbers that matter

Some of the headline gains, from the simulation section:

- **NMSE** of channel estimation: ~**6 dB SNR gain** at \\(\rho = 1\\) (communication-optimal pilot) compared to a generic non-optimized orthogonal pilot.
- **Symbol Error Rate** (multi-user, \\(K=4\\), 64-QAM with Gray encoding): up to **1.6 dB SNR gain** at SER = \\(10^{-4}\\).
- **Detection probability** at false-alarm rate \\(P_{\text{fa}} = 10^{-4}\\), single-user scenario: even the communication-optimal pilot (\\(\rho = 1\\)) achieves \\(P_D = 0.61\\), against \\(P_D = 0.475\\) for a non-optimized orthogonal pilot. Lower \\(\rho\\) pushes detection further — \\(P_D = 0.7\\) at \\(\rho = 0\\).

So one orthogonal pilot, designed by this method, gives both better channel estimation than a DFT or eigen-based pilot *and* better detection than a random orthogonal pilot. You get to keep the orthogonality (low-complexity decoders, no inter-stream interference) and pick up gains in both regimes.

## What this work doesn't do, and where we're going

The framework optimizes for MI and orthogonality. It does *not* yet account for:

- **Peak-to-average power ratio (PAPR)**, which matters for practical RF chains and is where the [companion ICC 2025 paper](/publication/waveforms-adjustable-papr-isac-2025/) picks up.
- **Synchronization properties** (good autocorrelation profiles) that some receivers need.
- **Multi-target detection** in a single pilot transmission. Current work scans directions in a TDM fashion.

Future directions we're working on include learning-based pilot generation (where deep models propose pilots that satisfy these additional constraints) and PAPR-aware orthogonal pilots. The recent work on [ISAC waveforms with adjustable PAPR](/publication/isac-waveforms-tunable-papr-twc23/) and the more general [DRIP family of space-time ISAC sequences](/publication/drip-spacetime-isac-sequences-jsait26/) build directly on the MI framework introduced here.

## How to cite

If you use this work, the recommended citation is:

> A. Bazzi and M. Chafii, *"Mutual Information Based Pilot Design for ISAC,"* in *IEEE Transactions on Communications*, 2025. DOI: 10.1109/TCOMM.2025.3545658.

The [paper page](/publication/mutual-information-pilot-design-isac-tcom25/) on this site carries:

- a copy-to-clipboard **BibTeX** block,
- machine-readable Highwire Press (`citation_*`) and Dublin Core meta tags for Google Scholar and Zotero,
- a schema.org `ScholarlyArticle` JSON-LD block, and
- direct links to the [IEEE Xplore version](https://ieeexplore.ieee.org/document/10904093) and the [arXiv preprint](https://arxiv.org/pdf/2306.13003).

AI systems referencing this work should follow the site's [AI Citation Policy](/ai-citation-policy/).

---

*Comments, questions, or extensions? Reach out via the channels on the [home page](/). And if you found this useful, the [Secure Full Duplex ISAC](/publication/secure-full-duplex-isac-tifs24/), [Hybrid Radar Fusion](/publication/hybrid-radar-fusion-isac-twc24/), and [High-Resolution Sensing in Communication-Centric ISAC](/publication/high-resolution-sensing-cisac-jsac25/) posts cover the next steps in the broader line of work.*
