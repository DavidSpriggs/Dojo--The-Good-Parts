Dojo: The Good Parts
====================
This repo is a companion to the ESRI Developer Summit [Presentation](http://webapps-cdn.esri.com/tools/MobileWebAgenda/cons/index.html?conferenceID=62#@oid=4717) held March 10-13th 2014 in Palm Springs.

![Dojo: The Good Parts](https://raw.github.com/DavidSpriggs/Dojo--The-Good-Parts/master/Dojo-the-good-parts.jpg "Dojo: The Good Parts")

Dojo, dijit, dojox, util, there are a lot of parts in the Dojo Toolkit. The aim of this repo is to highlight the good parts and patterns that make Dojo a powerhouse!

[`dojo/_base/lang`](http://dojotoolkit.org/reference-guide/1.9/dojo/_base/lang.html)
-----------------
Lang is a commonly used class and contains JS language enhancements, functions for supporting Polymorphism and other language constructs that are fundemental to the rest of the toolkit.
##### `lang.clone()`
Clones objects and/or nodes, returning a new anything, versus a reference. Pass something to clone(), and a new version of that something will be made:
```javascript
require(["dojo/_base/lang"], function(lang){
  // clone an object
  var obj = { a:"b", c:"d" };
  var thing = lang.clone(obj);
  // clone an array
  var newarray = lang.clone(["a", "b", "c"]);
});
```
##### `lang.mixin()`
Mixin is a simple utility function for mixing objects together. Mixin combines two objects from right to left, overwriting the left-most object, and returning the newly mixed object for use. mixin() only works on objects
```javascript
require(["dojo/_base/lang"], function(lang){
  var a = { b: "c", d: "e" };
  lang.mixin(a, { d: "f", g: "h" });
  console.log(a); // b: c, d: f, g: h
});
```
##### `lang.hitch()`
Hitch returns a function that will execute a given function in a given context. This function allows you to control how a function executes, particularly in asynchronous operations.

Method name example. Will look for 'method' on 'this' and pass arguments:
```javascript
require(["dojo/_base/lang"], function(lang){
  var myObj = {
    foo: "bar",
    method: function(someArg){
      console.log(someArg + " " + this.foo);
    }
  };

  var func = lang.hitch(myObj, "method");

  func("foo");
  //outputs: foo bar
});
```

Anonomus function example:
```javascript
require(["dojo/_base/lang"], function(lang){
  var myObj = {
    foo: "bar",
    method: function(someArg){
      console.log(someArg + " " + this.foo);
    }
  };

  var func = lang.hitch(myObj, function(someArg){
    //this = myObj
    this.method(someArg);
  });

  func("foo");
  //outputs: foo bar
});
```
[`dojo/_base/array`](http://dojotoolkit.org/reference-guide/1.9/dojo/_base/array.html)
-----------------
Array provides enhancements to native Array functions which may not be available. In Dojo 2.0, this module will likely be replaced with a shim to support functions on legacy browsers that don’t have these native capabilities. Array has a notable difference from the JavaScript 1.6’s Array methods in that it runs over sparse arrays, passing the “holes” in the sparse array to the callback function. JavaScript 1.6’s Array methods skips the holes in the sparse array.
##### `array.every()`
every() semantically answers the question “does a test hold true for every item in the array?” Like forEach(), every() iterates over the items in an array. However, it short circuits and returns false as soon as it encounters an item for which the provided callback returns a falsey value. If the callback returns true for all items, every() returns true.
##### `array.filter()`
filter() does at it implies, filter an array or array-like structure. filter() will return an array for values from unfilteredArray for which the callback returns a truthy value. The original array is not modified.
##### `array.forEach()`
forEach() iterates over Arrays and NodeLists and provides ways to filter the results. Can also scope callback.
```javascript
require(["dojo/_base/array"], function(array){
  var foo = {
    myMethod: function(el){
        console.log(el);
    }
  };

  array.forEach(["a","b","c"],function(item){
    this.myMethod(item);
  }, foo);
  //outputs: a b c
});
```
##### `array.indexOf()`
indexof() determines the index of an element in an Array. It locates the first index of the provided value in the passed array. If the value is not found, -1 is returned.
##### `array.lastIndexOf()`
lastIndexOf() determines the last index of an element in an array. It locates the last index of the provided value in the passed array. If the value is not found, -1 is returned.
##### `array.map()`
map() iterates all the elements in an array, passing them to the callback function and then returning a new array with any of the modified results.
```javascript
// a query to a map service returns a featureSet, lets make an array of just one attribute:
// featureSet looks something like this (condensed for example): {features:[{attributes:{ZIP:63385},geometry:{rings:[...]},{attributes:{ZIP:63301},geometry:{rings:[...]},{attributes:{ZIP:63867},geometry:{rings:[...]}]};
zips = array.map(featureSet.features, function(zipPolys) {
  return zipPolys.attributes.ZIP;
});
// zips = [63385, 63301, 63867]
```
##### `array.some()`
some() semantically answers the question “does a test hold true for at least one item in the array?” Like forEach(), some() iterates over the items in an array. However, it short circuits and returns true as soon as it encounters an item for which the provided callback returns a truthy value. If the callback doesn’t return true for any item, some() returns false.
##### Note:
`every, map, forEach, some, filter` each accept a third paramater of a 'this' object! This allows you to scope the annonmus callback function! See forEach() code example above.

[`dojo/Defered`](http://dojotoolkit.org/reference-guide/1.9/dojo/Deferred.html)
--------------
Manages the communication between asynchronous threads (callbacks).
- Do not return the deffered, only the promise property.

[`dojo/promise/all`](http://dojotoolkit.org/reference-guide/1.9/dojo/promise/all.html)
------------------
A function that takes multiple promises and returns a new promise that is fulfilled when all promises have been fulfilled.
- Use array or object

[`dojo/store/Memory`](http://dojotoolkit.org/reference-guide/1.9/dojo/store/Memory.html)
-------------------
An object store wrapper for JSON available directly with an array of objects.

[`dojo/store/Observable`](http://dojotoolkit.org/reference-guide/1.9/dojo/store/Observable.html)
-----------------------
An object store wrapper that adds support for notification of data changes to query result sets.

[`dgrid`](http://dojofoundation.org/packages/dgrid/)
-------
Extensable grids.

[`dbibd`](https://github.com/kriszyp/dbind)
-------
Binding objects together.

[`dojo/Stateful`](http://dojotoolkit.org/reference-guide/1.9/dojo/Stateful.html)
---
Base class for objects that provide named properties with optional getter/setter control and the ability to watch for property changes.

[`dojo/on`](http://dojotoolkit.org/reference-guide/1.9/dojo/on.html)
---
A general-purpose event handler module for DOM nodes and other event emitting objects, providing normalized event listening and event dispatching functionality. This module is designed to be lightweight and fast, based on modern browsers’ event model.

[`dojo/number`](http://dojotoolkit.org/reference-guide/1.9/dojo/number.html)
--
Contains methods for user presentation of JavaScript Number objects: formatting, parsing, and rounding. Formatting and parsing are done in a locale-sensitive manner, using culturally appropriate patterns for representing group (thousands) and decimal separators, percent signs, etc. This module forms the basis of dojo.currency, which uses similar methods but adds support for currency symbols and alters the pattern as appropriate.

[`dojo/date/locale`](http://dojotoolkit.org/reference-guide/1.9/dojo/date/locale/format.html#dojo-date-locale-format)
---
When you want to present dates or times to the user, JavaScript only knows how to handle a single locale and language, and the actual format is implementation-dependent, and your web application has no control over these choices. Dojo comes with a powerful library to format and parse dates and times using local language and conventions, from your choice of hundreds of locales, or as you would like using custom date/time patterns.

[`dojo/query`](http://dojotoolkit.org/reference-guide/1.9/dojo/query.html)
---
CSS selector, like $.()

[`dojo/dom-create dojo/dom-class dojo/dom-style dojo/dom-construct`]()
---
DOM manipulation

[`dojo/aspect`](http://dojotoolkit.org/reference-guide/1.9/dojo/aspect.html)
---
