# CSS

1. Use class names that are as short as possible but as long as necessary;
2. Avoid qualifying class names with type selectors;
3. When grouping selectors, keep individual selectors to a single line;
4. Use a space after a property name’s colon;
5. Do not use units after 0 values unless they are required;
6. Do not use put 0s in front of values or lengths between -1 and 1;
7. Separate rules by new lines;
8. Use lowercase and shorthand hex values;

```css
/* Not recommended */
div.navigation{             // 1, 2
    margin:0px;             // 5
    font-size: 0.8em;       // 6
    background: #FFFFFF;
}

/* Recommended */
.nav,                       // 3
.footer {                   // 3
    margin: 0;              // 4, 5
    font-size: .8em;        // 6
    background: #fff;
}
                            // 7
.nav__logo {}
```
