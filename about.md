---
layout: page
title: About the Lab
permalink: /about/
---

<p class="provisional-note">
The Waisman Lab is an early-career research group established in 2022 at FLENI in Buenos Aires, Argentina. We work with human pluripotent stem cell-derived cardiomyocytes to study heart muscle maturation and regeneration, combining stem cell differentiation, imaging, functional assays, and custom computational analysis. The lab is part of LIAN-FLENI and the Instituto de Neurociencias (INEU), and is supported by CONICET.
</p>

## Institutional Affiliations

{% include institutions-grid.html %}

## Location

<p>{{ site.location }}</p>

<div class="map-embed">
  <iframe
    src="https://www.google.com/maps?q=-34.33272440497676,-58.823616794202934&z=16&output=embed"
    loading="lazy"
    referrerpolicy="no-referrer-when-downgrade"
    allowfullscreen
    title="Map showing the Waisman Lab location">
  </iframe>
</div>

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
