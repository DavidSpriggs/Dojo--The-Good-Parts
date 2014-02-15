Dojo: The Good Parts
====================
This repo is a companion to the ESRI Developer Summit [Presentation](http://webapps-cdn.esri.com/tools/MobileWebAgenda/cons/index.html?conferenceID=62#@oid=4717) held March 10-13th 2014 in Palm Springs.

![Dojo: The Good Parts](https://raw.github.com/DavidSpriggs/Dojo--The-Good-Parts/master/Dojo-the-good-parts.jpg "Dojo: The Good Parts")

Dojo, dijit, dojox, util, there are a lot of parts in the Dojo Toolkit. The aim of this repo is to highlight the good parts and patterns that make Dojo a powerhouse!

[`dojo/_base/lang`](http://dojotoolkit.org/reference-guide/1.9/dojo/_base/lang.html)
-----------------
Lang is a commonly used class and contains JS language enhancements.

[`dojo/_base/array`](http://dojotoolkit.org/reference-guide/1.9/dojo/_base/array.html)
-----------------
Array functions.

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
