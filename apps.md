---
layout: default
permalink: /apps/
---

<div >

<a href="">
  <img src="http://is2.mzstatic.com/image/thumb/Purple71/v4/c7/73/c8/c773c833-79b9-db35-417a-27fb8feb788e/source.icns/100x100bb.png">
</a>
<h1>APNS Push</h1>
Test your iOS Push Notifications
</div>
<div>
    {% for app in data.apps %}
      <li>
        <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ app.title }}</a>
        <span class="post-meta">{{ post.date | date: "%b %-d, %Y" }}</span>
      </li>
    {% endfor %}


</div>

