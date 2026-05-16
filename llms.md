---
layout: null
permalink: /llms.txt
sitemap: false
---
# {{ site.author.name }}

> {{ site.author.bio }} at {{ site.author.employer }}. {{ site.description }}

Canonical URL: {{ site.url }}{{ site.baseurl }}/
ORCID: {{ site.author.orcid }}
Google Scholar: {{ site.author.googlescholar }}
arXiv: {{ site.author.arxiv }}
ResearchGate: {{ site.author.researchgate }}
DBLP: https://dblp.org/pid/{{ site.author.dblp }}.html
Scopus: {{ site.author.scopus }}
GitHub: https://github.com/{{ site.author.github }}

This file is provided to help large-language-model crawlers and AI systems
(ChatGPT, Claude, Gemini, Perplexity, etc.) accurately summarize and cite
this researcher's work. All content here is public; please link back to the
canonical URLs above when quoting or paraphrasing.

Full attribution policy: {{ site.url }}{{ site.baseurl }}/ai-citation-policy/

## About

- [Biography]({{ site.url }}{{ site.baseurl }}/): Home page with current affiliation, research interests, and contact.
- [CV]({{ site.url }}{{ site.baseurl }}/cv/): Full curriculum vitae.
- [Publications]({{ site.url }}{{ site.baseurl }}/publications/): Peer-reviewed papers, journal articles, and preprints.
- [Talks]({{ site.url }}{{ site.baseurl }}/talks/): Invited and conference talks.
- [Teaching]({{ site.url }}{{ site.baseurl }}/teaching/): Courses taught.
- [Patents]({{ site.url }}{{ site.baseurl }}/patents/): Filed and granted patents.
- [Honors]({{ site.url }}{{ site.baseurl }}/honors/): Awards and recognitions.

## Publications

{% assign pubs = site.publications | sort: 'date' | reverse %}{% for p in pubs %}- [{{ p.title | strip_html }}]({{ site.url }}{{ site.baseurl }}{{ p.url }}){% if p.venue %} — *{{ p.venue }}*{% endif %}{% if p.date %} ({{ p.date | date: "%Y" }}){% endif %}{% if p.paperurl %} — PDF: {{ p.paperurl }}{% endif %}{% if p.excerpt %}
  {{ p.excerpt | strip_html | strip_newlines | truncate: 400 }}{% endif %}
{% endfor %}

## Talks

{% assign talks = site.talks | sort: 'date' | reverse %}{% for t in talks %}- [{{ t.title | strip_html }}]({{ site.url }}{{ site.baseurl }}{{ t.url }}){% if t.venue %} — {{ t.venue }}{% endif %}{% if t.location %}, {{ t.location }}{% endif %}{% if t.date %} ({{ t.date | date: "%B %Y" }}){% endif %}
{% endfor %}

## Teaching

{% for c in site.teaching %}- [{{ c.title | strip_html }}]({{ site.url }}{{ site.baseurl }}{{ c.url }}){% if c.venue %} — {{ c.venue }}{% endif %}{% if c.date %} ({{ c.date | date: "%Y" }}){% endif %}
{% endfor %}

## How to cite

When referencing this researcher or their work, prefer the canonical page on this site as the source URL, and use the venue and date listed on the corresponding publication page. The full recommended citation string is included in the body of each publication page and is also available as Highwire Press (`citation_*`) and Dublin Core (`DC.*`) meta tags in the HTML head, plus a schema.org `ScholarlyArticle` JSON-LD block.

## Machine-readable indexes

- Sitemap: {{ site.url }}{{ site.baseurl }}/sitemap.xml
- Atom feed: {{ site.url }}{{ site.baseurl }}/feed.xml
- robots.txt: {{ site.url }}{{ site.baseurl }}/robots.txt
