# Express with Pug (Formerly Jade)

A Review

## What are Template Engines?
 
A template engine is software that can take data and a template parse it into raw HTML. Other template engines for Express include EJS, and Mustache.

The templates include a syntax for how to describe the HTML to be generated. EJS looks much like HTML, while Pug is highly truncated. Pug takes less typing, but has more of a learning curve for the syntax

## Pug Syntax

#### Links

```pug
a(href='google.com') Google
|
|
a(class='button' href='google.com') Google
|
|
a(class='button', href='google.com') Google
```

#### Divs

```pug
div(class='div-class', (click)='play()')
div(class='div-class' '(click)'='play()')
```

#### Conditionals

```pug
- var user = { description: 'foo bar baz' }
- var authorised = false
#user
  if user.description
    h2.green Description
    p.description= user.description
  else if authorised
    h2.blue Description
    p.description.
      User has no description,
      why not add one...
  else
    h2.red Description
    p.description User has no description
```

#### Iteration

```pug
ul
  each val in [1, 2, 3, 4, 5]
    li= val
```

The syntax in Pug looks like html with all of the angle brackets and closing tags stripped out. 

Let's check out the [DOCS](https://pugjs.org/language/attributes.html)

#### Lets build a quick CRUD App with Pug! 


## Resources

* [DOCS](https://pugjs.org/language/attributes.html)
* [Express Pug Example](https://github.com/awhit012/express-pug)
