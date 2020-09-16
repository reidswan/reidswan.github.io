---
layout: page
title: Projects
permalink: /projects/
---

{% for page in site.pages %}
    {% if page.categories contains "project_page" %}
## [{{page.title}}]({{page.url}})
{{page.blurb}}
    {% endif %}
{% endfor %}
