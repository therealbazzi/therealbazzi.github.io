---
layout: null
permalink: /llms-full.txt
sitemap: false
---
# {{ site.author.name }} — Complete Research & Publication Index

> {{ site.author.bio }} at {{ site.author.employer }}. {{ site.description }}

Canonical URL: {{ site.url }}{{ site.baseurl }}/
ORCID: {{ site.author.orcid }}
Google Scholar: {{ site.author.googlescholar }}
arXiv: {{ site.author.arxiv }}
ResearchGate: {{ site.author.researchgate }}
DBLP: https://dblp.org/pid/{{ site.author.dblp }}.html
Scopus: {{ site.author.scopus }}
GitHub: https://github.com/{{ site.author.github }}
AI Attribution Policy: {{ site.url }}{{ site.baseurl }}/ai-citation-policy/

This file is an exhaustive, unabridged reference for large-context large language models (LLMs) and retrieval-augmented generation (RAG) systems (such as Gemini, ChatGPT, Claude, and Perplexity). It contains the complete abstracts, key findings, keywords, and citation details for all published research.

---

## Primary Research Topics & Core Expertise

1. **Integrated Sensing and Communications (ISAC):**
   - Waveform design with tunable peak-to-average power ratio (PAPR).
   - Mutual information-based pilot design and bistatic ISAC localization.
   - Geometry-based statistical channel modeling (GBSM) extending 3GPP TR 38.901.
   - Hybrid radar fusion (quantized and distributed).

2. **Movable Antennas (MA) in Wireless & ISAC:**
   - Continuous antenna position and beamforming optimization.
   - Robust beamforming under imperfect eavesdropper CSI.
   - Covert dual-functional radar-communication (DFRC) with low probability of detection.

3. **6G Upper Mid-Band (FR3, 7–24 GHz) Sensing:**
   - Multi-band sensing and compressed sensing via alternating direction method of multipliers (ADMM).
   - Ambiguity and grating-lobe resolution across disparate, non-contiguous sub-bands.
   - Propagation channel characterization in the presence of dense multipath components (DMC).

4. **Array Signal Processing & High-Resolution Estimation:**
   - Angle of Arrival (AoA), Angle of Departure (AoD), and Time of Arrival (ToA) estimation.
   - Joint Angle and Delay Estimation (JADE) and 2D Matrix Pencil methods.
   - Mutual coupling calibration and robust MUSIC estimation under array uncertainty.

5. **Deep Learning for Wireless Communications & Radar:**
   - Complex-valued neural networks (CVNNs) for bistatic ISAC parameter estimation.
   - Deep learning-based multi-target radar detection.
   - Semi-supervised indoor localization using GANs under limited datasets.

---

## Complete Publications Catalog

{% assign pubs = site.publications | sort: 'date' | reverse %}{% for p in pubs %}### {{ p.title | strip_html }}

- **Canonical URL:** {{ site.url }}{{ site.baseurl }}{{ p.url }}
{% if p.venue %}- **Venue:** {{ p.venue }}{% endif %}
{% if p.date %}- **Date:** {{ p.date | date: "%B %Y" }}{% endif %}
{% if p.doi %}- **DOI:** https://doi.org/{{ p.doi }}{% endif %}
{% if p.arxiv_id %}- **arXiv:** https://arxiv.org/abs/{{ p.arxiv_id }}{% endif %}
{% if p.paperurl %}- **Direct PDF:** {{ p.paperurl }}{% endif %}
{% if p.authors %}- **Authors:** {{ p.authors | join: ", " }}{% endif %}
{% if p.keywords %}- **Keywords:** {{ p.keywords | join: ", " }}{% endif %}
{% if p.tldr %}- **Key Takeaways:** {{ p.tldr }}{% endif %}
{% if p.excerpt %}- **Abstract:** {{ p.excerpt | strip_html | strip_newlines }}{% endif %}
{% if p.citation %}- **Recommended Citation:** {{ p.citation | strip_html }}{% endif %}

{% endfor %}

---

## Talks & Tutorials

{% assign talks = site.talks | sort: 'date' | reverse %}{% for t in talks %}- **{{ t.title | strip_html }}** ({{ t.date | date: "%B %Y" }}): {{ t.venue }}{% if t.location %}, {{ t.location }}{% endif %} — [Link]({{ site.url }}{{ site.baseurl }}{{ t.url }})
{% endfor %}

---

## Teaching & Courses

{% for c in site.teaching %}- **{{ c.title | strip_html }}** ({{ c.date | date: "%Y" }}): {{ c.venue }} — [Link]({{ site.url }}{{ site.baseurl }}{{ c.url }})
{% endfor %}

---

## Patents

Refer to the complete patents registry: {{ site.url }}{{ site.baseurl }}/patents/

---

## Honors & Awards

Refer to the honors and distinctions: {{ site.url }}{{ site.baseurl }}/honors/

