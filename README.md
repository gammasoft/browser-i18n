browser-i18n
============

Simple tool for i18n in the browser, inspired by 
[mashpie/i18n-node](https://github.com/mashpie/i18n-node) and 
[jeresig/i18n-node-2](https://github.com/jeresig/i18n-node-2), 
with the difference that this script is browser only (not a node.js module).

### Usage

```html
<script src="/i18n.js"></script>
<script>
  //Will make a request to /locales/en.json and then cache the results
  var i18n = new I18n({
    //these are the default values, you can omit
    directory: "/locales",
    locale: "en",
    extension: ".json"
  });  
  
  console.log(i18n.__("Hello")); //Hello
  console.log(i18n.__("Hello %s", "Foo")); //Hello Foo
  console.log(i18n.__n("%s cat", 0)) //no cats
  console.log(i18n.__n("%s cat", 1)) //1 cat
  console.log(i18n.__n("%s cat", 2)) //2 cats
  
  //You can change locale at any time by issuing `setLocale`
  //Another request is made in order to load /locales/de.json
  i18n.setLocale("de");
  
  console.log(i18n.__("Hello")); //Hallo
  console.log(i18n.__("Hello %s", "Foo")); //Hallo Foo
  console.log(i18n.__n("%s cat", 0)) //keine katzen
  console.log(i18n.__n("%s cat", 1)) //1 katze
  console.log(i18n.__n("%s cat", 2)) //2 katzen
</script>
```

If you don't provide a locale at instantiation browser-i18n will first try 
to get locale information from html's lang tag (`<html lang="locale">...</html>`) in case 
it is not defined locale value will fallback to `en` automatically.

#### Locale Files

You will have to create a separate locale file for each language. Locale files should look like this:  

**/locales/en.json**
```json
{
  "Hello": "Hello",
  "Hello %s": "Hello %s",
  "%s cat": {
  	"zero": "no cats",
    "one": "%s cat",
    "other": "%s cats"
  }
}
```

**/locales/de.json**
```json
{
  "Hello": "Hallo",
  "Hello %s": "Hallo %s",
  "%s cat": {
  	"zero": "keine katzen",
    "one": "%s katze",
    "other": "%s katzen"
  }
}
```

Mind that you can use [Sprintf](https://github.com/alexei/sprintf.js) syntax in your locale files
so don't forget checking their documantation to get the most out of browser-i18n

### Dependencies
1. [JQuery](http://jquery.com/) 
2. [Sprintf](https://github.com/alexei/sprintf.js)

### The MIT License (MIT)

Copyright (c) 2013 Gammasoft

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
