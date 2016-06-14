---
layout: single
title: Moving from Wordpress to Jekyll
category: meta
tags: [wordpress, jekyll, traffic]
---

I moved my home page and blog from Wordpress to Jekyll over the past week, thanks to a small break in regular work. I've been using Wordpress.com since 2011, when I started blogging. I don't remember what led me back then to chose Wordpress, but overall, I haven't been and wasn't unhappy with it. It's easy to set up, and at some point it became possible to write posts in Markdown. Comments work out of the box. Some traffic stats are baked in. 

Two minor things that bothered me were that the editor would mangle posts when switching between the visual and text editors, and that it was always a bit clunky to work with figures and other media. You can just drag and drop them to a media upload page, which by itself is fine, but it is kind of clunky to update existing figures in a way that doesn't change their internal file names. At least it was for me. 

I noticed that some people have been using pages made with Jekyll and similar static page generators. My general sense of the selling points for Jekyll and similar projects like Pelican was that the static sites they create load faster and are more secure. They are not written in PHP. And I guess there's an appeal from figuring out the small-ish technical aspects of getting a blog running with them. 

- I like the minimalistic styling of the blogs Jekyll and Pelican create. 
- I like the idea of having control over all the content. Having a folder on my laptop that contains all the posts and content, rather than interacting with them through a web editor. 

I'm using a slightly modified version of the [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/) theme by Michael Rosen. He's set a set of really nice and clear instructions to get started and between that and a variety of tutorials for getting set up with Jekyll that one can find via google, I didn't have any major issues in exporting posts from Wordpress.com, setting up the theme, adding Disqus comments, hosting it on GitHub Pages, and switching my domain name registrar. There was a bit of manual work cleaning up and formatting the posts, but I don't have that many posts anyways. 

Beyond the documentation that comes with the Minimal Mistakes theme, Rose has the source code for both the theme and the documentation, including the sample posts, on GitHub. The theme itself is on the master branch, the documentation and sample posts on another branch. 

I found these guides to be helpful in particular:

- http://mattdickenson.com/2016/02/29/moving-from-wordpress-to-jeykll/
- http://www.girliemac.com/blog/2013/12/27/wordpress-to-jekyll/
- http://www.leemunroe.com/moving-wordpress-dreamhost-to-jekyll-github/
- http://michaeljdeeb.com/blog/using-a-custom-domain-with-github-pages/

The three main changes I made to the theme were to reduce the default font size (which was too big for me), change the table styling to Tufte style tables, and adding support for math formulas using MathJax. 

The theme style is controlled by a couple of Sass files. To make the default font smaller I found and changed the relevant variable in _variables.scss. 

As the [documentation explains](https://mmistakes.github.io/minimal-mistakes/docs/stylesheets/), changes in the SCSS files require regenerating the CSS style files. Doing the required installs and rebuilding the files went without problems for me, once I found that I had to do this (I don't know anything about SASS, Ruby).  

To make it possible to include Latex style math in posts I added a pointer to the MathJax scripts in the header templace in `_includes/head.html`, as recommended in the MathJax documentation. 

That worked without problems until it didn't. When I tested the posts that had formulas in them locally, the math displayed fine. But on GitHub Pages some would show up, some wouldn't. In the end, the problem was that on GitHub pages, the hmtl files get compressed into wonderful one-liners without any white space or line breaks. Locally they were still nicely formatted, which is why the equations were displaying locally but not on GitHub Pages. Wrapping the equations in `<p></p>` tags fixed the problem. 

There are two more things I want to do:

- Check and fix broken links. 
- Move all content to the blog.

I should probably work on actually posting things again as well. And working on the handful of *bona fide* academic projects I still have hanging in the air. 

## What people have been looking at

Moving to Jekyll/GitHub Pages and Google Analytics for statistics breaks continuity in those. So I guess this is a good time to look back at what people are coming to this blog for. It seems that other bloggers like to do these kinds of post at the end of the year, but I'll use this structural break as an opportunity instead. 

| Year | Posts |
|------|-------|
| 2011 | 9 |
| 2012 | 6 |
| 2013 | 10 |
| 2014 | 7 |
| 2015 | 5 |
| 2016 | 2 |

I started blogging at a crawling pace back in 2011, and I've stayed at a crawling pace since then, with a new post every 2 months or so at best. A lot of the early posts were dumping older data and notes from my graduate school days, like the [Stata do files for converting country names to codes]({ post.url 2013-09-05-stata-do-files-for-country-code-conversions }). This was also when I started learning R, and later, in 2013, SQL, so there were some posts related to R and mapping. Although the posts have become rarer in the past two years, I think they have been more substantial and self-contained.  

[![Visits per year]({{ site.url }}/content/2016/visits-per-year.png){: .align-center width="500px"}]({{ site.url }}/content/2016/visits-per-year.png)

[![Visits last months]({{ site.url }}/content/2016/visits-last-months.png){: .align-center width="500px"}]({{ site.url }}/content/2016/visits-last-months.png)

Looking at traffic, I had 1 or 2 thousand page views in the first year, which grew to 15 thousand in 2015. These days I get about a 1,000 views per month, although who knows how switching to Jekyll will impact that. That's not a lot, but a lot more than the few hundred views/visitors my self-written page got back in my early to mid grad student days. 

[![Visits per year]({{ site.url }}/content/2016/top-posts.png){: .align-center width="400px"}]({{ site.url }}/content/2016/top-posts.png)

The majority of visitors come for the Stata country conversion do files and for how to put north arrows and scales on R maps. Those posts have been up since 2012 and 2013, and I had the Stata do files on my web site before then, so I think there are some habitual users of these. I'm glad that three of the posts from 2015 are showing up in the top list (these are the ones marked with orange). 
