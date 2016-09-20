---
layout: post
title:  How to deploy an app from scratch with Heroku, using Node and Express
date: 2016-1-5
image: images/@stock/blog-9.jpg
excerpt:
  Nisi quas minima cumque et voluptate. et et iure nostrum necessitatibus et ipsam sed doloribus ab odio. voluptates velit et quaerat qui
categories:
      - Web Design
tags: Node, Express, Heroku, deployment, MEAN Stack, How to
author: Erik
published: true
permalink: /blog/How-to-deploy-an-app-from-scratch-with-Heroku-using-Node-and-Express
---

This post shares the steps to take an application and deploy it as a web application with Heroku. It details the files and steps required for Heroku and Express to launch the app.

In a previous [post](http://eriksilver.github.io/blog/How-to-serve-static-files-with-Node-and-Express-without-a-templating-engine/), I shared a detailed example of how to setup Express with Node.js to serve an application.

These are the these steps I used to publish an Angular app, the Event Management System. A link to the full Github repo is at the bottom.

1. If your using Git for your project, make a new branch:<br>
`git checkout -b new_branch_name`

2. Create a Procfile in the project root directory. Heroku will look for a Procfile to deploy the app.The contents of the Procfile is one line: web:  `node server.js`<br>
`touch Procfile`

3. Create a server.js file in the project root directory. This file will use Express to setup the server. In my Node + Express [post](http://eriksilver.github.io/blog/How-to-serve-static-files-with-Node-and-Express-without-a-templating-engine/), I go into detail about setting up the server.js file.<br>
`touch server.js`

4. Create a package.json file which Node.js (npm) uses to identify the project and specifies how to handle the projects dependencies. Heroku will look for a package.json file as well to build the deployment.<br>
`npm init`

5. Install Express, which is web framework for Node.js that will help setup the server. The '--save' flag will save Express as dependency for the application in the package.json file.<br>
`npm install express --save`

6. Arrange files - based on how the server.js file is setup, I have the files used in the "view" in a Public folder. Move your application/view files to a Public folder.<br>
Note: Express needs to remain in root directory as well as the server.js, Procfile, and package.json files.

7. Run the app! To run locally, use 'npm start'.<br>
`npm start`

8. When app is working and running locally, merge branch to master.<br>
`git checkout master`<br>
`git merge new_branch_name`<br>

9. Now, Heroku. Assuming you have the Heroku toolbelt installed, you can run 'heroku create' to spin up a new Heroku app.<br>
`heroku create`

10. Make sure you git respository is connected to Heroku as well. Check 'git remote -v'. Assuming you're good to go, push your local repo, you most up-to-date version of the codebase to Heroku.<br>
`git push heroku master`

11. Make sure the Heroku server is ready.<br>
`heroku ps:scale web=1`

12. Launch your app on the web!<br>
`heroku open`<br>
or depending on how your remotes are setup:<br>
`heroku open --app heroku_app_name`

Check out the repo [here](https://github.com/eriksilver/Events-CMS) if you want to reference the files.

How do you spin up a Node + Express server?
