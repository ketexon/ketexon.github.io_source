---
layout: page
title: About
permalink: /about/
---
## Me
My name is Zane Clark and I go by the username Ketexon.

I am a <span id="age"></span> year old student who finds joy in academia and creativity.

## This website

This website is hosted on [Github pages]{:target="_blank"} ([website][website github]{:target="_blank"}, [source][website source]{:target="_blank"}).

This website is based around [Jekyll]{:target="_blank"} and the [Minima]{:target="_blank"} theme, but the styling has been entirely redone using [Bootstrap 5.0]{:target="_blank"} with [Material Icons]{:target="_blank"}.

This website serves several purposes
<ul class="list-group">
<li class="list-group-item">To act as a r&eacute;sum&eacute;</li>
<li class="list-group-item">To publish (and archive) compositions</li>
<li class="list-group-item">To publish (and archive) poetry and stories</li>
<li class="list-group-item">To describe myself</li>
<li class="list-group-item">To give a place to write about my intests</li>
<li class="list-group-item">To give a place to publish essays</li>
</ul>

[Github pages]:https://pages.github.com/
[website github]:https://github.com/ketexon/ketexon.github.io
[website source]:https://github.com/ketexon/ketexon.github.io_source

[Jekyll]:https://jekyllrb.com/
[Minima]:https://github.com/jekyll/minima
[Bootstrap 5.0]:https://getbootstrap.com/
[Material Icons]:https://fonts.google.com/icons?selected=Material+Icons

<script>
document.querySelector("#age").appendChild(
	document.createTextNode(
		Math.floor((Date.now() - new Date("01 August 2003").getTime())/1000/60/60/24/365)
	)
)
</script>