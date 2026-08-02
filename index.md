---
layout: page
title: Home
permalink: /
feature_text: |
  The Derby Lightweight Preservation Group
feature_image:
---

The Derby Lightweight Preservation Group is working to preserve the only surviving Derby Lightweight 2-car set, 79612 & 79018.

This website will document the train, the restoration work and the people supporting it. 

## Current restoration status

{% assign restoration = site.data.restoration %}

**{{ restoration.status }} — {{ restoration.current_phase }}**

{{ restoration.summary }}

_Last updated: {{ restoration.last_updated | date: "%e %B %Y" | strip }}_

### Work in progress

{% for task in restoration.current_tasks %}
- {{ task }}
{% endfor %}

[Read the full restoration summary]({{ '/restoration/' | relative_url }}).

## Latest updates

{% if site.posts.size > 0 %}
{% for post in site.posts limit: 3 %}
### [{{ post.title }}]({{ post.url | relative_url }})

_{{ post.date | date: "%e %B %Y" | strip }}_

{{ post.summary | default: post.excerpt }}
{% endfor %}

[Browse all project updates]({{ '/updates/' | relative_url }}).
{% else %}
No updates have been published yet. [TO BE CONFIRMED: add the first project update.]
{% endif %}

## Support the project

The project welcomes practical help, specialist knowledge, materials, historical information and financial support. [Find out how you can support the group]({{ '/support-us/' | relative_url }}) or [contact the group]({{ '/contact/' | relative_url }}).
