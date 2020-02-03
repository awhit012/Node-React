# Express

![](https://upload.wikimedia.org/wikipedia/commons/6/64/Expressjs.png)

## Why Express?

Express is the number 1 framework for creating back end web applications in Node JS.

## Learning Objectives

* Describe the Express JS framework
* Use Express to build a simple API

## What is Express JS

Express is an unopinionated, server-side JavaScript framework that runs on a Node.js server. 

It uses `Middleware` and a request response cycle. 

It will allow us to make more robust web applications with less code than it would take to build the same application without a framework. 

#### Hello World in Express

```js
const express = require('express');
const app = express();

app.get('/', (req, res) => res.send('Hello World!'))

const server = app.listen(8080, ()=>{
  console.log('Node server created at port 8080');
});
```

Equivalent vanilla Node:
```js
const http = require('http')

server = http.createServer((req, res) => {
  if(req.url === "/" && req.method === "GET") {
    res.writeHead(200,{'Content-Type':'text/plain'});
    res.write("Hello World!");
    res.end();
  }
});

server.listen(8080,()=>{
  console.log('Node server created at port 8080');
})
```

Let's disect what's going on here. 

1. Requiring express returns an executable function
2. We call that function and save the resulting object in `app`
3. We now have routing methods like `app.get(...)` and `app.post(...)` that make it easy to set up our routes. 
4. We have a `res.send()` method that makes it easy to send responses. 

#### API In Detail with Demo

**EXPRESS:**

1. `express.static()`
	- Used for sending static HTML files. We don't need this for JSON API's
1. `express.Router()`
	- Used to create Routers as middleware. More on this below.
1. and a few more

**APP:**

1. `app.locals`
	- a place for local variables for the application
1. `app.get()`, `app.post()`, `app.put()`, `app.delete()`
	- All methods for routing
1. `app.route()`
	- Set up full CRUD route for a specific resource
1. Several More

**REQ:**
1. `req.body`
	- A beautiful, already parsed body of the requst. No need for `req.on('data')`!
1. `req.cookies`
	- Freshly parsed cookies
1. `req.params`
	- parameters mapped to route names (more later)
1. Several More

**RES:**

1. `res.json()`
	- Automatically sends parsed JSON! 
1. `req.cookie()`
	- Send cookie
1. `res.redirect('/some-url')`
	- Redirects client to new page.
1. `res.render()`
	- sends template using template engine (not needed for JSON API)
1. `res.send()`
	- Adds appropriate headers and calls `end()`

1. `res.sendFile()`
	- sends static file
1. `res.sendStatus()`
	- shorthand to send a response with just a status

#### Routing and Router

Since routing is a major part of server side applications, Express has not only our `app.get()` etc. methods, but also its own Router middleware. 

As the course is wrapping up, its a good time to get used to learning from reading documentation. Fortunately, Express's documentation is well written and organized. 

Let's look at it [here](http://expressjs.com/en/guide/routing.html)



## Resources
* [Starting a project](http://expressjs.com/starter/installing.html)
* [Hello World App](http://expressjs.com/starter/hello-world.html)
* [Routing](http://expressjs.com/en/guide/routing.html)
* [Express Example](https://github.com/awhit012/learn-express)

