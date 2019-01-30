---
layout: page
title: Walkthroughs
permalink: /walkthroughs/
---
{% for post in site.pages reversed %}
<div class="row">
	<div>
		<li><a href="{{ post.url }}"><h3>{{ post.title }}</h3></a></li>
		<b><sub>{{ post.date | date: '%B %d, %Y' }}</sub></b>
	  	{{ post.excerpt }}
	</div>
</div>
{% endfor %}