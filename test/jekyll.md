---
layout: default
title: Jekyll Test
custom_front: matter
---

## Site:
**site.time** : {{ site.time | date_to_xmlschema }}
**site.pages** : {{ site.pages | inspect }}
**site.html_pages** : {{ site.html_pages | inspect }}
**site.pages** -> 
{% for page in site.pages %}
    **name** : {{ page.name }}
    **path** : {{ page.path }}
    **url** : {{ page.url }}
    **title** : {{ page.title }}
{% endfor %}
**site.posts** : {{ site.posts | inspect }}
**site.static_files** : TOO LONG TO DISPLAY (of github info)
**site.html_files** : {{ site.html_files | inspect }}
**site.collections** : {{ site.collections | inspect }}

## This Page:
**page.name** : {{ page.name }}
**page.path** : {{ page.path }}
**page.url** : {{ page.url }}
**page.title** : {{ page.title }}
**page.date** : {{ page.date | date_to_xmlschema }}
**page.custom_front** : {{ page.custom_front }}
