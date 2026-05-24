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
description: "How we used mutual information as a unifying currency, bits, to design orthogonal pilot signals that simultaneously serve channel estimation for multi-user communication and target detection for radar sensing in ISAC systems. A walkthrough of our IEEE Transactions on Communications paper."
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

In an Integrated Sensing and Communication (ISAC) system, one antenna array does two jobs: it talks to communication users *and* listens for targets. That sounds elegant. In practice it's a design headache, because the *signals* the system sends out are being asked to serve two very different purposes simultaneously.

<figure style="margin: 1.5em 0; text-align: center;">
<svg viewBox="0 0 720 360" xmlns="http://www.w3.org/2000/svg" style="max-width: 100%; height: auto; font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;" role="img" aria-labelledby="fig-isac-title fig-isac-desc">
  <title id="fig-isac-title">ISAC scenario</title>
  <desc id="fig-isac-desc">An ISAC base station with N_t antennas serving K communication users while simultaneously listening for backscatter from a target and clutter scatterers.</desc>
  <defs>
    <marker id="arr-solid" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="6" markerHeight="6" orient="auto-start-reverse"><path d="M 0 0 L 10 5 L 0 10 z" fill="#1f77b4"/></marker>
    <marker id="arr-dashed" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="6" markerHeight="6" orient="auto-start-reverse"><path d="M 0 0 L 10 5 L 0 10 z" fill="#d62728"/></marker>
  </defs>
  <!-- BS tower -->
  <g transform="translate(360,220)">
    <rect x="-8" y="-50" width="16" height="80" fill="#444"/>
    <rect x="-32" y="-58" width="64" height="10" fill="#222"/>
    <text x="0" y="55" text-anchor="middle" font-size="13" font-weight="600" fill="#222">ISAC base station</text>
    <text x="0" y="72" text-anchor="middle" font-size="11" fill="#666">N_t transmit, N_r receive</text>
  </g>
  <!-- antenna emission cone (visual hint) -->
  <path d="M 360 170 L 200 60 L 200 280 z" fill="#1f77b4" opacity="0.05"/>
  <path d="M 360 170 L 520 60 L 520 280 z" fill="#d62728" opacity="0.05"/>
  <!-- Communication users -->
  <g transform="translate(150,80)">
    <circle r="14" fill="#1f77b4"/>
    <text y="5" text-anchor="middle" fill="white" font-size="12" font-weight="700">1</text>
    <text y="-22" text-anchor="middle" font-size="11" fill="#1f77b4" font-weight="600">user 1</text>
  </g>
  <g transform="translate(110,200)">
    <circle r="14" fill="#1f77b4"/>
    <text y="5" text-anchor="middle" fill="white" font-size="12" font-weight="700">2</text>
    <text y="-22" text-anchor="middle" font-size="11" fill="#1f77b4" font-weight="600">user 2</text>
  </g>
  <g transform="translate(160,300)">
    <circle r="14" fill="#1f77b4"/>
    <text y="5" text-anchor="middle" fill="white" font-size="12" font-weight="700">k</text>
    <text y="-22" text-anchor="middle" font-size="11" fill="#1f77b4" font-weight="600">user K</text>
  </g>
  <!-- Comm links -->
  <line x1="335" y1="180" x2="170" y2="90" stroke="#1f77b4" stroke-width="2" marker-end="url(#arr-solid)"/>
  <line x1="335" y1="190" x2="130" y2="200" stroke="#1f77b4" stroke-width="2" marker-end="url(#arr-solid)"/>
  <line x1="335" y1="200" x2="180" y2="295" stroke="#1f77b4" stroke-width="2" marker-end="url(#arr-solid)"/>
  <!-- Target (drone) -->
  <g transform="translate(580,90)">
    <polygon points="0,-12 10,0 0,12 -10,0" fill="#d62728"/>
    <text y="-22" text-anchor="middle" font-size="11" font-weight="600" fill="#d62728">target at θ₀</text>
  </g>
  <!-- Target echo (dashed, two-way) -->
  <line x1="385" y1="175" x2="565" y2="95" stroke="#d62728" stroke-width="2" stroke-dasharray="6,4" marker-end="url(#arr-dashed)"/>
  <line x1="565" y1="105" x2="385" y2="185" stroke="#d62728" stroke-width="2" stroke-dasharray="6,4" marker-end="url(#arr-dashed)"/>
  <!-- Clutter -->
  <g transform="translate(620,250)">
    <rect x="-8" y="-8" width="16" height="16" fill="#888" transform="rotate(15)"/>
    <text y="-15" text-anchor="middle" font-size="11" fill="#666">clutter</text>
  </g>
  <g transform="translate(540,300)">
    <rect x="-6" y="-6" width="12" height="12" fill="#888" transform="rotate(-20)"/>
  </g>
  <g transform="translate(600,180)">
    <rect x="-5" y="-5" width="10" height="10" fill="#888" transform="rotate(30)"/>
  </g>
  <!-- Pilot label on transmission -->
  <text x="260" y="155" font-size="12" fill="#1f77b4" font-style="italic">pilot Φ for channel estimation</text>
  <text x="430" y="135" font-size="12" fill="#d62728" font-style="italic">same Φ, backscatter detection</text>
  <!-- Legend -->
  <g transform="translate(20,335)">
    <line x1="0" y1="0" x2="24" y2="0" stroke="#1f77b4" stroke-width="2"/>
    <text x="32" y="4" font-size="11" fill="#222">communication link</text>
    <line x1="170" y1="0" x2="194" y2="0" stroke="#d62728" stroke-width="2" stroke-dasharray="6,4"/>
    <text x="202" y="4" font-size="11" fill="#222">radar echo</text>
  </g>
