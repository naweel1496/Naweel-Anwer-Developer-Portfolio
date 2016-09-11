---
layout: default
permalink: /apps/
---
<div class="my-apps">
  <header>My Apps</header>
  {% for app in site.data.apps %}
  <section style="text-align:{% cycle 'left', 'right' %}" >
    <img src="{{ app.image }}">
    <h2>{{ app.name }}</h2>
    <p class="sub-title">{{ app.subtitle }}</p>
    <summary>{{ app.description }}</summary>
    <p><a href="{{app.appstore_url}}">View in Mac App Store</a></p>
  </section>
  {% endfor %}
</div>
