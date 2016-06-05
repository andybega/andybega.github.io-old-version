
TODO:


```
[![tag]({{ site.url }}/assets/2015/foo.png)]({{ site.url }}/assets/2015/foo.png)

{% capture fig_img %}
[![tag]({{ site.url }}/assets/2015/foo.png)]({{ site.url }}/assets/2015/foo.png)
{% endcapture %}
{% capture fig_caption %}
Stairs? Were we're going we don't need no stairs.
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>{{ fig_caption | markdownify | remove: "<p>" | remove: "</p>" }}</figcaption>
</figure>
```

```
bundle exec jekyll serve --config _config.yml,_config.dev.yml
```
	
# Changes from template

Drop in booktabs tabley style from tufte CSS. To _tables.scss. 

Then have to rebuild CSS, see:

https://mmistakes.github.io/minimal-mistakes/docs/stylesheets/

MathJax

Added the script code to `_includes/scripts.html`:

```
<!-- MathJax support -->
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

```

Reduced default font size.



