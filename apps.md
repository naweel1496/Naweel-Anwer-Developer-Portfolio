---
layout: default
permalink: /apps/
---
<div class="my-apps">
  <h1>My Apps</h1>
  {% for app in site.data.apps %}
  <section style="text-align:{% cycle 'left', 'right' %}" >
    <img src="{{ app.image }}">
    <h2>{{ app.name }}</h2>
    <p class="sub-title">{{ app.subtitle }}</p>
    <summary>{{ app.description }}</summary>
    <p class="mac-store">
      <a href="{{app.appstore_url}}">
        <span>{% include icons/app-store.svg %}</span>View in Mac App Store
      </a>
    </p>
  </section>
  {% endfor %}
</div>
