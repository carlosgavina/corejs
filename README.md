# Core.js

__Current Version:__ 0.2

A tiny (13kb) and pointless javascript framework for even tinier web apps.


## Why?

I could say a million reasons why we need another javascript framework, but really, the only reason why we need another one is because I was bored.


## Main Features

* Super tiny (13kb)
* Clunky code
* One dependency, <a href="http://zeptojs.com/">Zepto</a> (Recommended) or <a href="http://jquery.com/">jQuery</a>


## Quick Start

Creating an App in Core.js is faster than eating a peanut, here's how:

```js
/* App Config */

var NotesApp = new $$.App({

        name : "notesapp",

        Router : {
            "Signup"        : "/signup",
            "Article"       : "/article/{id}",
            "EditArticle"   : "/article/{id}/edit"
        }

    });
```
