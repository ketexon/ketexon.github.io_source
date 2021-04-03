---
layout: page
title: About
permalink: /about/
---
## Contact
Please contact me through either of these emails.

{% if site.author.email -%}
	<div class="row">
		<div class="col-auto">
			{% for email in site.author.email %}
				<div class="row mt-1">
					<a class="u-email link-primary" href="mailto:{{ email }}">
						{{ email }}
					</a>
				</div>
			{% endfor %}
		</div>
		<div class="col-auto">
			{% for email in site.author.email %}
				<div class="row mt-1">
					<button type="button" class="u-email-copy btn btn-sm btn-secondary py-0"
						onmouseup="navigator.clipboard.writeText('{{ email }}'); setTimeout(()=>this.blur(), 100)"
						data-bs-toggle="tooltip" data-bs-placement="top" title="Copied to clipboard">
						<span class="material-icons">content_copy</span>
					</button>
				</div>
			{% endfor %}
		</div>
	</div>
	
{%- endif %}



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

## Copyright and Licensing

All musical compositions and poems are licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/" target="_blank">Creative Commons Attribution-NonCommercial 4.0 International License</a>. <img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc/4.0/80x15.png" /> Said simply, you can use the works in any manner that you please as long as it is not commercial. If you wish to use it commercially, contact me.

This audio files are licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/" target="_blank">Creative Commons Attribution 4.0 International License</a>. <img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/80x15.png" />

The website itself, with the exception of the already-licensed works therein, is licensed under the [MIT License]. 

[Github pages]:https://pages.github.com/
[website github]:https://github.com/ketexon/ketexon.github.io
[website source]:https://github.com/ketexon/ketexon.github.io_source

[Jekyll]:https://jekyllrb.com/
[Minima]:https://github.com/jekyll/minima
[Bootstrap 5.0]:https://getbootstrap.com/
[Material Icons]:https://fonts.google.com/icons?selected=Material+Icons

[MIT License]:/license/

<script>
document.querySelector("#age").appendChild(
	document.createTextNode(
		Math.floor((Date.now() - new Date("01 August 2003").getTime())/1000/60/60/24/365)
	)
)
</script>