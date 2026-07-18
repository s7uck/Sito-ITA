---
layout: default
title: Foto
permalink: /gallery
---

<style>
	body { max-width: unset;}
	section { padding: 0; gap: 0; flex-wrap: nowrap;}
	section>img, table { height:100%;}
	.timestamp, time { color: yellowgreen; text-align: right;}
	td .icon { position: absolute; z-index: -10; opacity: .5; top: 0.2em; left: 0.2em;}
</style>

<header class="hero">
	<h1>foto</h1>
	{% include nav.html ani="yes" %}
</header>

{% assign photos = site.pages | where_exp: "item", "item.dir contains '/photos/'" | sort: "date" | reverse %}

<main class="wide gridlock ani" id="photo-grid">{% for photo in photos %}
	<section{% if photo.rating >= 4 %} class="big"{% endif %} onclick="window.location = '{{ photo.url }}'" title="{{ photo.filename }}">
		<img src="{{ photo.image }}" alt="{{ photo.title | default: photo.filename }}">

		<figcaption>
			<table>{% if photo.title != '' %}
				<tr><th><big>{{ photo.title }}</big></th></tr>{% endif %}
				<tr>{% if photo.camera != '' %}
					<td><img class="icon" src="/images/camera.svg" alt="Camera">
						{{ photo.camera }}
					</td>{% endif %}{% if photo.location != '' %}
					<td><img class="icon" src="/images/location.svg" alt="Location">
						{{ photo.location }}
					</td>{% endif %}
					<td class="timestamp"><time>{{ photo.date | date: "%-d %B %Y %H:%M" }}</time></td>
				</tr>
			</table>
		</figcaption>
	</section>{% endfor %}
</main>