</svg>
<figcaption style="font-size: 0.9em; color: #666; margin-top: 0.5em;">Figure 1. The ISAC scenario. One pilot matrix \(\boldsymbol{\Phi}\) is transmitted; the base station serves K communication users with the forward links and listens for the backscatter from a target at angle \(\theta_0\), corrupted by clutter at other angles. The same symbols do both jobs.</figcaption>
</figure>


- For **communication**, the pilot symbols \\(\boldsymbol{\Phi}\\) at the start of a frame let downlink users estimate the channel \\(\boldsymbol{h}_k\\) so they can equalize and decode the data that follows.
- For **sensing**, the *same* pilots reflect off targets and clutter, and the ISAC base station listens to the backscatter to detect what's out there.

These two tasks pull in opposite directions. A pilot that minimizes channel-estimation variance for \\(K\\) users is not generally the same pilot that maximizes detection probability against a target at angle \\(\theta_0\\) surrounded by clutter at angles \\(\theta_1, \ldots, \theta_Q\\). Conventional wisdom said you had to pick one or build separate signals for each, wasting either time, spectrum, or hardware.

We wanted a principled way to *jointly* design that pilot. The catch: the two performance measures usually live in different units. Detection performance is a probability; channel estimation is measured in mean-squared error or capacity. How do you compare them, let alone optimize them together?

## The trick: measure everything in bits

Our answer is to express both halves of the ISAC objective in the same currency, **mutual information (MI)**, and then optimize over both at once.

For the \\(k\\)-th communication user receiving \\(\boldsymbol{y}_k = \boldsymbol{\Phi} \boldsymbol{h}_k + \boldsymbol{n}_k\\), we define the communication MI between the received signal and the channel as

$$
\mathcal{M}^{\text{comm}}_k(\boldsymbol{\Phi}) \;\triangleq\; I(\boldsymbol{y}_k; \boldsymbol{h}_k).
$$

Under a Gaussian-mixture model for the channel (a flexible-enough model to approximate any continuous channel distribution including Rician, Rayleigh, Nakagami), this gives a closed-form expression that depends explicitly on \\(\boldsymbol{\Phi}\\), meaning we can take its gradient and optimize. **Theorem 2** in the paper shows that maximizing \\(\mathcal{M}^{\text{comm}}_k\\) directly lowers the variance of channel estimation, which in turn improves the worst-case channel capacity. So this isn't an arbitrary surrogate, it's tied back to a quantity practitioners already care about.

