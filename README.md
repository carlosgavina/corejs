# Core.js

__Current Version:__ 0.2.10a

A tiny (15kb) and pointless javascript framework for even tinier web apps.


## Why?

I could say a million reasons why we need another javascript framework, but really, the only reason why we need another one is because I was bored.


## Main Features

* Super tiny (15kb minified, 5kb gzipped!)
* Event driven
* One dependency, <a href="http://zeptojs.com/">Zepto</a> (Recommended) or <a href="http://jquery.com/">jQuery</a>
* Clunky code


## Quick Start

Include [core.min.js](core.min.js) in your page, don't forget to add <a href="http://zeptojs.com/">Zepto</a> (Recommended) or <a href="http://jquery.com/">jQuery</a> before.

```html
<script src="core.min.js"></script>
```


Creating an App in Core.js is faster than eating a peanut, here's how:

```js
/* App Config */

var NotesApp = new $$.App({
      name    : "notesapp",
      Router  : {
        "/signup"        		: "Signup",
        "/article/{id}"  		: "Article",
        "/article/{id}/edit"   	: "EditArticle"
      }
    });
```

You are set! Head to the [Documentation](documentation.md) to see how awesome and easy Core.js is. _Awesomer_ than Battman.


## [Documentation](documentation.md)

I try to have this as documented as possible, but not all features are explained. See [Documentation](documentation.md).


## Thanks etc.

* to <a href="https://github.com/Couto">couto</a> for <a href="https://github.com/Couto/Blueprint">Blueprint</a>
* to <a href="https://github.com/magalhini">magalhini</a> and <a href="https://github.com/gnclmorais">gnclmorais</a>

You guys are awesome.
