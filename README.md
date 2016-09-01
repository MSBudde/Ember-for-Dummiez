# Ember-for-Dummiez

## By the end of this lesson you "SHOULD" know how to build a simple app using Ember from scratch.

## We'll cover these steps:

Installing Ember.
Creating a new application.
Defining a route.
Writing a UI component.
Building your app to be deployed to production.
---

## Install Ember

You can install Ember with a single command using npm, the Node.js package manager. Type this into your terminal:

1
npm install -g ember-cli@2.5
---
## Create a New Application

Once you've installed Ember CLI via npm, you will have access to a new ember command in your terminal. You can use the ember new command to create a new application.

1
 ## ember new ember-quickstart

This one command will create a new directory called ember-quickstart and set up a new Ember application inside of it. Out of the box, your application will include:

A development server.
Template compilation.
JavaScript and CSS minification.
ES2015 features via Babel.
By providing everything you need to build production-ready web applications in an integrated package, Ember makes starting new projects a breeze.
---

Let's make sure everything is working properly. cd into the application directory ember-quickstart and start the development server by typing:


cd ember-quickstart
ember server


After a few seconds, you should see output that looks like this:

Livereload server on http://localhost:49152
Serving on http://localhost:4200/
(To stop the server at any time, type Ctrl-C in your terminal.)


Open http://localhost:4200 in your browser of choice. You should see a page that says "Welcome to Ember" and not much else. Congratulations! You just created and booted your first Ember app.

Switch to your editor and open app/templates/application.hbs. This is called the application template and it is always on screen while the user has your application loaded.

In your editor, change the text inside the <h2> from Welcome to Ember to PeopleTracker and save the file. Notice that Ember detects the change you just made and automatically reloads the page for you in the background. You should see that "Welcome to Ember" has been replaced by "PeopleTracker".
---
## Define a Route

Let's build an application that shows a list of scientists. To do that, the first step is to create a route. For now, you can think of routes as being the different pages that make up your application.

Ember comes with generators that automate the boilerplate code for common tasks. To generate a route, type this in your terminal:


1 ember generate route scientists


You'll see output like this:


1 installing route
2 create app/routes/scientists.js 3 create app/templates/scientists.hbs
4 updating router
5 add route scientists
6 installing route-test
7 create tests/unit/routes/scientists-test.js

That's Ember telling you that it has created:

A template to be displayed when the user visits /scientists.
A Route object that fetches the model used by that template.
An entry in the application's router (located in app/router.js).
A unit test for this route.
Open the newly-created template in app/templates/scientists.hbs and add the following HTML:





