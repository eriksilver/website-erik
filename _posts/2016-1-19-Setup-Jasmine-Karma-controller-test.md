---
layout: post
title:  Set up an Angular controller unit test with Jasmine and Karmas
date: 2016-1-19
image: images/@stock/blog-9.jpg
excerpt:
  Nisi quas minima cumque et voluptate. et et iure nostrum necessitatibus et ipsam sed doloribus ab odio. voluptates velit et quaerat qui
categories:
      - Web Design
tags: Unit-testing, Karma, Jasmine, Angular, How to
author: Erik
published: true
permalink: /blog/Set-up-an-Angular-controller-unit-test-with-Jasmine-and-Karma
---

My goal was to setup a unit test for an Angular controller. I decided to use the Jasmine for the testing assertions and Karma as the test runner.

This post shares the step by step process to add the testing framework to an Angular app and get it running.

These are the these steps I used to publish an Angular app, the Event Management System. A link to the full Github repo is at the bottom.

First, [install Karma](http://karma-runner.github.io/0.13/intro/installation.html), which is used to run the tests.

{% highlight js %}
npm install karma --save-dev
npm install karma-jasmine karma-chrome-launcher --save-dev
npm install -g karma-cli
{% endhighlight %}

Next, create a configuration file that tells Karma about your project. Here, it is called 'my.conf.js'.
{% highlight js %}
karma init my.conf.js
{% endhighlight %}

The dependencies of the app are important because they are included in the testing configuration. In this project, the major dependencies are Angular and Firebase. I also added Angular Mocks, a module that helps inject and mock Angular services for unit tests.

Many of the errors I ran into, e.g. 'module is not defined' and 'module is not available', were caused by not having the proper files OR the files load in the correct order in the configuration file.

Here is a snapshot of my configuration file (my.conf.js):
{% gist 5c5b66010c44dae90ce0 %}

The unit tests are written plain JavaScript, and so you'll need to create files for the tests. I created a test folder in my project root directory and I created two files for the tests, 'hello.js' and 'appSpec.js'.

The first test I wrote was a basic one in 'hello.js', to make sure Jasmine and Karma were hooked up correctly. The simple test is testing 'true' to be 'true'.
{% highlight js %}
describe("hello test is true", function () {
    it("should work", function () {
        expect(true).toBe(true)
    })
})
{% endhighlight %}

Next, I wrote two tests in the 'appSpec.js' file. I created a simple controller to test, called 'AppCtrl', to make sure the wiring was correct to specifically test a controller.

{% highlight js %}
describe('AppCtrl hello world controller test', function(){
    var scope; //we'll use this scope in our tests

    //mock Application to allow us to inject our own dependencies
    beforeEach(module('EventCMS'));
    //mock the controller for the same reason and include $rootScope and $controller
    beforeEach(inject(function($rootScope, $controller){
        //create an empty scope
        scope = $rootScope.$new();
        //declare the controller and inject our empty scope
        $controller('AppCtrl', {$scope: scope});
    }));
    // tests start here
    it('should have variable text = "Hello World!"', function(){
        expect(scope.text).toBeDefined();
        expect(scope.text).toBe('Hello World!');
    });
});
{% endhighlight %}

The final test was my real test case - the List View controller, which handles the main List View in the application. I setup one test with to assertions 1) that the controller exists (is not null) and 2) that the scope.events is defined.

Note the code that is above the '//tests start here'. The way Karma works is to spawn a web server to run the application in a browser to execute the source code against the the test code. We need to define variables we want to use in our tests and also inject the module, scope, and controller so we can use and reference those in the tests.

{% highlight js %}
describe('ListCtrl controller test', function(){
    var scope; //we'll use this scope in our tests
    var listViewCtrl; //define controller to use in tests

    //mock Application to allow us to inject our own dependencies
    beforeEach(module('EventCMS'));
    //mock the controller for the same reason and include $rootScope and $controller
    beforeEach(inject(function($rootScope, $controller){
        //create an empty scope
        scope = $rootScope.$new();
        //declare the controller and inject our empty scope
        listViewCtrl = $controller('ListCtrl', {$scope: scope});
    }));

    // tests start here
    it('should have scope.events be defined', function(){
        //controller exists
        expect(listViewCtrl).not.toBeNull();
        //scope.events is populated
        expect(scope.events).toBeDefined();
    });
});
{% endhighlight %}

We're ready to run the tests!

{% highlight js %}
//basic start command
karma start my.conf.js

OR

//manually set to single run test with dedugging
karma start my.conf.js --log-level debug --single-run
{% endhighlight %}
Note: I preferred setting singleRun to true in the 'my.conf.js' config file, otherwise a browser window opens and stays open.

Here I presented one of many ways and flavors to do unit testing with Angular.
Other options I'm interested in are, keeping the tests running in the background, displaying the tests in the browser, and updating them with each save or commit.

Here is the live application: [Events CMS](https://events-to-manage.herokuapp.com/) <br>
Check out the repo [here](https://github.com/eriksilver/Events-CMS) if you want to view the code and files.
