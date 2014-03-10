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
Manages the communication between asynchronous threads (callbacks). The deferred is the private interface that should not be returned to calling code. That's what the promise is for. See `dojo/promise/Promise`.

This example provides a basic usage of Deferred, where we are creating an async process via the setTimeout function. This could also be an async query to the server (ajax).
```javascript
require(["dojo/Deferred", "dojo/dom", "dojo/on", "dojo/domReady!"],
function(Deferred, dom, on){
  function asyncProcess(){
    var deferred = new Deferred();

    dom.byId("output").innerHTML = "I'm running...";

    setTimeout(function(){
      deferred.resolve("success");
    }, 1000);

    return deferred.promise;
  }

  on(dom.byId("startButton"), "click", function(){
    var process = asyncProcess();
    process.then(function(results){
      dom.byId("output").innerHTML = "I'm finished, and the result was: " + results;
    });
  });
  
});
```
```html
<h1>Output:</h1>
<div id="output">Not yet started.</div>
<button type="button" id="startButton">Start</button>
```
##### Notes:
- Do not return the deffered, only the promise: `return deferred.promise;`

[`dojo/promise/all`](http://dojotoolkit.org/reference-guide/1.9/dojo/promise/all.html)
------------------
A function that takes multiple promises and returns a new promise that is fulfilled when all promises have been fulfilled.
```javascript
// inside of a calss member function: ('dojo/promise/all', 'esri/tasks/query', 'esri/tasks/QueryTask' are required)
//query to get geometries of all zips from map service
var zipArray = [63385, 63301, 6387];
var queryTaskPoints = new QueryTask(url_1);
var queryTaskPolys = new QueryTask(url_2);

var zipWhereClause = "ZIP IN (" + ZipArray.join(",") + ")";

var query1 = new Query();
query1.where = zipWhereClause;
query1.outFields = ['*'];
query1.maxAllowableOffset = 1000;
query1.returnGeometry = true;
query1.outSpatialReference = this.map.spatialReference;

var query2 = new Query();
query2.where = zipWhereClause;
query2.outFields = ['*'];
query2.maxAllowableOffset = 1000;
query2.returnGeometry = true;
query2.outSpatialReference = this.map.spatialReference;

all([queryTaskPoints.execute(query1), queryTaskPolys.execute(query2)]).then(lang.hitch(this, 'viewZipsOnComplete'), lang.hitch(this, 'viewZipsOnError'));
// class member function 'viewZipsOnComplete' will recive array of results.
```
##### Notes:
Use an array or object:
```javascript
require(["dojo/promise/all"], function(all){

  all([promise1, promise2]).then(function(results){
    // results will be an Array
  });

  // -- or --

  all({
    promise1: promise1,
    promise2: promise2
  }).then(function(results){
    // results will be an Object using the keys "promise1" and "promise2"
  });

});
```
[`dojo/store/Memory`](http://dojotoolkit.org/reference-guide/1.9/dojo/store/Memory.html)
-------------------
Memory is an object store wrapper for JavaScript/JSON available directly with an array. This store implements the new Dojo Object Store API.
```javascript
require(["dojo/store/Memory"], function(Memory){
    var someData = [
        {id:1, name:"One"},
        {id:2, name:"Two"}
    ];
    store = new Memory({data: someData});

    store.get(1) -> Returns the object with an id of 1

    store.query({name:"One"}) // Returns query results from the array that match the given query

    store.query(function(object){
        return object.id > 1;
    }) // Pass a function to do more complex querying

    store.query({name:"One"}, {sort: [{attribute: "id"}]}) // Returns query results and sort by id

    store.put({id:3, name:"Three"}); // store the object with the given identity

    store.remove(3); // delete the object
});
```
[`dgrid`](http://dojofoundation.org/packages/dgrid/)
-------
Extensable ui data grids. Too much to cover here, see this link to get [started](http://dojofoundation.org/packages/dgrid/tutorials/hello_dgrid/).
```javascript
this.dgrid = new(declare([Grid]))({
	//selectionMode: "single",
	bufferRows: Infinity,
	columns: [{
		label: "Type",
		field: "type",
		sortable: true
	}, {
		label: "Truck",
		field: "label",
		sortable: true
	}, {
		label: "Last Report",
		field: "date",
		sortable: true,
		formatter: function(value) {
			return new Date(value).toLocaleString();
		}
	}]
}, 'truckGrid');
this.dgrid.startup();

var trucks = array.map(this.lastKnown.graphics, function(g) {
	return g.attributes;
});
this.deviceStore = new Memory({
	data: trucks
});
this.dgrid.set("store", this.deviceStore);
```

[`dbind`](https://github.com/kriszyp/dbind)
-------
dbind is a functional reactive data binding package that provides straightforward binding of data to components like form inputs, validation connectors, and more. The dbind framework is designed to help you create organized, well-structured, layered applications, facilitating a clean separation between a data model with validation logic and presentation elements. It is also intended to be compatible with Dojo and bindr, giving you the full capabilities of the bindr reactive data binding language with Dojo and Dijit widgets.
```javascript
require(['dbind/bind'], function(bind){
    bind(anInputElement).to(myObject, "propertyName");
    //see output realtime:
    bind(myDiv).to(myObject, 'propertyName');
});
```
For dijits:
```javascript
require(['dijit/form/TextBox', 'dbind/bind'], function(TextBox){
    var textBox = new TextBox({}, 'textbox');
    bind(textBox).to(myProperty);
});
```
[`dojo/Stateful`](http://dojotoolkit.org/reference-guide/1.9/dojo/Stateful.html)
---
Base class for objects that provide named properties with optional getter/setter control and the ability to watch for property changes.
```javascript
require(["dojo/Stateful", "dojo/_base/declare"], function(Stateful, declare){
  // Subclass dojo/Stateful:
  var MyClass = declare([Stateful], {
    foo: null,
    _fooGetter: function(){
      return this.foo;
    },
    _fooSetter: function(value){
      this.foo = value;
    }
  });

  // Create an instance and set some initial property values:
  myObj = new MyClass({
    foo: "baz"
  });

  // Watch changes on a property:
  myObj.watch("foo", function(name, oldValue, value){
    // Do something based on the change
  });

  // Get the value of a property:
  myObj.get("foo");

  // Set the value of a property:
  myObj.set("foo", "bar");
});
```

[`dojo/on`](http://dojotoolkit.org/reference-guide/1.9/dojo/on.html)
---
A general-purpose event handler module for DOM nodes and other event emitting objects, providing normalized event listening and event dispatching functionality. This module is designed to be lightweight and fast, based on modern browsers’ event model.
```javascript
require(["dojo/on"], function(on){
  on(target, "event", function(e){
    // handle event
  });

  on.emit(target, "event", {
    bubbles: true,
    cancelable: true
  });
});
```
[`dojo/Evented`](http://dojotoolkit.org/reference-guide/1.9/dojo/Evented.html)
---
dojo/Evented is a module that provides a class that can be used as a base class or mixin for JavaScript classes that emit their own events. dojo/Evented is designed to provide a class that allows a developer to emit events and provide an easy way to allow those events to be connected to by downstream users. It leverages the API concepts of :ref:dojo/on <dojo/on>. It should be noted though that this is for what is commonly referred to as “sythetic” events, which are different than DOM events, which dojo/on normalises.
```javascript
define(["dojo/Evented", "dojo/_base/declare"], function(Evented, declare){
  var MyComponent = declare([Evented], {
    startup: function(){
      // once we are done with startup, fire the "ready" event
      this.emit("ready", {});
    }
  });

  component = new MyComponent();
  component.on("ready", function(){
    // this will be called when the "ready" event is emitted
    // ...
  });
  component.startup();
});
```

[`dojo/number`](http://dojotoolkit.org/reference-guide/1.9/dojo/number.html)
--
Contains methods for user presentation of JavaScript Number objects: formatting, parsing, and rounding. Formatting and parsing are done in a locale-sensitive manner, using culturally appropriate patterns for representing group (thousands) and decimal separators, percent signs, etc. This module forms the basis of dojo.currency, which uses similar methods but adds support for currency symbols and alters the pattern as appropriate.

[`dojo/date/locale`](http://dojotoolkit.org/reference-guide/1.9/dojo/date/locale/format.html#dojo-date-locale-format)
---
When you want to present dates or times to the user, JavaScript only knows how to handle a single locale and language, and the actual format is implementation-dependent, and your web application has no control over these choices. Dojo comes with a powerful library to format and parse dates and times using local language and conventions, from your choice of hundreds of locales, or as you would like using custom date/time patterns.

[`dojo/query`](http://dojotoolkit.org/reference-guide/1.9/dojo/query.html)
---
CSS selector, like $.()
```javascript
require(["dojo/query", "dojo/NodeList-dom"], function(query){
  query("li").forEach(function(node){
    node.innerHTML = "Something";
  }).style("color", "red")
    .style("fontSize", "12px");
});
```
```javascript
require(["dojo/query", "dojo/NodeList-fx"], function(query, nodeListFx){
    query("li.evens").fadeOut({
          duration:1000,
          onEnd: function(){ ... },
          // begin playing immediately, and return the nodeList for further iteration
          auto:true
        }).onclick(doSomething);
});
```

`dojo/dom-* (class, style, construct)`
---
DOM manipulation, abstracted.

##### [`dojo/dom-class`](http://dojotoolkit.org/reference-guide/1.9/dojo/dom-class.html)
Manipulate css class names on nodes.

Methods: contains(), add(), remove(), replace(), toggle().
```javascript
require(["dojo/dom-class", "dojo/dom", "dojo/on"],
function(domClass, dom, on){
  on(dom.byId("button2"), "click", function(){
    domClass.toggle("example2", "style2");
  });
});
```

[`dojo/aspect`](http://dojotoolkit.org/reference-guide/1.9/dojo/aspect.html)
---
The dojo/aspect module provides aspect oriented programming facilities to attach additional functionality to existing methods.

##### `after()`

The module includes an after function that provides after advice to a method. The provided advising function will be called after the main method is called. The after function’s signature is:
```javascript
after(target, methodName, advisingFunction, receiveArguments);
```

##### `before()`
The module also includes a before function that provides before advice to a method. The provided advising function will be called before the main method is called. The before function’s signature is:
```javascript
before(target, methodName, advisingFunction);
```

##### `around()`
The module finally includes an around function that provides around advice to a method. The provided advising function will be called in place of the main method, and the advising function will be passed a chaining function that can be used to continue to call execution to the next advice or original method. The around function’s signature is:
```javascript
around(target, methodName, advisingFactory);
```

##### Example of after(): (in a class module)
```javascript
postCreate: function() {
    this.printTask = new esri.tasks.PrintTask(this.printTaskURL);
    aspect.after(this.printTask, '_createOperationalLayers', this.operationalLayersInspector, false);
},
operationalLayersInspector: function(opLayers) {
    array.forEach(opLayers, function(layer) {
        if (layer.id == "Measurement_graphicslayer") {
            array.forEach(layer.featureCollection.layers, function(fcLayer) {
                array.forEach(fcLayer.featureSet.features, function(feature) {
                    delete feature.attributes;
                    feature.symbol.font.family = "Courier";
                    feature.symbol.font.variant = esri.symbol.Font.VARIANT_NORMAL;
                    feature.symbol.font.size = "32pt";
                });
            });
        }
    });
    return opLayers;
},
```
[`dojo/_base/declare`](http://dojotoolkit.org/reference-guide/1.9/dojo/_base/declare.html)
---
Declare contains functions to define Dojo classes, which support standard Object Oriented concepts within Dojo. JavaScript uses prototype-based inheritance, not class-based inheritance (which is used by most programming languages). Dojo provides the ability to simulate class-based inheritance using declare.
```javascript
// in "my/Person.js"
define(["dojo/_base/declare", "dojo/_base/lang"], function(declare, lang){
  return declare(null, {
    name: "Anonymous",
    age: null,
    residence: "Universe A",

    constructor: function(kwArgs){
      lang.mixin(this, kwArgs);
    },

    moveTo: function(residence){
      this.residence = residence;
    }
  });
});
```
```javascript
// using the class elsewhere...
require(["my/Person"], function(Person){
  var anon  = new Person();
  var alice = new Person({ name: "Alice", age: 42, residence: "Universe 1" });

  console.log(anon.name, alice.name); // "Anonymous", "Alice"
  console.log(anon.residence, alice.residence); // "Universe A", "Universe 1"
  alice.moveTo("Universe 420");
  console.log(alice.residence); // "Universe 420"
});
```
