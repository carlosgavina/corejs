# Core.js Documentation

__Current Version:__ 0.3.3b


## 0.3.3

#### 0.3.3b

* Fixed buf with routing one sized url's ( ex: example.com/settings/ )


#### 0.3.3

* Fixed major routing bug, now if pushstate is true, templates are forced to have full url.


## 0.3.2

#### 0.3.2c

* Fixed bugs with the router and pushstate in some browsers


#### 0.3.2b

* fixed minor bug that prevented the pushState to fire on page load.


#### 0.3.2

* pushState added to the Router, turned on by default, this is defined in the App (pushState: true)
Now you can hide the hash in the url's, example.com/#/user/carlosgavina -> example.com/user/carlosgavina


## 0.3.1

* fixed a Router bug that prevented variables to pass in some cases


## 0.3

* Fixed Router bugs
* Added `extend` methods for `$$.View`, `$$.Data` and `$$.Controller`
* Other bug fixes and optimizations

