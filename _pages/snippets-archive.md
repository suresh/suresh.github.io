---
title: ML Notes
layout: collection
permalink: /snippets/
collection: snippets
entries_layout: list
classes: wide
---

Here is a collection  of snippets that are useful while doing data, python or machine learning projects.

### AWS
<table cellspacing="0" class="archive-table book-archive">
  {% assign snippets = site.snippets | sort: 'last_modified_at' | reverse %}
  {% for snip in snippets %}
    {% if snip.tags == "sklearn" %}
    <tr class="{% cycle 'even', 'odd' %}">
      <td class="title">
        {{snip.title}}
      </td>
      <td >{{ snip.excerpt }}</td>
    </tr>
    {% endif %}
  {% endfor %}
  </table>
