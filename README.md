# Ember-for-Dummiez

## By the end of this lesson you "SHOULD" know how to build a simple app using Ember from scratch.

## We'll cover these steps:

1) Installing Ember.
2) Creating a new application.
3) Defining a route.
4) Writing a UI component.
5) Building your app to be deployed to production.
---

## Install Ember

You can install Ember with a single command using npm, the Node.js package manager. Type this into your terminal:


1) npm install -g ember-cli@2.5
---
## Create a New Application

Once you've installed Ember CLI via npm, you will have access to a new ember command in your terminal. You can use the ember new command to create a new application.


 1) ## ember new ember-quickstart

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


 ember generate route scientists


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
Open the newly-created template in app/templates/scientists.hbs and add the following HTML:

app/templates/scientists.hbs
1
<h2>List of Scientists</h2>
In your browser, open http://localhost:4200/scientists. You should see the <h2> you put in the scientists.hbs template, right below the <h2> from our application.hbs template.

Now that we've got the scientists template rendering, let's give it some data to render. We do that by specifying a model for that route, and we can specify a model by editing app/routes/scientists.js.

We'll take the code created for us by the generator and add a model() method to the Route:

app/routes/scientists.js

import Ember from 'ember';

export default Ember.Route.extend({
  model() {
    return ['Marie Curie', 'Mae Jemison', 'Albert Hofmann'];
  }
});
(This code example uses the latest features in JavaScript, some of which you may not be familiar with. Learn more with this overview of the newest JavaScript features.)

In a route's model() method, you return whatever data you want to make available to the template. If you need to fetch data asynchronously, the model() method supports any library that uses JavaScript Promises.

Now let's tell Ember how to turn that array of strings into HTML. Open the scientists template and add some Handlebars code to loop through the array and print it:

app/templates/scientists.hbs



1) <h2>List of Scientists</h2>

2) <ul>
  3) {{#each model as |scientist|}}
    4) <li>{{scientist}}</li>
  5) {{/each}}
6) </ul>
Here, we use the each helper to loop over each item in the array we provided from the model() hook and print it inside an <li> element.

Create a UI Component

As your application grows and you notice you are sharing UI elements between multiple pages (or using them multiple times on the same page), Ember makes it easy to refactor your templates into reusable components.

Let's create a people-list component that we can use in multiple places to show a list of people.

As usual, there's a generator that makes this easy for us. Make a new component by typing:


1) ember generate component people-list
Copy and paste the scientists template into the people-list component's template and edit it to look as follows:

app/templates/components/people-list.hbs

1) <h2>{{title}}</h2>

2) <ul>
 3) {{#each people as |person|}}
  4)  <li>{{person}}</li>
 5) {{/each}}
6) </ul>
Note that we've changed the title from a hard-coded string ("List of Scientists") to a dynamic property ({{title}}). We've also renamed scientist to the more-generic person, decreasing the coupling of our component to where it's used.

Save this template and switch back to the scientists template. Replace all our old code with our new componentized version. Components look like HTML tags but instead of using angle brackets (<tag>) they use double curly braces ({{component}}). We're going to tell our component:

What title to use, via the title attribute.
What array of people to use, via the people attribute. We'll provide this route's model as the list of people.
app/templates/scientists.hbs



1) <h2>List of Scientists</h2>

2) <ul>
 3)  {{#each model as |scientist|}}
4)    <li>{{scientist}}</li>
 5) {{/each}}
6) </ul>
7) {{people-list title="List of Scientists" people=model}}
---
Go back to your browser and you should see that the UI looks identical. The only difference is that now we've componentized our list into a version that's more reusable and more maintainable.

You can see this in action if you create a new route that shows a different list of people. As an exercise for the reader, you may try to create a programmers route that shows a list of famous programmers. By re-using the people-list component, you can do it in almost no code at all.

Building For Production

Now that we've written our application and verified that it works in development, it's time to get it ready to deploy to our users. To do so, run the following command:


1) ember build --env production

The build command packages up all of the assets that make up your application—JavaScript, templates, CSS, web fonts, images, and more.

In this case, we told Ember to build for the production environment via the --env flag. This creates an optimized bundle that's ready to upload to your web host. Once the build finishes, you'll find all of the concatenated and minified assets in your application's dist/ directory.

The Ember community values collaboration and building common tools that everyone relies on. If you're interested in deploying your app to production in a fast and reliable way, check out the Ember CLI Deploy addon.

If you deploy your application to an Apache web server, first create a new virtual host for the application. To make sure all routes are handled by index.html, add the following directive to the application's virtual host configuration FallbackResource index.html

Installing Ember Edit Page

Getting started with Ember is easy. Ember projects are created and managed through our command line build tool Ember CLI. This tool provides:

Modern application asset management (including concatenation, minification, and versioning).
Generators to help create components, routes, and more.
A conventional project layout, making existing Ember applications easy to approach.
Support for ES2015/ES6 JavaScript via the Babel project. This includes support for JavaScript modules, which are used throughout this guide.
A complete QUnit test harness.
The ability to consume a growing ecosystem of Ember Addons.
Dependencies

Node.js and npm

Ember CLI is built with JavaScript, and expects the Node.js runtime. It also requires dependencies fetched via npm. npm is packaged with Node.js, so if your computer has Node.js installed you are ready to go.

Ember requires Node.js 0.12 or higher and npm 2.7 or higher. If you're not sure whether you have Node.js or the right version, run this on your command line:


1) node --version
2)npm --version
If you get a "command not found" error or an outdated version for Node:

Windows or Mac users can download and run this Node.js installer.
Mac users often prefer to install Node using Homebrew. After installing Homebrew, run brew install node to install Node.js.
Linux users can use this guide for Node.js installation on Linux.
If you get an outdated version of npm, run npm install -g npm.

Git

Ember requires Git to manage many of its dependencies. Git comes with Mac OS X and most Linux distributions. Windows users can download and run this Git installer.

Watchman (optional)

On Mac and Linux, you can improve file watching performance by installing Watchman.

PhantomJS (optional)

You can run your tests from the command line with PhantomJS, without the need for a browser to be open. Consult the PhantomJS download instructions.

Installation

Install Ember using npm:


1) npm install -g ember-cli@2.5
To verify that your installation was successful, run:


1) ember -v
If a version number is shown, you're ready to go.





