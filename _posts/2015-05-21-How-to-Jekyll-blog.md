---
layout: post
title: How to Create a Jekyll Blog with Poole (or Type Theme)
date: 2015-05-21
image: images/@stock/blog-9.jpg
excerpt:
  Nisi quas minima cumque et voluptate. et et iure nostrum necessitatibus et ipsam sed doloribus ab odio. voluptates velit et quaerat qui
categories:
    - Web Design
tags: Jekyll, Blog
author: Erik
---


### Update October 2015
I wanted a portfolio site in addition to a blog, so I found a new Jekyll theme to replace my original blog based on the [Poole](https://github.com/poole/poole) theme. Then I extended the Kami theme further and made my own customizations like the full blog page.

>The ease of modifying and extending a theme as well as the simple static site hosting are two of the beauties of using Jekyll.

### What is Jekyll, anyway?
Jekyll is a site generator for blogs that uses static (read: text) files. It will take a directory of text files and run them through 1) a converter (e.g. Markdown) and 2) a Liquid renderer and spit out a ready to publish website.

### What is Poole?
Poole calls itself a "diligent and noble steward" for building Jekyll sites, aka the "Jekyll Butler." It is designed to make a clear setup path for a Jekyll site by providing a full plain Jekyll install with some examples pages, posts, templates, etc to get you up and running fast.

It also has two design themes available Hyde and Lanyon (used on this site).

### Super Fast Setup
* Go to the local directory for your new blog.
* Copy the Poole repository from [Github](https://github.com/poole/poole)
* Clone the repository: <code>$ git clone https://github.com/poole/poole</code>

* This will create a 'poole' directory with all the files in it
* User this Jekyll command to run locally in the browser: <code>$ jekyll serve</code>

More details on [setup and installation](https://github.com/poole/poole) are on Github.

### Customizations
Archive Page
I like some of the customizations done by by [Joshua Lande](http://joshualande.com/jekyll-github-pages-poole/), like the Archive page. So I wanted to set one up on my Poole blog.
To do this, I created an 'archive.md' file and saved it in the blog directory.

### Summary
I found this faster and prettier than working through the setup instructions from [Jekyll](www.jekyllrb.com).
Also, I liked starting with theme that already incorporates some design, and the theme code and design is totally customizable.
