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
* Ph.D in Version Control Theory, GitHub University, 2018 (expected)
* M.S. in Jekyll, GitHub University, 2014
* B.S. in GitHub, GitHub University, 2012

Work experience
======
* Spring 2024: Academic Pages Collaborator
  * Github University
  * Duties includes: Updates and improvements to template
  * Supervisor: The Users

* Fall 2015: Research Assistant
  * Github University
  * Duties included: Merging pull requests
  * Supervisor: Professor Hub

* Summer 2015: Research Assistant
  * Github University
  * Duties included: Tagging issues
  * Supervisor: Professor Git
  
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