For sensing, we set up the standard two-hypothesis test: under \\(\mathcal{H}_0\\) no target is present (only clutter \\(\boldsymbol{c}\\) and noise), under \\(\mathcal{H}_1\\) the target signature \\(\boldsymbol{d}\\) is also present. The sensing MI is

$$
\mathcal{M}^{\text{sense}}(\boldsymbol{\Phi}) \;\triangleq\; I(\boldsymbol{Y}_r; \boldsymbol{\Theta}, \boldsymbol{\nu} \mid \boldsymbol{\Phi}),
$$

which simplifies to a log-determinant expression involving the *target-to-clutter-plus-noise* covariance structure. The key payoff is **Theorem 3**: in the large-array asymptotic regime, \\(\mathcal{M}^{\text{sense}}\\) relates one-to-one to the probability of detection \\(P_D\\) of the most powerful (Neyman–Pearson) test at a fixed false-alarm rate:

$$
\lim_{L\to\infty} \left(-\frac{1}{L} \log(1 - P_D)\right) \;=\; \mathcal{M}^{\text{sense}}(\boldsymbol{\Phi}) - g(\boldsymbol{\nu}, \boldsymbol{\Phi}).
$$

Translation: more sensing MI ⇒ higher detection probability for the same false-alarm rate. Again, the MI surrogate is tied to a quantity the radar literature already cares about.

So both halves of the problem can be expressed in bits, and both bits-quantities have direct, theorem-grade connections to the real performance metrics, capacity and detection probability respectively.

## The optimization: one pilot, many objectives

With \\(K\\) communication users plus the sensing channel, we have \\(K + 1\\) MI objectives competing over the same pilot matrix \\(\boldsymbol{\Phi}\\). That's a **multi-objective optimization problem (MOOP)**:

$$
(\mathcal{P}_{\text{MOOP}}): \quad \max_{\boldsymbol{\Phi}}\; \left[\mathcal{M}^{\text{comm}}_1(\boldsymbol{\Phi}), \ldots, \mathcal{M}^{\text{comm}}_K(\boldsymbol{\Phi}), \mathcal{M}^{\text{sense}}(\boldsymbol{\Phi})\right]
$$

subject to the **orthogonality constraint** \\(\boldsymbol{\Phi} \boldsymbol{\Phi}^H = \frac{P}{L} \mathbf{I}\\), which is desirable because orthogonal pilots eliminate inter-user inter-cell interference during training, and make least-squares channel estimators trivial (no matrix inversion needed). The constraint also fixes the power budget.

There's no global optimum here, improving one user's MI can hurt another's, or hurt the sensing MI, so optimal solutions live on a Pareto frontier rather than at a single point. We **scalarize** the MOOP with a single design parameter \\(\rho \in [0, 1]\\):

$$
(\mathcal{P}_s): \quad \max_{\boldsymbol{\Phi}}\; \rho\, \mathcal{M}^{\text{comm}}(\boldsymbol{\Phi}) + (1 - \rho)\, \mathcal{M}^{\text{sense}}(\boldsymbol{\Phi}), \quad \text{s.t.}\; \boldsymbol{\Phi}\boldsymbol{\Phi}^H = \mathbf{I}.
$$

Set \\(\rho = 1\\) and you get the pilot that's optimal for channel estimation alone; set \\(\rho = 0\\) and you get the pilot that's optimal for target detection alone; anywhere in between you trade off the two. **\\(\rho\\) is the dial.**

