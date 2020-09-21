---
published: true
---


<div class="feed-app">
</div>


<script>
const app = document.querySelector('.feed-app');
const PROXY_URL = 'https://cors-anywhere.herokuapp.com/';
const RSS_URL = 'https://feedbin.com/starred/a32b5165f939eb1ebb0f25d0f88b3f67.xml';
fetch(PROXY_URL + RSS_URL)
  .then(response => response.text())
  .then(str => new window.DOMParser().parseFromString(str, "text/xml"))
  .then(data => {

    const items = data.querySelectorAll("item");
    let html = ``;
    items.forEach(el => {
      var url = new URL(el.querySelector('link').innerHTML);

      html += `
          <div class='blogpost' style="grid-template-columns: none !important;">
          <div id='date'>
            <div id='day'>{{ post.date | date: "%-d" }}</div>
            <div id='month'>{{ post.date | date: "%b %Y" }}</div>
          </div>
           <div id='overview'>
            <div id='title'><a href="${el.querySelector("link").innerHTML}" target="_blank" rel="noopener">${el.querySelector("title").textContent}</a></div>
            <div id='excerpt'>${url.hostname.replace('www.', '')}</div>
            </div>
          </div>
      `;
    });
    app.insertAdjacentHTML("beforeend", html);
  });
</script>

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