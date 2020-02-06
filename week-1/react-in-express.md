# React in Express - A Monolithic Design Pattern

In this lesson we will build an Express app that serves a React app. 

## Up and Running

### Using Express Generator

To get our boilerplate code done quickly, we can use express-generator. 

Since we will be using React as our view layer, we will add `--no-view`:

```bash
npx express-generator --no-view react-in-express
```

This sets up our basic Express app, including this line, for serving static files from the public folder as we have seen before:

```js
app.use(express.static(path.join(__dirname, 'public')));
```

However, we are going to point this to a different folder, where our compiled React app will live: 

`app.use(express.static(path.join(__dirname, 'client/build')));`


For now, let's also comment out lines 17-18 of app.js, which set up a router, and lets add a couple routes of our own. We can set up our API routes later.  

```js

// app.use('/', indexRouter);
// app.use('/users', usersRouter);

// we will use routes like these to get data from our react app
// This will ultimately go in its own route file, but for now lets keep it simple:
app.get('/api/items', (req,res) => {
    var list = ["item1", "item2", "item3"];
    res.json(list);
    console.log('Sent list of items');
});
```

We also will set up a "catch all" route which will direct anything that isn't caught by the routes above to simply send the React app. 
```js
// Handles any requests that don't match the ones above will default to sending the React app. 
app.get('*', (req,res) =>{
    res.sendFile(path.join(__dirname+'/client/build/index.html'));
});
```

### Using `create-react-app`

If you havn't already, install `create-react-app`

`npm install -g create-react-app`

Then, lets delete the 'public' directory, and create a new empty folder called `client`. We do this because create-react-app is going to create a sub-folder called public. So we want to put it in a folder called client. 

From our root project directory run `create-react-app client`

This will create our react app inside of the client directory. Lets take a look at those files. 

### Running the App

Finally, we need to run `npm run build` from inside our react app. Now if we go to `localhost:3000` we should see our React app!
We should also be able to see our dummy list data if we go to `localhost:3000/api/items`.

For dev purposes, we will then run a server from within the react app as well, otherwise we miss out on live-reload, and have to run `npm run build` after every change to see it in the browser.

From inside the "client" folder, run `npm start`, and we will access the react app from a different PORT. However, in production, all files will be static files that live in `/client/public/build`, and the second server will not be needed. 

## Building Our App

Now, let's get building! Let's build our recipe app like we did in Pug, this time with React and Express. 

Our approach here will be different. Instead of building: "Route, Controller, Model, View," React is providing us with a SPA framework. 

I like the outside-in approach:

1. Build the desired view in React, first with dummy data
2. Create an AJAX that would hit the desired /api/someResource endpoint
3. Create a route for that endpoing
4. Create a controller method
5. Create the Model

(Basically, we are just moving the View portion from the last thing we do to the first, and the rest of our process stays the same. 

Let's build this together!







