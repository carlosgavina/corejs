# Core.js Documentation

__Current Version:__ 0.2.2


## "I want to" index

* [Make an App](#creating-an-app)
* [Use the Router](#catching-router-events)
* [Use an Api](#using-an-api--api-)



## Creating an App

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

You are all set, next lets see how you can listen for Router (url) changes.


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


## Using an Api ( $$.Api )

You can configure endpoints for an Api in the $$.App contructor ( or by using the $$.Api object )

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

### Listen for Api request events

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

Available Events:

* Success
* Error
* Timeout


### Linking $$.Data with the Api

To make things even more powerful, Core.js lets you link an Api request to a $$.Data object:

```js
/* Link an Api request to a $$.Data */

var Note = new $$.Data({
    request: "notes"
  });

// Uses the "notes" configured in our app in the "Using an Api" example
// or for lazy people, matches: api.example.com/notes/
Note.push();

Note.on("Change", function( e, d ) {

  // Event fired when the data in Note is changed.
  // in this case after the pull request is made successfully

  // Show in the console the new data stored in Note
  console.log( this.get() );

});

```
