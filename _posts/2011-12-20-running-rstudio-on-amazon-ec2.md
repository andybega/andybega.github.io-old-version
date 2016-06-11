---
layout: single
title: Running RStudio on Amazon EC2
date: 2011-12-20 08:51:54.000000000 +02:00
type: post
published: true
status: publish
categories:
- post
tags:
- EC2
- R
- RStudio
meta:
  _edit_last: '19821693'
  twitter_cards_summary_img_size: a:6:{i:0;i:500;i:1;i:338;i:2;i:3;i:3;s:24:"width="500"
    height="338"";s:4:"bits";i:8;s:4:"mime";s:9:"image/png";}
  _wpas_skip_4719251: '1'
  _wpas_skip_4719248: '1'
  _wpas_skip_4719261: '1'
---

For the most part I don't do things that are computationally so intensive that I can't run them on my work desktop. There have been a few times however where I ran simulations or bootstrapped models, and now Bayesian models with MCMC, that take a while to run. One solution has been to run things on [FSU's high performance computing cluster](http://www.hpc.fsu.edu/). It takes a little bit of effort, for someone without a background in computer science or programming like me, and it is inconvenient in several ways.

An alternative is to use Amazon's [EC2 cloud computing service](http://aws.amazon.com/ec2/). A few weeks ago I started playing around with it, and running basic instances for limited time is actually free. I use R/RStudio for the most part, but was overwhelmed by which AMI to use without having to instal R/RStudio. Fortunately someone has created AMI's (Amazon Machine Images) with RStudio Server, which, once running, lets you use RStudio through your web browser.

To begin, get an Amazon Web Services account and log in to the management console. [Louis Aslett](http://www.louisaslett.com/) has created a number of AMI's--[choose](http://www.louisaslett.com/RStudio_AMI/) one and start an instance on EC2 with that AMI id.

If you started the instance with the default security group settings like me, you will also have to open port 80 to get access. Go to the security group settings in Amazon management console, select whichever group your instance runs under (e.g. default), and add a custom TCP rule for port 80 (i.e. port range 80). Add the rule and apply. Find out your instance address (instances, at the bottom, it's the string that ends with amazonaws.com, e.g. `ec2-184-88-8-888.compute-1.amazonaws.com`), paste into your browser and you should get to a RStudio log in. The defaults are "rstudio" for both. And, there.

[![]({{ site.url }}/content/2011/rstudio-ec2.png)]({{ site.url }}/content/2011/rstudio-ec2.png)