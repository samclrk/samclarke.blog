---
published: true
---


<ul id="feed-app" class="archive-list">
</ul>

<script>
const app = document.querySelector('.post-feed-liked');
const PROXY_URL = 'https://cors-anywhere.herokuapp.com/';
const RSS_URL = 'https://feedbin.com/starred/a32b5165f939eb1ebb0f25d0f88b3f67.xml';

  var count = 0;

fetch(PROXY_URL + RSS_URL)
  .then(response => response.text())
  .then(str => new window.DOMParser().parseFromString(str, "text/xml"))
  .then(data => {

    const items = data.querySelectorAll("item");
    let html = `<h2 class="featured-title kg-width-normal" style="margin-top:4rem; margin-bottom: none;!important">What I've been reading</h2>`;
    items.forEach(el => {
      var url = new URL(el.querySelector('link').innerHTML);
      count += 1;
       if (count > 4) {
        return false;
    }
    else if (count == 4) {
        // DO nothing
    }
    else {
      html += `
		<article class="feed post liked-article">
  <div class="feed-calendar">
  </div>
  <h2 class="feed-title">${el.querySelector("title").innerHTML}</h2>
  <div class="feed-right">
    <svg class="icon feed-visibility feed-visibility-public"><use xlink:href="#star"></use></svg>
    <div class="feed-length">
      ${url.hostname.replace('www.', '')}
    </div>
  </div>
  <svg class="icon feed-icon"><use xlink:href="#chevron-right"></use></svg>
  <a class="u-permalink" href="${el.querySelector("link").innerHTML}"></a>
   
</article>
      `;
     }
    });
   
    app.insertAdjacentHTML("beforeend", html);
  });
  
  console.log(html)

</script>