Dojo: The Good Parts 2
====================
This repo is a companion to the ESRI Developer Summit [Presentation](http://webapps-cdn.esri.com/tools/MobileWebAgenda/cons/index.html?conferenceID=62#@oid=4717) held March 10-13th 2014 in Palm Springs.

![Dojo: The Good Parts](https://raw.github.com/DavidSpriggs/Dojo--The-Good-Parts/master/Dojo-the-good-parts.jpg "Dojo: The Good Parts")

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