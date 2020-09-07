--- 
---


I'm Sam, a Product Manager from the UK. For the last decade I've infrequently written about my life, technology, the books I'm reading and films I'm watching. I'm pro-cannabis and have more recently begun to write about my experiences with using it to manage anxiety and stress.

{% assign indexable_posts = site.posts | where: "index",true %}

{% unless indexable_posts.size == 0 %}
## Latest
<ul>
{% for post in indexable_posts limit:5 %}
    <li style="list-style-type: none; margin: 0; padding: 0;">
      {{ post.date | date: "%d %b %Y" }} — <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
{% endfor %}
</ul>
{% endunless %}