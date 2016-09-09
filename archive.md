---
layout: page
title: 
permalink: /archive/
---
<article>

<!-- from http://www.mitsake.net/2012/04/archives-in-jekyll/ -->

{% for post in site.posts %}
{% capture this_year %}{{ post.date | date: "%Y" }}{% endcapture %}
    {% capture this_month %}{{ post.date | date: "%B" }}{% endcapture %}
    {% capture next_year %}{{ post.previous.date | date: "%Y" }}{% endcapture %}
    {% capture next_month %}{{ post.previous.date | date: "%B" }}{% endcapture %}
  
    {% if forloop.first %}
      <h1>{{this_year}}</h1>
      <h2>{{this_month}}</h2>
      <ul>
    {% endif %}
  
    <li><span>{{ post.date | date: "%B %e, %Y" }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  
    {% if forloop.last %}
      </ul>
    {% else %}
      {% if this_year != next_year %}
        </ul>
        <h1>{{next_year}}</h1>
        <h2>{{next_month}}</h2>
        <ul>
      {% else %}    
        {% if this_month != next_month %}
          </ul>
          <h2>{{next_month}}</h2>
          <ul>
        {% endif %}
      {% endif %}
    {% endif %}
  {% endfor %}

