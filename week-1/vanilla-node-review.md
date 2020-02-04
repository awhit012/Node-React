# Vanilla Node

A Review

## The HTTP Module
 
`const http = require('http')`

![](https://i.ytimg.com/vi/VLXAzzRjQws/maxresdefault.jpg)

## Learning Objectives

* Use the native HTTP module to create a web server

## What is a Web Server?

![](https://i0.wp.com/www.informationq.com/wp-content/uploads/2017/12/What-is-a-Web-Server.jpg)

A Web Server is software that handles HTTP(s) requests. 

We can build one in Node by taking advantage of the Node Event loop, which will run waiting for requests of any kind, including web requests, and with Node's built in HTTP module. 


## Anatomy of the HTTP module:

#### Server

The server itself is a specialized event loop created to run on the Node event loop, specifically listening for Request.

The response gets sent using the `end` command. 

We can create a server using `http.createServer()`.

```js
const http = require('http'),
      server = http.createServer();

server.on('request',(request,response)=>{
   response.writeHead(200,{'Content-Type':'text/plain'});
   response.write('Hello world');
   response.end();
});

server.listen(3000,()=>{
  console.log('Node server created at port 3000');
});
```

or a little more cleanly:

```js
//server.js
const http = require('http')
      
const makeServer = function (request,response){
   response.writeHead(200,{'Content-Type':'text/plain'});
   response.write('Hello world');
   response.end();
},
      
server = http.createServer(makeServer);

server.listen(3000,()=>{
  console.log('Node server created at port 3000');

```

#### Requests

Our server listens for requests, much like an event listener can listen for clicks. Like we can access the event using an argument like this: `(event)`, we can access the request using an argument as shown above. Like events have a whole set of attributes and methods, so do requests.

In building web servers, requests are the only input that comes in. Responses are the only output. Our application is responsible for what happens in between. 

The request object will be different depending on the request. 

Requests have the following attributes (and more):

- url, the url the request is being made to
- path, which contains any query strings or parameters in the url
- headers, which store metadata
- method, 'GET, POST, etc'
- body, which has the data being sent, if there is any, such as in a POST or PUT request


#### Response

The response object is automatically created when a request comes in as well. 

We can build the response the way we want using `response.writeHead(200,{'Content-Type':'text/plain'})` and `response.write(someJSON)` etc. 

We will be building our response objects depending on the request object. 

For example, a request that has a method of GET, and a url of `localhost:3000/comments`, might get a response that looks like this: 


```js
response.writeHead(200,{'Content-Type':'text/plain'});
response.write(JSON.stringify(comments));
response.end();
```

#### Request Body

When there is data in the body of the request, Node HTTP loads it in chunks. To get this data, we need to set up a special event listener to piece together these chunks back into usable data:

```js
let body = [];
request.on('data', (chunk) => {
  body.push(chunk);
}).on('end', () => {
  body = Buffer.concat(body).toString();
  // at this point, `body` has the entire request body stored in it as a string
});
```

#### Error Handling

We can add an 'error' listener to our requests like this: 

```js
request.on('error', (err) => {
  // This prints the error message and stack trace to `stderr`.
  console.error(err.stack);
});
```

## Implementation 

## Basic

```js
const http = require('http'),
      
makeServer = function (request,response){
  response.writeHead(200,{'Content-Type':'text/plain'});
  response.write('Hello world');
  response.end();
}
      
server = http.createServer(makeServer);

server.listen(8080,()=>{
  console.log('Node server created at port 8080');
})
```

## HTML

```js
const http = require('http')
const html = `<!DOCTYPE html>
              <html>
              <head>
                <title>My Web Page</title>
              </head>
              <body>
                <h1 style="color:red;">HELLO WORLD!</h1>
                <p style="color:green;">It's a beautiful day.</p>
              </body>
              </html>`
      
makeServer = function (request,response){
  response.writeHead(200,{'Content-Type':'text/html'});
  response.write(html);
  response.end();
}
      
server = http.createServer(makeServer);

server.listen(8080,()=>{
  console.log('Node server created at port 8080');
})
```

## JSON

```js
const http = require('http')
const codeSnippets = [
  {
    id: 1, 
    name: "Knuth Morris Pratt",
    code: `console.log('KMP FTW')`
  }
]
      
makeServer = function (request,response){
  response.writeHead(200,{'Content-Type':'application/json'});
  response.write(JSON.stringify(codeSnippets));
  response.end();
}
      
server = http.createServer(makeServer);

server.listen(8080,()=>{
  console.log('Node server created at port 8080');
})
```

## Resources

* [Intro to Node Web Servers](https://codeburst.io/the-only-nodejs-introduction-youll-ever-need-d969a47ef219)
* [HTTP Docs](https://nodejs.org/api/http.html)
* [Anatomy of a HTTP transaction](https://nodejs.org/es/docs/guides/anatomy-of-an-http-transaction/)
* [Vanilla Node JSON REST API](https://github.com/awhit012/vanilla-node-json-rest-api)
