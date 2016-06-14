
```
bundle exec jekyll serve --config _config.yml,_config.dev.yml --drafts
```

TODO:

- check for broken links
- move all papers from DB to GHP
- post on wordpress moving to new blog


```
[![tag]({{ site.url }}/assets/2015/foo.png){: .align-center}]({{ site.url }}/assets/2015/foo.png)

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

Linking to other posts. Use raw file names.
```
{% post_url 2010-07-21-name-of-post %}

{% post_url /subdir/2010-07-21-name-of-post %}

[Name of Link]({% post_url 2010-07-21-name-of-post %})
```

# Changes from template

Drop in booktabs tabley style from tufte CSS. To _tables.scss. 

Then have to rebuild CSS, see:

https://mmistakes.github.io/minimal-mistakes/docs/stylesheets/

MathJax

Added the script code to header.

```
<!-- MathJax support -->
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

```

Github pages is not showing MathJax with environments. They are rendering properly locally, but not on GHP. Problem was html compression, which removed line breaks. Had to wrap in paragraphs. Removed html compression anyways.

Reduced default font size.



