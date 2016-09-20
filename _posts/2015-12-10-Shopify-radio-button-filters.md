---
layout: post
title:  Replacing a Shopify Collection drop-down filter with radio buttons
date: 2015-12-10
image: images/@stock/blog-9.jpg
excerpt:
  Nisi quas minima cumque et voluptate. et et iure nostrum necessitatibus et ipsam sed doloribus ab odio. voluptates velit et quaerat qui
categories:
      - Web Design
      - Shopify
tags: Shopify, filters, How to
author: Erik
published: true
permalink: /blog/Replacing-Shopify-Collection-drop-down-filters-with-radio-buttons
---


A client's site used a drop-down menu to filter their product tags but wanted a more customized solution. The radio button filter that I implemented offers a better user experience and aesthetic.

<p></p>

<strong>The page with the drop-down filter originally looked like this:</strong>
{:.center}
![]({{ site.baseurl }}/img/jewelry-dropdown.jpg)
<p></p>
<strong>And with radio buttons, the filtering looked like [this](http://www.supermarkethq.com/collections/jewelry):</strong>
{:.center}
![]({{ site.baseurl }}/img/jewelry-radio.jpg)

The original implementation used the drop-down menu to display all product tags available and when a user selected a tag, jQuery was used to add that tag to the url handle using 'window.location.href'. That reloads the page with the tag filter. As an example, the url would look like this if the "rings" tag is selected: www.supermarkethq.com/collections/jewelry/rings
To learn more about how Shopify filters work, see this [post](http://eriksilver.github.io/blog/How-to-work-with-Shopify-Collection-Filters-and-their-limitations).

####How to filter with radio buttons
The radio button implementation is more complex and includes additional elements:

* Custom tags assigned to the radio buttons for each collection. This is also a way to subcategorize a collection, instead of showing all tags for all products.

* Refactor the CSS selector to an 'input' and add additional CSS classes for the radio buttons.

* Add logic to check if a radio button is selected; only one can be selected at a time.

<strong>Here is a look at the final radio button code:</strong>
{% gist 57acc1a8330a8d8dff50%}

What questions do you have about Shopify collection and product filters?

Contact me [here](http://eriksilver.github.io/contact) to chat about your project needs.   