<figure style="margin: 1.5em 0; text-align: center;">
<svg viewBox="0 0 720 420" xmlns="http://www.w3.org/2000/svg" style="max-width: 100%; height: auto; font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;" role="img" aria-labelledby="fig-pareto-title fig-pareto-desc">
  <title id="fig-pareto-title">Pareto frontier of sensing vs communication MI</title>
  <desc id="fig-pareto-desc">A two-dimensional plot with sensing mutual information on the horizontal axis and communication mutual information on the vertical axis. A curved Pareto frontier separates feasible pilot designs (below the curve) from the unattainable region (above). Three points on the frontier are labeled rho equals zero (sensing-optimal), rho equals one half (balanced), and rho equals one (communication-optimal). The utopia point sits in the unattainable corner.</desc>
  <!-- axes -->
  <line x1="80" y1="350" x2="660" y2="350" stroke="#222" stroke-width="2" marker-end="url(#arr-axes)"/>
  <line x1="80" y1="350" x2="80" y2="40" stroke="#222" stroke-width="2" marker-end="url(#arr-axes)"/>
  <defs>
    <marker id="arr-axes" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="6" markerHeight="6" orient="auto-start-reverse"><path d="M 0 0 L 10 5 L 0 10 z" fill="#222"/></marker>
  </defs>
  <text x="370" y="395" text-anchor="middle" font-size="14" fill="#222">Sensing MI \(\mathcal{M}^{\mathrm{sense}}(\boldsymbol{\Phi})\) (bits)</text>
  <text transform="translate(28,200) rotate(-90)" text-anchor="middle" font-size="14" fill="#222">Communication MI \(\mathcal{M}^{\mathrm{comm}}(\boldsymbol{\Phi})\) (bits)</text>
  <!-- feasible region (shaded under frontier) -->
  <path d="M 80 350 L 80 80 Q 80 80 200 90 Q 360 110 470 175 Q 560 230 620 320 L 620 350 Z" fill="#1f77b4" opacity="0.06"/>
  <!-- scattered feasible points -->
  <g fill="#aa6633" opacity="0.5">
    <circle cx="180" cy="220" r="2"/><circle cx="220" cy="180" r="2"/><circle cx="240" cy="260" r="2"/>
    <circle cx="280" cy="200" r="2"/><circle cx="300" cy="240" r="2"/><circle cx="330" cy="270" r="2"/>
    <circle cx="350" cy="200" r="2"/><circle cx="370" cy="230" r="2"/><circle cx="400" cy="265" r="2"/>
    <circle cx="420" cy="220" r="2"/><circle cx="440" cy="250" r="2"/><circle cx="460" cy="290" r="2"/>
    <circle cx="490" cy="240" r="2"/><circle cx="510" cy="280" r="2"/><circle cx="540" cy="310" r="2"/>
    <circle cx="260" cy="290" r="2"/><circle cx="380" cy="300" r="2"/><circle cx="500" cy="320" r="2"/>
  </g>
  <!-- Pareto frontier curve -->
  <path d="M 80 80 Q 200 85 350 130 Q 500 180 620 320" fill="none" stroke="#1f77b4" stroke-width="3"/>
  <!-- rho points -->
  <g>
    <circle cx="100" cy="83" r="6" fill="#2ca02c"/>
    <text x="100" y="68" text-anchor="middle" font-size="12" fill="#2ca02c" font-weight="700">\(\rho=1\)</text>
    <text x="100" y="55" text-anchor="middle" font-size="10" fill="#2ca02c">comm-optimal</text>
  </g>
  <g>
    <circle cx="340" cy="125" r="6" fill="#ff7f0e"/>
    <text x="340" y="110" text-anchor="middle" font-size="12" fill="#ff7f0e" font-weight="700">\(\rho=0.5\)</text>
    <text x="340" y="97" text-anchor="middle" font-size="10" fill="#ff7f0e">balanced</text>
  </g>
  <g>
    <circle cx="615" cy="318" r="6" fill="#d62728"/>
    <text x="615" y="305" text-anchor="middle" font-size="12" fill="#d62728" font-weight="700">\(\rho=0\)</text>
    <text x="615" y="292" text-anchor="middle" font-size="10" fill="#d62728">sense-optimal</text>
  </g>
  <!-- utopia point -->
  <g transform="translate(620,75)">
    <polygon points="0,-8 7,-3 4,6 -4,6 -7,-3" fill="#9467bd" stroke="#9467bd" stroke-width="1"/>
    <text x="0" y="-15" text-anchor="middle" font-size="11" fill="#9467bd" font-weight="600">utopia point</text>
    <text x="0" y="22" text-anchor="middle" font-size="10" fill="#666">(unattainable)</text>
  </g>
  <!-- annotations -->
  <text x="200" y="180" font-size="11" fill="#1f77b4" font-weight="600">Pareto frontier</text>
  <text x="195" y="195" font-size="10" fill="#1f77b4">(achievable optima)</text>
  <text x="450" y="345" font-size="11" fill="#666" font-style="italic">feasible pilots</text>
