---
layout: page
title: About
permalink: /about/
---

## About the Lab

<p class="provisional-note">
[PLACEHOLDER] Waisman Lab is an early-career research group based in Buenos
Aires, Argentina, studying human pluripotent stem cell-derived
cardiomyocytes. The lab is affiliated with FLENI, INEU, and CONICET.
</p>

## Institutional Affiliations

{% include institutions-grid.html %}

## Location

<p>{{ site.location }}</p>
<p class="provisional-note">[PLACEHOLDER] Map / institutional address to be added later.</p>

## Contact

<ul class="contact-list">
  <li><strong>{{ site.pi_name }}</strong></li>
  <li><a href="mailto:{{ site.contact_email }}">{{ site.contact_email }}</a></li>
  {% assign inst_names = site.data.institutions | map: "name" %}
  <li>{{ inst_names | join: " · " }}</li>
  <li><a href="{{ site.github_org_url }}" target="_blank" rel="noopener">GitHub</a></li>
  {% if site.google_scholar_url and site.google_scholar_url != "" %}
  <li><a href="{{ site.google_scholar_url }}" target="_blank" rel="noopener">Google Scholar</a></li>
  {% endif %}
</ul>
