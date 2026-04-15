---
layout: default
title: Shows
permalink: /shows/
---
<div class="page-content">

<h1>🎤 Shows</h1>

{% assign today = site.time | date: "%Y-%m-%d" %}
{% assign shows_sorted = site.data.shows | sort: "date" %}
{% assign upcoming = "" | split: "" %}
{% assign past = "" | split: "" %}
{% for show in shows_sorted %}
  {% assign show_date_str = show.date | date: "%Y-%m-%d" %}
  {% if show_date_str >= today %}
    {% assign upcoming = upcoming | push: show %}
  {% else %}
    {% assign past = past | push: show %}
  {% endif %}
{% endfor %}
{% assign past = past | reverse %}

{% if upcoming.size > 0 %}
<h2>Upcoming</h2>
<ul class="show-list">
{% for show in upcoming %}
    <li class="show">
        <div class="show-date">{{ show.date | date: "%a %b %-d, %Y" }}</div>
        <div class="show-main">
            <div class="show-venue">{{ show.venue }}</div>
            <div class="show-city">{{ show.city }}</div>
            {% if show.notes %}<div class="show-notes">{{ show.notes }}</div>{% endif %}
        </div>
        {% if show.tickets %}
        <a class="show-tickets" href="{{ show.tickets }}" target="_blank" rel="noopener">🎟 Tickets</a>
        {% endif %}
    </li>
{% endfor %}
</ul>
{% else %}
<p style="text-align: center; opacity: 0.7;"><em>No shows on the books right now — check back soon.</em></p>
{% endif %}

{% if past.size > 0 %}
<h2>Past Shows</h2>
<ul class="show-list past">
{% for show in past %}
    <li class="show">
        <div class="show-date">{{ show.date | date: "%b %-d, %Y" }}</div>
        <div class="show-main">
            <div class="show-venue">{{ show.venue }}</div>
            <div class="show-city">{{ show.city }}</div>
            {% if show.notes %}<div class="show-notes">{{ show.notes }}</div>{% endif %}
        </div>
    </li>
{% endfor %}
</ul>
{% endif %}

</div>