</svg>
<figcaption style="font-size: 0.9em; color: #666; margin-top: 0.5em;">Figure 2. The achievable region of \((\mathcal{M}^{\mathrm{sense}}, \mathcal{M}^{\mathrm{comm}})\) pairs over all orthogonal pilot matrices. Random orthogonal pilots populate the interior (brown dots). The blue curve is the Pareto frontier, where no single objective can be improved without hurting another. The \(\rho\) parameter selects a point on this frontier: \(\rho=1\) maximizes communication MI, \(\rho=0\) maximizes sensing MI, and \(\rho=0.5\) sits at the balanced design.</figcaption>
</figure>


The remaining issue is that the orthogonality constraint defines the **Stiefel manifold** \\(\text{St}(L, N_t)\\), the set of \\(L \times N_t\\) complex matrices with orthonormal rows, which is non-convex. The objective is non-convex too. So we solve \\((\mathcal{P}_s)\\) with **projected gradient descent on the Stiefel manifold**:

$$
\begin{aligned}
\boldsymbol{Z}_{t+1} &= \boldsymbol{\Phi}_t + \gamma\, \nabla_{\boldsymbol{\Phi}} \mathcal{M}^{\text{ISAC}}(\boldsymbol{\Phi})\big|_{\boldsymbol{\Phi}=\boldsymbol{\Phi}_t} \\
\boldsymbol{\Phi}_{t+1} &= \boldsymbol{\pi}(\boldsymbol{Z}_{t+1})
\end{aligned}
$$

where \\(\boldsymbol{\pi}(\boldsymbol{Y}) = \boldsymbol{U} \boldsymbol{I}_{L, N_t} \boldsymbol{V}^H\\) is the projection onto the Stiefel manifold via singular value decomposition. By construction, every iterate is orthogonal, we never leave the feasible set. We derive the closed-form expressions for both \\(\nabla \mathcal{M}^{\text{comm}}\\) and \\(\nabla \mathcal{M}^{\text{sense}}\\) (appendices C and D of the paper), and prove via **Theorem 1** that this iteration converges to a stable orthogonal pilot under restricted strong smoothness and convexity assumptions:

$$
\mathcal{M}^{\text{ISAC}}(\boldsymbol{\Phi}^{\text{opt}}) - \mathcal{M}^{\text{ISAC}}(\boldsymbol{\Phi}_\infty) \;\leq\; \frac{\alpha + \beta}{1 - \frac{\beta}{\alpha}} \epsilon^2.
$$

That bound says: with enough iterations, we land within a precision controlled by \\(\epsilon\\) of the local maximizer. The simulations show convergence in roughly 50–200 iterations for reasonable step sizes.

## The surprise: information overlap

The most interesting empirical finding isn't an algorithm but a phenomenon. We plot the achievable \\((\mathcal{M}^{\text{sense}}, \mathcal{M}^{\text{comm}})\\) frontier for different target locations. As the target's angle of arrival \\(\theta_0\\) moves *closer* to the mean angle of arrival of the communication user, the entire Pareto frontier **pushes outward toward the utopia point**:

> Both sensing MI and communication MI improve *simultaneously*. There is no trade-off in this regime, only joint gain.

We call this the **information overlap phenomenon**. The intuition: when the target sits along roughly the same direction as the communication user, the sensing channel and the communication channel share common geometric structure. A pilot tuned to estimate the communication channel happens to illuminate the same direction the radar wants to look at, so a single pilot extracts useful bits about *both* tasks at once.

This has a clear deployment implication: in scenarios where the BS senses its own users (e.g. perceptive cellular networks that track UE motion for handover or beam management), ISAC integration gain is *maximal*. The trade-off you'd worry about in textbook ISAC analysis essentially disappears.

