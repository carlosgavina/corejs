# Core.js

__Current Version:__ 0.2

A tiny (13kb) and pointless javascript framework for even tinier web apps.



## Why?

I could say a million reasons why we need another javascript framework, but really, the only reason why we need another one is because I was bored.



## Main Features

* Super tiny (13kb minified, 4kb gzipped!)
* Event driven
* Clunky code
* One dependency, <a href="http://zeptojs.com/">Zepto</a> (Recommended) or <a href="http://jquery.com/">jQuery</a>



## Quick Start

Creating an App in Core.js is faster than eating a peanut, here's how:

```js
/* App Config */

var NotesApp = new $$.App({
      name    : "notesapp",
      Router  : {
        "Signup"        : "/signup",
        "Article"       : "/article/{id}",
        "EditArticle"   : "/article/{id}/edit"
      }
    });
```


### Catching Router Events

All Core.js objects are events enabled, a new $$.App object stores important global events like routing.


```js
/* App Config */

NotesApp.on("Router:Default", function( e, data ) {
  // code for the default route, the root for the website ( example.com/ )
  // this refers to the parent element, NotesApp
  console.log( this );
});

NotesApp.on("Router:Article", function( e, data ) {
  // Prints to the console the 'id' value from the url, ( example.com/#/article/123 )
  console.log( data.id );
});

/* The app will only listen Router events after the 'start' method */
NotesApp.start();

```
