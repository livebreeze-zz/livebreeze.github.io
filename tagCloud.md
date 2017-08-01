---
layout: page
title: Tag Cloud
---

<table>
    <tr>
        <td>
            <div class="blog-tags"> 
                {% assign tags = site.tags | sort %}
                {% for tag in tags %}
                <a href="#{{ tag[0] | slugify }}" class="action-button shadow animate green" style="font-size: {{ tag | last | size  |  times: 400 | divided_by: site.tags.size | plus: 35  }}%"> 
                    {{ tag | first }} <small>({{ tag | last | size }})</small>
                </a>
                {% endfor %}
            </div>
        </td>
    </tr>
</table>
<div class="post-preview"> 
{% for tag in tags %} 
    <h2 id="{{ tag[0] | slugify }}" style="padding-top: 70px;"> {{ tag[0] }}  <small>(<i class="badge">{{ tag | last | size }}</i>)</small></h2>
    <ul class="later on">
    {% for post in tag[1] %}
        <a class="post-link" href="{{ site.baseurl }}{{ post.url }}">
    <li>
        {{ post.title }}
    <small class="post-meta"> - Posted on {{ post.date | date: "%B %-d, %Y" }}</small>
    </li>
    </a>
    {% endfor %}
    </ul>
    <a href="#top" class="action-button shadow animate yellow" style="padding:2px 15px; font-size:11px">
        <span class="fa fa-refresh" aria-hidden="true"></span> Go back to the top
    </a> 
{% endfor %}
</div>