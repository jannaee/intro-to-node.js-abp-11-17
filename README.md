# Intro To Node.js

## Objectives

1. Introduce Node.js
2. Introduction to `npm` and `package.json`
3. Introduction to `module.exports` and `require`

## Introduce Node.js

Javascript was invented in 1995 by Brendan Eich as a scripting language that could be used in the newly released web browser Netscape. The language allowed programmers to safely run code on in the browser and make the page interactive. This is known as "front-end" programming, as the code is being interperted and executed by the browser, generally after the page has loaded. Quickly, many browsers adopted their own version of Javascript to allow the same functionality. In 1997, the language was standardized under the name ECMAScript, but everyone still calls it Javascript.

For years, Javascript existed only within browsers. The only program capable of interpreting Javascript, what's known as a "runtime", was the browser. The Javascript interpreter was bundled into browsers and Javascript was a front-end only language, only capable of manipulating web pages and providing interactivity for front-end developers.

Around 2008, Google unbundled the Javascript interpreter they wrote for their new browser Chrome, and released it as a standalone runtime and interpreter, suddenly allowing Javascript to run not just within a web browser, but anywhere. A year later, Ryan Dahl built a framework for writing server-side code in Javascript known as Node.js.

Node.js allows Javascript to function much like other multi-purpose languages, capable of being used to build basically anything, including the back-end of web applications.

## `module.export`, `require` and Common.js

One of the amazing thing that the Node ecosystem introduces to Javascript is the ability to share state and scope across files. Whereas in the browser we deliver essentially a single massive playload of the entire frontend Javascrip application logic, on a backend application, we must be able to separate our program's logic and components across multiple files, each with a single concern and responsibility.

Following the Common.js pattern, Node allows files to declare scopes they wish to export and allow other files to load as though they were defined locally. While each file can maintain its own private scope, through `module.exports` and `require`, you can define an object or class in one file and load it into the scope of another file safely. 

## Node.js, NPM, and Packages

Node also introduces the concepts of remotely hosted "packages" that can be included in your application through the Node Package Manager, npm, that also plugs into `module.export`, `require`, and Common.js.

A Node Package is a prebuilt piece of functionality that another Node program can inherit. Node Packages are like superpowers for your code and application, allowing you to grab some functionality someone has already built and add it to your application.

Every Node application ships with a file `packages.json` that can contain dependencies that the application requires. These dependencies are install via the Node Package Manager, `npm`, and the compatible interfaces such as `yarn` by Facebook.

Once required, a Node package can be loaded into your application wherever required via the `require` pattern.

## HTTP Server

And finally, what Node is known for is the introduction of an HTTP Server within the framework, allowing Node applications to easily listen for HTTP requests and serve HTTP responses, making Node a choice for building Web Applications.

