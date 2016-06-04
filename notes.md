
TODO:

	- figure out slugs, ideally to maintain old WP links
	- migrate domain name from WP to my own
	- homepage + blog or just blog?

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