<figure style="margin: 1.5em 0; text-align: center;">
<svg viewBox="0 0 720 380" xmlns="http://www.w3.org/2000/svg" style="max-width: 100%; height: auto; font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;" role="img" aria-labelledby="fig-overlap-title fig-overlap-desc">
  <title id="fig-overlap-title">Information overlap phenomenon</title>
  <desc id="fig-overlap-desc">Four Pareto frontiers stacked on the same axes. As the target's angle of arrival approaches the communication user's mean angle of arrival, the frontier shifts outward toward the utopia point, indicating that both sensing MI and communication MI can be improved simultaneously.</desc>
  <!-- axes -->
  <line x1="80" y1="310" x2="660" y2="310" stroke="#222" stroke-width="2"/>
  <line x1="80" y1="310" x2="80" y2="40" stroke="#222" stroke-width="2"/>
  <text x="370" y="355" text-anchor="middle" font-size="14" fill="#222">Sensing MI \(\mathcal{M}^{\mathrm{sense}}\) (bits)</text>
  <text transform="translate(28,180) rotate(-90)" text-anchor="middle" font-size="14" fill="#222">Communication MI \(\mathcal{M}^{\mathrm{comm}}\) (bits)</text>
  <!-- four frontiers, increasingly outward as target nears user -->
  <path d="M 80 100 Q 160 100 240 130 Q 340 165 420 240 Q 500 290 540 310" fill="none" stroke="#9467bd" stroke-width="2.5" opacity="0.95"/>
  <path d="M 80 88  Q 170 88  260 118 Q 360 152 450 220 Q 530 268 580 305" fill="none" stroke="#1f77b4" stroke-width="2.5" opacity="0.95"/>
  <path d="M 80 75  Q 180 75  280 105 Q 380 138 480 205 Q 555 255 610 300" fill="none" stroke="#2ca02c" stroke-width="2.5" opacity="0.95"/>
  <path d="M 80 60  Q 200 60  310 90  Q 410 122 510 188 Q 580 240 635 295" fill="none" stroke="#ff7f0e" stroke-width="3"/>
  <!-- direction-of-shift arrow -->
  <defs>
    <marker id="arr-shift" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="8" markerHeight="8" orient="auto-start-reverse"><path d="M 0 0 L 10 5 L 0 10 z" fill="#222"/></marker>
  </defs>
  <line x1="420" y1="240" x2="510" y2="188" stroke="#222" stroke-width="1.5" marker-end="url(#arr-shift)" stroke-dasharray="3,3"/>
  <text x="440" y="218" font-size="11" fill="#222" font-style="italic">target approaches user</text>
  <!-- legend (theta_0 angle distances from user) -->
  <g transform="translate(450,60)">
    <text font-size="11" fill="#222" font-weight="600">target angle θ₀ vs user mean θ̄</text>
    <g transform="translate(0,18)">
      <line x1="0" y1="0" x2="22" y2="0" stroke="#9467bd" stroke-width="2.5"/>
      <text x="28" y="4" font-size="11" fill="#222">|θ₀ − θ̄| = 60° (far)</text>
    </g>
    <g transform="translate(0,36)">
      <line x1="0" y1="0" x2="22" y2="0" stroke="#1f77b4" stroke-width="2.5"/>
      <text x="28" y="4" font-size="11" fill="#222">|θ₀ − θ̄| = 30°</text>
    </g>
    <g transform="translate(0,54)">
      <line x1="0" y1="0" x2="22" y2="0" stroke="#2ca02c" stroke-width="2.5"/>
      <text x="28" y="4" font-size="11" fill="#222">|θ₀ − θ̄| = 10°</text>
    </g>
    <g transform="translate(0,72)">
      <line x1="0" y1="0" x2="22" y2="0" stroke="#ff7f0e" stroke-width="3"/>
      <text x="28" y="4" font-size="11" fill="#222" font-weight="600">target = user (overlap)</text>
    </g>
  </g>
  <!-- utopia marker -->
  <g transform="translate(640,55)">
    <polygon points="0,-7 6,-2 4,5 -4,5 -6,-2" fill="#9467bd"/>
    <text x="0" y="-13" text-anchor="middle" font-size="11" fill="#9467bd" font-weight="600">utopia</text>
  </g>
