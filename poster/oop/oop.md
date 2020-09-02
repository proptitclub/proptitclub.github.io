---
layout: categorical
title: About
categorical: oop
order : 1
---
# oop-list post

---

<h2>{{ site.data.oop.docs_list_title }}</h2>
<ul>
   {% for item in site.data.oop.docs %}
      <li><a href="{{site.urlsite}}/poster/{{page.categorical}}/{{ item.url }}">{{ item.title }}</a></li>
   {% endfor %}
</ul>



