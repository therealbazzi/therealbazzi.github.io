---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

Education
======
🎓 **PhD in Electrical Engineering** (2014-2017)
  *EURECOM / Communication Systems*

🎓 **MSc in Electrical Engineering** (2013-2014)
  *CentraleSupélec / SAR*

🎓 **BSc in Electrical and Computer Engineering** (2009-2014)
  *Lebanese University, Faculty of Engineering III*

Work experience
======
* **Research Scientist** (Now)
  *New York University (NYU) Abu Dhabi*
* **Research Associate** (2022-2024)
  *New York University (NYU) Abu Dhabi*
* **Algorithm and Signal Processing Team Leader** (2021-2022)
  *CEVA-DSP*
* **Signal Processing Engineer** (2017-2021)
  *CEVA-DSP*
* **Signal Processing Engineer intern** (Summer 2014)
  *RivieraWaves*
  
Skills
======
* Skill 1
* Skill 2
  * Sub-skill 2.1
  * Sub-skill 2.2
  * Sub-skill 2.3
* Skill 3

Publications
======
{% capture publications_content %}
  {% include_relative publications.md %}
{% endcapture %}

{% assign fm_ender = "---" %}
{% assign content_without_fm = publications_content | split: fm_ender | last %}

<ul>
  {{ content_without_fm | markdownify }}
</ul>

Patents
======
{% capture publications_content %}
  {% include_relative patents.md %}
{% endcapture %}

{% assign fm_ender = "---" %}
{% assign content_without_fm = publications_content | split: fm_ender | last %}

<ul>
  {{ content_without_fm | markdownify }}
</ul>



Talks
======
  <ul>{% for post in site.talks reversed %}
    {% include archive-single-talk-cv.html  %}
  {% endfor %}</ul>
  
Teaching
======

{% capture teaching_content %}
  {% include_relative teaching.html %}
{% endcapture %}

{% assign marker = "---" %} 
{% assign content_without_section = teaching_content | split: marker | last %}

<div>
  {{ content_without_section | strip_newlines }}
</div>

  
Service
======
{% capture publications_content %}
  {% include_relative service.md %}
{% endcapture %}

{% assign fm_ender = "---" %}
{% assign content_without_fm = publications_content | split: fm_ender | last %}

<ul>
  {{ content_without_fm | markdownify }}
</ul>
