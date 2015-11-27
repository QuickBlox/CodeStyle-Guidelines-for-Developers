# QuickBlox Android Code Style
Most of the following guidelines match [Java Code Conventions from Oracle (JCC)](http://www.oracle.com/technetwork/java/codeconventions-150003.pdf). Read it carefully first.

These conventions *may* and, probably, *will* be complemented by new practices that were missed in previous editions.

This is just a must-have set of recommendations and principles. For deeper explanations, details, examples and edge-cases, please take a look at JCC document.


## Why do Code Conventions matter?
- 80% of the lifetime cost of a piece of software goes to maintenance.
- Hardly any software is maintained for its whole life by the original author.
- Code conventions improve the readability of the software, allowing engineers to understand new code more quickly and thoroughly.


#### Programming Best Practices
- Make as little public methods and fields as possible.
- All naming should be done in a self-explanatory way and as short as it could be without conflicting with an explanatory part.
- Numeric and literal constants should not be coded directly in the most cases, magic numbers aren't nice for code readability.
- Avoid assigning several variables to the same value in a single statement, it's hard to read.
- Copy-pasting is evil, if you need the same code in 2+ places than you have to find a way to reuse it, so the logics will be the same in all places.
- Format your code before each commit. ```Ctrl + Alt + L``` for Windows or ```Cmd + Alt + L``` for OS X.
- Keep it simple.

## Open to discussion
If any of convention really bothers you — we can always discuss things and make changes.