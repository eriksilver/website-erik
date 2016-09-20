---
layout: post
title:  How to serve static files with Node and Express, without a templating engine
date: 2015-10-20
image: images/@stock/blog-9.jpg
excerpt:
  Nisi quas minima cumque et voluptate. et et iure nostrum necessitatibus et ipsam sed doloribus ab odio. voluptates velit et quaerat qui
categories:
      - Web Design
tags: Node, Express, MEAN Stack, How to
author: Erik
published: true
permalink: /blog/How-to-serve-static-files-with-Node-and-Express-without-a-templating-engine
---

This example uses Node + Express to serve static files for an Angular app, without using
an Express templating engine.

Some examples for setting up an Express server with a Node app, include
the use of Jade as a templating engine. This is app does not use a templating engine and I didn't want to add one. I had my views as plain html files.

I found it hard to find an example of the simple case of a single page application, an Angular app, find a good example of setting up Express.

So I pieced together clues from Stack Overflow and looked at the Express API directly to
put together a simple server setup for this Angular app, a single page application.

One tricky part was figuring out the res.sendFile and getting the file directly and entry point file properly identified. The entry point for this app is the index.html; that is the only page the server points to and then Angular handles the routing.

I had to restructure my files, that is, get the right files in the public directory.
Here is what the files structure looks like:

{:.center}
![Angular App file structure]({{ site.baseurl }}/img/gaApp-files.jpg)

Here is my final server.js file, with comments.

{% highlight js %}
//Use/'require' the Node module 'Express'
var express = require('express');
//Define variable app to use methods of the Express function
var app = express();
//express.static is built-in middleware to server static files, 'public' is the name of the directory
//that holds the files to published
app.use(express.static('public'));
//define a port
var port = 8000;
//the listen method binds and listens for connections on the specified host and port
//using just "port" will work locally; but to deploy on Heroku, I had to use
//"process.env.PORT || 8000" because Heroku will set the port randomly
app.listen(process.env.PORT || 8000, function() {
    console.log('app listening on port ' + port);
});
//Routes HTTP GET requests to the specified path with the specified callback functions
//here '*' is the path we want to get, which is a catch-all route
//since we have a single page application (SPA) architecture, we are using Angular
//to do the routing and we just need the Express server to have a single entry point into the
//application, which is through the index.html file
app.get('*', function(req, res) {
    //__dirname is a special word to access the local file + public/index.html is the
    //directory for the published files
    //the sendFile method transfers the file that is the single point of entry
    //Transfers the file at the given path.
    res.sendFile(__dirname + "/public/index.html");
});
{% endhighlight js %}

How do you serve your apps with Node and Express?
