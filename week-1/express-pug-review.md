# Express with Pug (Formerly Jade)

A Review

## What are Template Engines?
 
A template engine is software that can take data and a template parse it into raw HTML. Other template engines for Express include EJS, and Mustache.

The templates include a syntax for how to describe the HTML to be generated. EJS looks much like HTML, while Pug is highly truncated. Pug takes less typing, but has more of a learning curve for the syntax

## Pug Syntax

```pug
a(href='google.com') Google
|
|
a(class='button' href='google.com') Google
|
|
a(class='button', href='google.com') Google
```

The syntax in Pug looks like html with all of the angle brackets and closing tags stripped out. 

Let's check out the [DOCS](https://pugjs.org/language/attributes.html)

#### Lets build a quick CRUD App with Pug! 


## Resources

* [DOCS](https://pugjs.org/language/attributes.html)
* [Express Pug Example](https://github.com/awhit012/express-pug)
