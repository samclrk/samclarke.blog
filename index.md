---
---

{% assign indexable_posts = site.posts | where: "index",true %}

{% unless indexable_posts.size == 0 %}
## Latest
<ul>
{% for post in indexable_posts limit:5 %}
    <li>
      {{ post.date | date: "%d %b %Y" }} — <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
{% endfor %}
</ul>
{% endunless %}