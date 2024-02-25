---
layout: page
permalink: /repositories/
title: repositories
description: A collection of my repositories on GitHub, for detailed information on a specifc project view my 'projects' tab.
nav: true
nav_order: 4
---
## GitHub Repositories

{% if site.data.repositories.github_repos %}

<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
  {% for repo in site.data.repositories.github_repos %}
    {% include repository/repo.liquid repository=repo %}
  {% endfor %}
</div>
{% endif %}
