---
sitemap: true
---

## Archive

---
layout: archive
---


<ul class="taxonomy__index">
  {% assign postsInYear = site.posts | where_exp: "item", "item.hidden != true" | group_by_exp: 'post', 'post.date | date: "%Y"' %}
  {% for year in postsInYear %}
    <li>
      <a href="#{{ year.name }}">
        <strong>{{ year.name }}</strong> <span class="taxonomy__count">{{ year.items | size }}</span>
      </a>
    </li>
  {% endfor %}
</ul>

{% assign entries_layout = page.entries_layout | default: 'list' %}
{% assign postsByYear = site.posts | where_exp: "item", "item.hidden != true" | group_by_exp: 'post', 'post.date | date: "%Y"' %}
{% for year in postsByYear %}
  <section id="{{ year.name }}" class="taxonomy__section">
    <h2 class="archive__subtitle">{{ year.name }}</h2>
    <div class="entries-{{ entries_layout }}">
      {% for post in year.items %}
        {% include archive-single.html type=entries_layout %}
      {% endfor %}
    </div>
    <a href="#page-title" class="back-to-top">{{ site.data.ui-text[site.locale].back_to_top | default: 'Back to Top' }} &uarr;</a>
  </section>
{% endfor %}



{% assign indexable_posts = site.posts | where: "index",true %}

{% unless indexable_posts.size > 0 %}
There aren't any posts here yet. Check back soon!
{% else %}
  {% for post in indexable_posts %}
  <div class='blogpost'>
    <div id='date'>
      <div id='day'>{{ post.date | date: "%-d" }}</div>
      <div id='month'>{{ post.date | date: "%b %Y" }}</div>
    </div>
    <div id='overview'>
      <div id='title'>{% include tags.html %}<a href="{{ post.url }}">{{ post.title }}</a></div>
      <div id='excerpt'>{{ post.excerpt | strip_html | truncatewords: 10 }}</div>
    </div>
  </div>
  {% endfor %}
{% endunless %}

<div style="text-align: center; margin-top: 6em;"><a href="/feed.xml" style="color: #EAECEF;">Atom/RSS</a></div>
