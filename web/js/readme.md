# JavaScript

1. Namespacing:
    * Variable and function names written as camelCase;
    * Constant variables written in UPPERCASE with underline for separating words;
    * Constructors starts by word in uppercase;
    * Use a leading underscore  when naming private properties;
    * Starts with prefix `$` for Jquery-wrappers variables;
    * Starts with prefix `j-` for variable which save HTML-DOM element;
    * When saving a reference to `this` use `that`;
    * If you do make accessor functions use `getVal()` and `setVal(val)`. If the property is a boolean, use `isVal()` or `hasVal()`;
2. Always use semicolons;
3. Prefer single over double quotation marks;
4. Use [JsDoc](http://usejsdoc.org/about-getting-started.html) syntax for commenting code;
5. Always put spaces around operators and after commas;
6. Use ‘===’ and ‘!==’ over ’==’ and ‘ !=’;
7. Use shortcuts;

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
8. Use braces with all multi-line blocks;
