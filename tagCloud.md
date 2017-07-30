---
layout: page
title: Tag Cloud
---

<div>
{% assign sorted_tags = (site.tags | sort: 0) %}
{% for tag in sorted_tags %}
 <div>
    <a class="action-button shadow animate green" href="/tags/{{ tag[0] }}" style="font-size: {{ tag | last | size | times: 400 | divided_by: site.tags.size | plus: 35  }}%" draggable="false">
     {{ tag | first }} <small>({{ tag | last | size }})</small>
    </a>
</div>
{% endfor %}
</div>