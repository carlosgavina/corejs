# Core.js Documentation

__Current Version:__ 0.3.3b


## "I want to" index

* [Make an App](#creating-an-app-app)
* [Use the Router](#catching-router-events)
* [Manage Data](#using-data-and-local-storage-data)
* [Use Local Storage](#using-data-and-local-storage-data)
* [Create a 'Type' of Data (extend Data)](#create-a-type-of-data-extend-data)
* [Use Templates](#using-templates--microtemplate)
* [Create a View](#creating-a-view--view)
* [Create a 'Type' of View (extend View)](#create-a-type-of-view-aka-extending-the-view)
* [Use an Api](#using-an-api--api)


## Creating an App `$$.App`

Creating an App in Core.js is faster than eating a peanut, here's how:

```js
/* App Config */

var NotesApp = new $$.App({
      name    : "notesapp",
      Router  : {

        // route match          : event fired

        "/signup"               : "Signup",
        "/article/{id}"         : "Article",
        "/article/{id}/edit"    : "EditArticle"

      }
    });
```

You are all set, next lets see how you can listen for Router (url) changes.


### Catching Router Events

All Core.js objects are Events enabled, a new `$$.App` object stores important global events, such as the Routing, or in english, detects changes in the URL and fires events accordingly.


```js
/* App Config */

NotesApp.on("Router:Default", function( e, data ) {
  // code for the default route, the root for the website ( example.com/ )
  // this, refers to the parent object, NotesApp
  console.log( this );
});

NotesApp.on("Router:Article", function( e, data ) {
  // Prints to the console the 'id' value from the url, ( example.com/#/article/123 )
  console.log( data.id );
});

/* The app will only listen Router events after the 'start' method */
NotesApp.start();

```

## Using Data and Local Storage `$$.Data`

With `$$.Data` you can manage data, store it in the browser local storage and send it to an [Api](#linking-data-with-the-api)

Creating a `$$.Data` object, easier than reading.

```js
/* create a $$.Data object */
// passing an id enables localStorage for this object automatically

var Note = new $$.Data({
    id: "MyNote"
    attributes: {
      title : "Default Title"
    }
  });

// set a new title attribute
Note.set("title", "My Note Title");

// get the title attribute
Note.get("title");

```

Listening for events on a `$$.Data` object:

```js
// continues from previous example

// Detect a specific attribute change
Note.on("Change:title", function( e, d ) {
  // the "title" attribute was changed
});

```

#### Create a 'Type' of Data (extend Data)

This is useful if you want to use various data objects that share events, methods and other behaviors.

```js
var User = $$.Data.extend({
      // events shared by all the views based on this one
      events : {
        "Change" : function() {
          // everytime data is changed this is called
          console.log("Oh my, the Data changed!");
        }
      }
    });

var user_a  = new User(),
    user_b  = new User();

user_a.on('change', function() { console.log('Data from User A changed!') });

user_a.set('name', 'charles');
//'Oh my, the Data changed!' in the console
//'Data from User A changed!' in the console

user_b.set('name', 'jane');
//'Oh my, the Data changed!' in the console

```


#### Options:

* id
* attributes


#### Methods:

* set
* get
* pull
* push


#### Events:

* Change
* Change:`Attribute Name`
* Pull:Success
* Pull:Error
* Pull:Timeout
* Push:Sucess
* Push:Error
* Push:Timeout


## Using Templates  `$$.Microtemplate`

`$$.Microtemplate` is a tiny and fast logic-less template engine that uses the already famous {{musthash}} syntax.
Unlike most other template systems that give you one way to load your template, with `$$.Microtemplate` you can load templates in three ways:

* From an HTML string, using the 'html' parameter
* From an URL, using the 'url' parameter
* From a DOM element, using the 'el' parameter and passing a valid Zepto or jQuery element.

### Syntax
```html
<h1>{{title}}</h1>
<p>{{text}}</p>
```

### Create a Template
Creating a template is less difficult than growing a musthash (if you are a man that is):

```js
// getting a template from a HTML string
var NoteTemplateFromHTML = new $$.Microtemplate({ html: "<h1>Hello {{username}}</h1>" });

// getting a template from an URL
var NoteTemplateFromURL = new $$.Microtemplate({ url: "templates/hello.html" });

// getting a template from a DOM element
var NoteTemplateFromEl = new $$.Microtemplate({ el: $("#template-hello") });
```

### Render the Template

```js
// calling the render method and passing a Zepto / jQuery element, prints the template into the DOM
// This renders '<h1>Hello carlosgavina</h1>'
NoteTemplateFromHTML.render({
  el : $("#content"),
  variables {
    username : "carlosgavina"
  }
});
```

if you use an URL to get the Template, the render method will only be called when the template is ready

```js
// will render the template into the dom as soon as the template is ready
NoteTemplateFromURL.render({ el : $("#content") });
```

#### Options

* id
* url
* html
* el

#### Methods

* render


## Creating a View  `$$.View`

Views give an easy way to manage the content of a section of your DOM.

### Create a View

```js
var NoteView = $$.View({
      el : $("#content"),
      template : new $$.Microtemplate({ html: "<h1>Hello {{username}}</h1>" }),
      init : function() {
        console.log("this is a view");
      }
    });
```

#### Create a Type of View, aka extending the View

This is useful if you want to render various views that share events, methods and other behaviors.

```js
var NoteView = $$.View.extend({
      // method fired when the view is started
      init : function() {
        this.on("SayHi", function() { console.log("Hi!"); })
      },

      // the html template
      template : new $$.Microtemplate({ html: "<h1>Hello {{username}}</h1>" }),

      // events shared by all the views based on this one
      events : {
        "Template:Rendered" : function() { // code for when a template rendered }
      }

    });

var newnote   = new NoteView(),
    othernote = new NoteView();

//'Hi!' in the console
newnote.trigger('SayHi');

//Hi! in the console
othernote.trigger('SayHi');

```



#### Methods:

* Render
* Update (available after the first Render)



## Using an Api  `$$.Api`

You can configure endpoints for an Api in the `$$.App` contructor ( or by using the `$$.Api` object )

```js
/* Configuring an Api in your App */

var NotesApp = new $$.App({
      name  : "notesapp",
      Api   : {
        url: "api.example.com/",
        requests: {

          // will match api.example.com/user/
            "user"    : { endpoint: "user/" },

            // will match api.example.com/notes/
            "notes"   : { endpoint: "notes/" }

        }
      }
    });

```


With this set, you can make requests to the server by the Api reference in NotesApp.Api:

```js
/* making a request to our NotesApp api */

// Following request matches api.example.com/user/?id=123
var getNotes = new NotesApp.Api.get("notes", {
    data: { id : 123 }
  });

// Matches api.example.com/user/
// Sends by POST the title and content
var postNotes = new NotesApp.Api.post("notes", {
    data: { title : "My note", content: "This is my first note!" }
  });

```

### Listening for Api request events

To catch Api requests events just use the .on method as such:

```js
/* Listening for events in api requests */
// This is a continuation of the previous example

getNotes.on("Success", function( e, d ) {
  // Code for when a request was successfull
});

getNotes.on("Error", function( e, d ) {
  // Code for when a request gives an error
});

```

#### Events:

* Success
* Error
* Timeout


### Linking `$$.Data` with the Api

To make things even more powerful, Core.js lets you link an Api request to a `$$.Data` object:

```js
/* Link an Api request to a $$.Data */

var Note = new $$.Data({
    request: "notes"
  });

// With the .push method, the attributes for this $$.Data object are sent by POST
// to the URL configured in our app in the "Using an Api" example
// or for lazy people, matches: api.example.com/notes/
Note.push();

Note.on("Change", function( e, d ) {

  // Event fired when the data in Note is changed.
  // in this case after the pull request is made successfully

  // Show in the console the new data stored in Note
  console.log( this.get() );

});

```


