---
layout: default
title: Jekyll Test
custom_front: matter
---

site.time : {{ site.time | date_to_xmlschema }}
site.pages : {{ site.pages | inspect }}
site.posts : {{ site.posts | inspect }}
site.static_files : {{ site.static_files | inspect }}
site.html_pages : {{ site.html_pages | inspect }}
site.html_files : {{ site.html_files | inspect }}
site.collections : {{ site.collections | inspect }}

page.path : {{ page.path }}
page.url : {{ page.url }}
page.name : {{ page.name }}
page.title : {{ page.title }}
page.date : {{ page.date | date_to_xmlschema }}

page.custom_front : {{ page.custom_front }}
