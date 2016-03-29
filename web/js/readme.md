# JavaScript

* Namespacing:
    * Variable and function names written as camelCase;
    * Constant variables written in UPPERCASE with underline for separating words;
    * Constructors starts by word in uppercase;
    * Use a leading underscore  when naming private properties;
    * Starts with prefix `$` for Jquery-wrappers variables;
    * Starts with prefix `j-` for variable which save HTML-DOM element;
    * When saving a reference to `this` use `that`;
    * If you do make accessor functions use `getVal()` and `setVal(val)`. If the property is a boolean, use `isVal()` or `hasVal()`;
* Declare variables in the beginning of a function;
* Always use semicolons;
* Prefer single over double quotation marks;
* Use [JsDoc](http://usejsdoc.org/about-getting-started.html) syntax for commenting code;
* Always put spaces around operators and after commas;
* Use ‘===’ and ‘!==’ over ’==’ and ‘ !=’;
* Use shortcuts;

```javascript
/* Not recommended */
if (name !== '') {
    // do some magic
}
/* Recommended */
if (name) {
    // write the code
}
```

* Use braces with all multi-line blocks;
* Separate chain of calls logically;

```javascript
$('.j-btn').addClass('active')
    .siblings().removeClass('active');
```
