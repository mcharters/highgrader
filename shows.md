---
layout: default
title: Shows
permalink: /shows/
---
<div class="page-content">

<h1>🎤 Shows</h1>

{% comment %}
  Past vs. upcoming is decided in the browser (see script below) using the
  visitor's real current date. We can't rely on Liquid's site.time here: on a
  static GitHub Pages site that value is frozen at the last build, so shows
  would never move to "Past" until the next push/rebuild. We render every show
  with a machine-readable data-date and let JS sort them at view time.
{% endcomment %}
{% assign shows_sorted = site.data.shows | sort: "date" %}

<h2 class="shows-heading" data-section="upcoming">Upcoming</h2>
<ul class="show-list upcoming"></ul>
<p class="shows-empty" hidden><em>No shows on the books right now — check back soon.</em></p>

<h2 class="shows-heading" data-section="past" hidden>Past Shows</h2>
<ul class="show-list past"></ul>

<template id="shows-data">
{% for show in shows_sorted %}
    <li class="show" data-date="{{ show.date | date: "%Y-%m-%d" }}">
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
</template>

<script>
(function () {
    // Local "today" as YYYY-MM-DD so string comparison matches data-date.
    var now = new Date();
    var today = now.getFullYear() + '-' +
        String(now.getMonth() + 1).padStart(2, '0') + '-' +
        String(now.getDate()).padStart(2, '0');

    var shows = Array.prototype.slice.call(
        document.getElementById('shows-data').content.querySelectorAll('.show')
    );

    var upcomingList = document.querySelector('.show-list.upcoming');
    var pastList = document.querySelector('.show-list.past');
    var upcomingHeading = document.querySelector('.shows-heading[data-section="upcoming"]');
    var pastHeading = document.querySelector('.shows-heading[data-section="past"]');
    var emptyMsg = document.querySelector('.shows-empty');

    var upcomingCount = 0, pastCount = 0;

    shows.forEach(function (show) {
        var node = show.cloneNode(true);
        if (show.getAttribute('data-date') >= today) {
            upcomingList.appendChild(node);
            upcomingCount++;
        } else {
            // Past shows read newest-first.
            pastList.insertBefore(node, pastList.firstChild);
            pastCount++;
        }
    });

    if (upcomingCount === 0) {
        upcomingHeading.hidden = true;
        emptyMsg.hidden = false;
    }
    if (pastCount > 0) {
        pastHeading.hidden = false;
    }
})();
</script>

</div>
