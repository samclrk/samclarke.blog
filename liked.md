---
published: true
---


<ul id="feed-app" class="archive-list">
</ul>


<script>
const app = document.querySelector('#feed-app');
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
        <li>
         <a href="${el.querySelector("link").innerHTML}" target="_blank" rel="noopener">
            <strong>
              ${el.querySelector("title").innerHTML}
            </strong>
            </a>
          ${url.hostname.replace('www.', '')}
        </li>
      `;
    });
    app.insertAdjacentHTML("beforeend", html);
  });
</script>