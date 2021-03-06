# ![Carpet.js Icon](http://mgachowski.pl/carpetjs.svg) Carpet.js

<small>project icon: Rug by Factorio.us collective from The Noun Project</small>

Master: [![Build Status](https://travis-ci.org/mateuszgachowski/Carpet.js.svg?branch=master)](https://travis-ci.org/mateuszgachowski/Carpet.js) Develop: [![Build Status](https://travis-ci.org/mateuszgachowski/Carpet.js.svg?branch=develop)](https://travis-ci.org/mateuszgachowski/Carpet.js)

# Framework Usage

## Installation

```
bower install carpet
```

or download the compressed file [from here](https://github.com/mateuszgachowski/Carpet.js/blob/master/dist/carpet.min.js)

## Minimal application

Minimal application will not do anything until you define some modules.

Example:

```html
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Carpet.js - Sample usage</title>
  </head>
  <body>
    <!-- your code here -->
    <script src="bower_components/carpet/dist/carpet.min.js"></script>

    <script>
      Carpet.init(); // Initialises the framework
    </script>
  </body>
</html>
```

## Modules

Carpet.js is about modules so you have to define one before you start.
Modules are defined very easily:

In html file:

```html
<div data-module="myFirstModule"></div>
```
In JS file (before `Carpet.init()`)

```js
Carpet.module('myFirstModule', function (exports, settings, context) {
  'use strict';

  exports.init = function () {
    console.log('I will show when a data-module="myFirstModule" will be found in DOM');
  };
});
```

`Carpet.module()` takes two parameters:
- name of the module (string, it should fit the name put in `data-module` attribute)
- module body (function which will contain all the module body)

Your module body will be called with three parameters: `exports`, `settings` and `context`.

- `exports` - object which will be 'public', you can extend it with a function or properties. `exports.init` is reserved for the initial function which will be called immediately after module init. If you do not provide `exports.init` the module will stay in the memory but have to be initialized in another way (e.g. PubSub)
- `settings` - object with module settings. Settings can be passed by the DOM attribute as following:
```js
data-settings="{'key' : 'value', sample: [1, 3, 5]}"
```

- `context` - is a HTML DOM context which should be used as scope for all DOM finding actions, e.g. using jQuery:
```js
$('a', context).anything(); // or
$(context).find('.my-pro-element').on('click', anotherFunction);
```

**Additional informations**

In module body you can also access its `this` context where you can find some additional data:

```js
  this.name       // - (string) containing the name of the module
  this.moduleBody // - (function) body of the module
  this.settings   // - (object) settings object
  this.methods    // - (object) all public methods - same as 'exports'
```

## Logging to console

Carpet.js comes with bunch of console.log extensions which will help you to organise your console output.

Sample logs:
```js
Carpet:log ["Module: navigation has been loaded to memory"]
Carpet:info ["Module: navigation has been autoinited"]
```

**Enable logging**

Logging is disabled by default. You can easily enable it by just setting the `Carpet.loggingEnabled` to `true`.
Remember the property must be set before `Carpet.init()`.

```js
Carpet.loggingEnabled = true;
```

**Use available logging methods**

```js
Carpet.log('log me'); // with log level
Carpet.warn('something wrong!'); // with warn level
Carpet.error('Application abort!!'); // with error level
Carpet.info('I am awesome'); // with info level
```

Logs can take any type and any amount of parameters

```js
Carpet.warn('log me', {}, [], 1, -1, Infinity, function(){} /* any other type here */); // with log level
```

**Clearing the output**

To clear the output just call `Carpet.clearConsole()`

# Contribution

## Setup for development

```
  npm install
  grunt dist      # Generates dist files with full testing and linting
  # or
  grunt dist-dev  # Generates dist files without checking the code
```

## Generating JSDoc

```
grunt docs
```

## Running unit tests

```
npm test
```

Feel free to contribute or add [issues](https://github.com/mateuszgachowski/Carpet.js/issues) and questions
