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

One of the amazing things that the Node ecosystem introduces to Javascript is the ability to share state and scope across files. Whereas in the browser we deliver essentially a single massive playload of the entire front-end Javascript application logic, on a backend application, we must be able to separate our program's logic and components across multiple files, each with a single concern and responsibility.

Following the Common.js pattern, Node allows files to declare scopes they wish to export and allow other files to load as though they were defined locally. While each file can maintain its own private scope, through `module.exports` and `require`, you can define an object or class in one file and load it into the scope of another file safely. 

For example:

**User.js**

```js
class User{
  constructor(name, email){
    this.name = name;
    this.email = email
  }
  greeting(){
    console.log(`Hello, I'm ${this.name}`)
  }
}

module.exports = User
```

**cli.js**

```js
const User = require("./User.js")

const userName = "Avi"
const userEmail = "avi@flatironschool.com"

const avi = new User(userName, userEmail)
avi.greeting() // Hello, I'm Avi
```

In this example, the `cli.js` program is able to load the class `User` defined in `User.js` by explicitly requiring that constant through `require`. `User.js` makes itself available to other files through `module.exports`.

## Node.js, NPM, and Packages

Node also introduces the concepts of remotely hosted "packages" that can be included in your application through the Node Package Manager, npm, that also plugs into `module.exports`, `require`, and Common.js.

A Node Package is a prebuilt piece of functionality that another Node program can inherit. Node Packages are like superpowers for your code and application, allowing you to grab some functionality someone has already built and add it to your application.

Every Node application ships with a file `package.json` that can contain dependencies that the application requires. These dependencies are install via the Node Package Manager, `npm`, and the compatible interfaces such as `yarn` by Facebook.

Once required, a Node package can be loaded into your application via the `require` pattern.

Imagine this complete Node Command Line Application, using both `module.exports` and `package.json` to `require` libraries and code. We're going to integrate the NPM Package [prompt](https://www.npmjs.com/package/prompt) to create command line prompt inputs for a node application.

In the application's `package.json`, we have:
**File: `package.json`**
```js
{
  "dependencies": {
    "prompt": "^1.0.0"
  }
}
```

`package.json` uses JSON notation to list dependencies. There's a lot more you can do with `package.json` but this is all that's required to be able to load the `prompt` library into our application.

* [Using `package.json`](https://docs.npmjs.com/getting-started/using-a-package.json)
* [Basics of `package.json` and NPM](http://nodesource.com/blog/the-basics-of-package-json-in-node-js-and-npm/)

Then we have our `User` class defined in `User.js` that is exported through `module.exports`.

**File: `User.js`**
```js
class User{
  constructor(name){
    this.name = name;
  }
  greeting(){
    console.log(`Hello, I'm ${this.name}`)
  }
}

module.exports = User;
```

Finally, `cli.js` can require both `User.js` and `prompt` to build a simple Node Command Line Application that asks for your name and instantiates a `User` that greets you.

**File: `cli.js`**
```js
const User = require("./User.js") // Local File
const prompt = require('prompt'); // NPM Package

prompt.start();
 
prompt.get('name', function(err, result){
  const user = new User(result.name)
  user.greeting()
});
```

The entire source for this [sample application is available](https://github.com/learn-co-curriculum/simple-node-intro).

## HTTP Server

And finally, what Node is known for is the introduction of an HTTP Server within the framework, allowing Node applications to easily listen for HTTP requests and serve HTTP responses, making Node a choice for building Web Applications.

**File: `server.js`**
```js
const http = require('http') // A package included with Node
const port = 3000

const requestHandler = (request, response) => {
  console.log(request.url)
  response.end('Hello Node.js Server!')
}

const server = http.createServer(requestHandler)

server.listen(port, (err) => {
  console.log(`server is listening on ${port}`)
})
```

The framework [`express.js`](https://expressjs.com/) adds a friendly DSL on top of the Node [`http`](https://nodejs.org/api/http.html) package.


