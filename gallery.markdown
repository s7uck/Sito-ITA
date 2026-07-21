---
layout: default
title: Foto
permalink: /gallery
---

<style>
	body { max-width: unset;}
	#photo-grid>section { padding: 0; gap: 0; flex-wrap: nowrap;}
	section>img, section>table { height:100%;}
</style>

<header class="hero">
	<h1 class="hero">foto</h1>
	{% include nav.html ani="yes" %}
</header>

{% assign photos = site.pages | where_exp: "item", "item.dir contains '/photos/'" | sort: "date" | reverse %}

<main class="wide gridlock ani" id="photo-grid">{% for photo in photos %}
	<section{% if photo.rating >= 4 %} class="big"{% endif %} onclick="window.location = '{{ photo.url }}'" title="{{ photo.filename }}">
		<img src="{{ photo.image }}" alt="{{ photo.title | default: photo.filename }}">

		<figcaption>
			<table>{% if photo.title %}
				<tr><th><big>{{ photo.title }}</big></th></tr>{% endif %}
				<tr>{% if photo.camera %}
					<td class="ily"><img class="icon" src="/images/camera.svg" alt="Camera">
						{{ photo.camera }}
					</td>{% endif %}{% if photo.location %}
					<td class="ily"><img class="icon" src="/images/location.svg" alt="Location">
						{{ photo.location }}
					</td>{% endif %}
					<td class="timestamp"><time>{{ photo.date | date: "%-d %B %Y %H:%M" }}</time></td>
				</tr>
			</table>
		</figcaption>
	</section>{% endfor %}
</main>