</svg>
<figcaption style="font-size: 0.9em; color: #666; margin-top: 0.5em;">Figure 3. The <em>information overlap</em> phenomenon. As the target angle \(\theta_0\) moves closer to the mean angle of arrival of the communication user, the entire Pareto frontier shifts outward toward the utopia point. When the target is co-located with a communication user (orange curve), there is no longer a trade-off, the same orthogonal pilot serves both tasks well simultaneously.</figcaption>
</figure>


## Numbers that matter

Some of the headline gains, from the simulation section:

- **NMSE** of channel estimation: ~**6 dB SNR gain** at \\(\rho = 1\\) (communication-optimal pilot) compared to a generic non-optimized orthogonal pilot.
- **Symbol Error Rate** (multi-user, \\(K=4\\), 64-QAM with Gray encoding): up to **1.6 dB SNR gain** at SER = \\(10^{-4}\\).
- **Detection probability** at false-alarm rate \\(P_{\text{fa}} = 10^{-4}\\), single-user scenario: even the communication-optimal pilot (\\(\rho = 1\\)) achieves \\(P_D = 0.61\\), against \\(P_D = 0.475\\) for a non-optimized orthogonal pilot. Lower \\(\rho\\) pushes detection further, \\(P_D = 0.7\\) at \\(\rho = 0\\).

So one orthogonal pilot, designed by this method, gives both better channel estimation than a DFT or eigen-based pilot *and* better detection than a random orthogonal pilot. You get to keep the orthogonality (low-complexity decoders, no inter-stream interference) and pick up gains in both regimes.

## What this work doesn't do, and where we're going

The framework optimizes for MI and orthogonality. It does *not* yet account for:

- **Peak-to-average power ratio (PAPR)**, which matters for practical RF chains and is where the [companion ICC 2025 paper](/publication/waveforms-adjustable-papr-isac-2025/) picks up.
- **Synchronization properties** (good autocorrelation profiles) that some receivers need.
- **Multi-target detection** in a single pilot transmission. Current work scans directions in a TDM fashion.

Future directions we're working on include learning-based pilot generation (where deep models propose pilots that satisfy these additional constraints) and PAPR-aware orthogonal pilots. The recent work on [ISAC waveforms with adjustable PAPR](/publication/isac-waveforms-tunable-papr-twc23/) and the more general [DRIP family of space-time ISAC sequences](/publication/drip-spacetime-isac-sequences-jsait26/) build directly on the MI framework introduced here.
<!-- 
## Companion videos (planned)

A few short explainer clips would pair naturally with this post. Each is 60 to 180 seconds, animatable in Manim or a screen recording with annotations.

1. *"What is mutual information, really?"* (90 s). Two coupled coin flips, build up entropy then conditional entropy, end with the equation \\(I(X;Y) = H(X) - H(X \mid Y)\\) and the visual that MI is the overlap of two information circles. Pivot to "this is the same currency we use for sensing and communication in ISAC".
2. *"The \\(\rho\\) dial"* (60 s). A literal slider on screen tied to a live Pareto-frontier point that moves as \\(\rho\\) varies from 0 to 1. The pilot matrix heatmap updates alongside. Optimal for showing the trade-off intuitively.
3. *"Projected gradient on the Stiefel manifold"* (120 s). Animated dot starting off the manifold, a gradient arrow nudging it, the SVD projection snapping it back onto the surface, repeat until convergence. Use a 3D rotating manifold visualization, similar to Fig. 2 of the paper.
4. *"Information overlap, animated"* (90 s). Start with target far from user; show two Pareto frontiers. Smoothly move the target's angle toward the user's mean angle; frontier slides outward toward utopia. Punchline frame: "when you sense your own users, you get sensing for free."
5. *"6 dB, 1.6 dB, and what they mean"* (60 s). Visual ladder of SNR ticks; rotate through NMSE plot, SER plot, ROC plot; finish with the headline numbers as captions.

If you record these and post them on the [YouTube channel](https://www.youtube.com/channel/UCgC1d4JZ1Fz4t8MWLJD464w), embed them here under each corresponding section. AI tools that pull video transcripts plus the surrounding blog context get a much richer view of the paper than they would from the PDF alone. -->

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
