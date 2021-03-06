
Chic
====

Chic is an extremely simple class-like interface to JavaScript prototypal inheritance.

**Current Stable Version:** *1.0.1*  
**Automated Build Status:** [![Build Status][travis-status]][travis]  
**Node Support:** *0.6, 0.8*  
**Browser Support:** *Android Browser 2.2–4.2, Firefox 3.6, Firefox 4–16, Google Chrome 14–23, Internet Explorer 6–10, Mobile Safari iOS 4–6, Opera 12.10, Safari 5–6*


Getting Started
---------------

You can use Chic on the server side with [Node.js][node] and npm:

```sh
$ npm install chic
```

On the client side, you can either install Chic through [Component][component]:

```sh
$ component install rowanmanning/chic
```

or by simply including `chic.js` in your page:

```html
<script src="path/to/lib/chic.js"></script>
```


Usage
-----

In Node.js or using Component, you can include Chic in your script by using require:

```js
var Class = require('chic').Class;
```

If you're just including with a `<script>`, `Class` is available in the `chic` namespace:

```js
var Class = chic.Class;
```

The rest of the examples assume you've got the `Class` variable already.

### Create a class

Creating classes is very simple. You extend the base class like this:

```js
var Animal = Class.extend();
```

Obviously you want to add methods to your class, to give it some functionality:

```js
var Animal = Class.extend({
    eat:   function () { ... },
    sleep: function () { ... },
    poop:  function () { ... }
});
```

The `init` method is a special one. This is your class constructor, and is called when a new instance of your class is created. You can set things up in here.

```js
var Animal = Class.extend({
    init: function () {
        this.alive = true;
    }
});
```

### Instantiating a class

Instantiating your new class is just like instantiating any other JavaScript class now. You'll be able to use all those methods you defined!

```js
var fluffy = new Animal();
fluffy.poop(); // Bad Fluffy!
```

### Extending classes

Any class you create is also extendable. You extend custom classes in exactly the same way as the base class:

```js
var Cat = Animal.extend();
```

If you define methods in this extend, then they will override methods of the same name which have been inherited from the parent class. For example:

```js
var Animal = Class.extend({
    speak: function () {
        return 'Roar!';
    }
});

var Cat = Animal.extend({
    speak: function () {
        return 'Miaow?';
    }
});

var mrTibbles = new Cat();
mrTibbles.speak(); // Miaow?
```

If you wish to call the parent method, then that's possible using `this.sup`, which is a reference to the parent method with the same name as the one being called:

```js
var Animal = Class.extend({
    init: function (name) {
        this.name = name;
    },
    eat: function () {
        return this.name + ' is eating';
    }
});

var Cat = Animal.extend({
    eat: function () {
        return this.sup() + ' like a good kitty';
    }
});

var pet = new Cat('Mr Tibbles');
pet.eat(); // Mr Tibbles is eating like a good kitty
```


Development
-----------

To develop Chic, you'll need to clone the repo and install dependencies:

```sh
$ npm install
```

No code will be accepted unless all tests are passing and there are no lint errors. Commands are outlined below:

### Lint code

Run JSHint with the correct config against the code-base:

```sh
$ npm run-script lint
```

### Run unit tests (CLI)

Run unit tests on the command line in a Node environment:

```sh
$ npm test
```

### Run unit tests (browser)

To run unit tests in supported browsers, you need to run a small express app to serve the files (this bundles test together to make managing them a lot easier):

```sh
$ npm run-script testapp
```

Now you will be able to visit `http://localhost:3893/` in your browsers to run the tests. The app will automatically restart whenever a JavaScript file changes locally, so re-running the tests is just a case of reloading the page.

Unfortunately, my testing tools don't work correctly in Firefox 3.6 and IE 6–8. Because of this, there is a stripped down test suite available on `http://localhost:3893/legacy` which caters for these browsers.


Credit
------

This library was inspired by John Resig's great [Simple JavaScript Inheritance post][inspiration].


License
-------

Chic is licensed under the [MIT][mit] license.



[component]: https://github.com/component/component
[inspiration]: http://ejohn.org/blog/simple-javascript-inheritance/
[mit]: http://opensource.org/licenses/mit-license.php
[node]: http://nodejs.org/
[travis]: https://secure.travis-ci.org/rowanmanning/chic
[travis-status]: https://secure.travis-ci.org/rowanmanning/chic.png?branch=master
