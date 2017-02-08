<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**

- [Reference](#reference)
- [Indentation](#indentation)
- [Braces](#braces)
- [Line length](#line-length)
- [Wrapping lines](#wrapping-lines)
- [Commentaries](#commentaries)
- [Variables declarations](#variables-declarations)
  - [For class level declarations](#for-class-level-declarations)
  - [For method level declarations](#for-method-level-declarations)
  - [Classed and interfaces](#classed-and-interfaces)
- [Statements](#statements)
- [White Space](#white-space)
  - [Blank lines](#blank-lines)
  - [Blank spaces](#blank-spaces)
- [Naming](#naming)
- [Methods](#write Short Methods)
- [Programming practices](#programming-practices)
- [Exception handling](#exception handling)
- [Best Practices](#best Practices)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

#### Reference
Use this reference for android code style :https://source.android.com/source/code-style.html

#### Indentation
Four spaces should be used, tabs need to be avoided, since they can look and behave different on different development machines.


#### Braces
- There should *always* be a space between a statement and `{` brace.
- Every code block (in `if`, `while`, `for` statements) *MUST* be enclosed by braces *even* if the block contains *only one statement*. 
By not doing this, one relies on the code layout for correctness. Bugs are easily introduced this way.


#### Line length
Avoid lines longer than 120-130 characters, since they're not comfortable to work with, even on large displays.


#### Wrapping lines
If an expression does not fit on a single line these principles should be used:
- Break the line after a comma
- Break before an operator
- Prefer higher-level breaks to lower-level breaks
- Usually new line should be aligned at the same level on the previous line
- If any of the above rules damage code readability — just indent 8 spaces instead
- Always keep in mind that line wrapping should be done for the best possible readability

Here are some examples of breaking long method calls:
```java
method(longExpression1, longExpression2, longExpression3,
       longExpression4, longExpression5);

Object result = method(longExpression1,
                       method2(longExpression2,
                               longExpression3));
```

Line wrapping for `if` statements
```java
//BAD INDENTATION
if ((condition1 && condition2)
    || (condition3 && condition4)
    ||!(condition5 && condition6)) {    //BAD WRAPS
    doSomethingAboutIt();               //MAKE THIS LINE EASY TO MISS
}

//GOOD INDENTATION INSTEAD
if ((condition1 && condition2)
        || (condition3 && condition4)
        ||!(condition5 && condition6)) {
    doSomethingAboutIt();
}
```

Ternary expressions can be written in these ways:
```java
result = (condition) ? true : false;
result = (condition) ? true
                     : false;
result = (condition)
         ? true
         : false;
```


#### Commentaries
- Header comments should be avoided as a general rule, except the need for a copyright/license notice
- Try to avoid use of comments to disable some of the code
We use version control systems, so there is no need to comment code to uncomment it later, you can always restore code from VCS
- Use `TODO`, `HACK`, `FIXME` comments if you need to highlight something in the code
- Always try to avoid comments in the code as much as possible, code should be self-explanatory
- Good comments explain "why" and not "how"
- Tricky code should not be commented but rewritten
- There is no need to specify file's author in the beginning. Disable default file header in your IDE. Every change is recorded by VCS anyway

These principles don't relate to Java-doc commentaries. Documentation commentaries have different purpose.


#### Variables declarations

##### Field initialization

Instance variables should be initialized in their declaration if possible. This improves readability of the code and reduces code in the constructor. You can omit explicitly initializing the value if the default initialization value for that type is the desired one.

##### For class level declarations
- One declaration per line is recommended to improve readability
- Always try to use empty line to group variables by their purpose: views/adapters/fragments and other UI related variables, business related models to other models etc.
As an example:
```java
private TextView labelTextView;
private ImageView avatarImageView;
private Button submitButton;

private User user;
private RegistrationModel registrationModel;
private boolean isNewUser;

private BroadcastReceiver sessionReceiver;
private BroadcastReceiver networkChangedReceiver;
```

- Avoid tab indentation between variable type and name, use one space char
- If applicable it's recommended to initialize all variables in the constructor
- You should explicitly initialize the field value only if default value isn't the desired one

##### For method level declarations
- Put declarations only at the beginning of blocks where variables are used in
- Try to avoid local declarations that hide declarations at higher levels by using same name

##### Classed and interfaces
- No space between a method name and the parenthesis `(` starting its parameter list
- Open brace `{` appears at the end of the same line as the declaration statement 
- Closing brace `}` starts a line by itself indented to match its corresponding opening
statement, except when it is a null statement the `}` should appear immediately after the `{`
```java
public class Example {

    public void emptyMethod() {}

    public void nonEmptyMethod() {
        doSomething();
    }

}
```

#### Statements
- Each line should contain *only one* statement
- Braces are used around *all* statements, even single line ones, see Braces part
- `if-else` class of statements should place `else` or `else if` on the same line as the closing brace, divided with one space
```java
if (statement) {
    doSomethingOne();
} else if (otherStatement) {
    doSomethingTwo();
} else {
    doSomethingThree();
}
```

- In `switch` statements `case` should align on the same level as opening `switch`
- After the every statement should be an empty line, except for the ones who falls through
- Every time a case falls through (doesn’t include a break statement), add a comment where the break statement would normally be
Try to avoid these constructions if possible, though, as these are hard to read
```java
switch (string) {
case XYZ:
    doSomethingOne();
	break;
	
case ABC:
    doSomething();
    /* if case should fall through to the next case */
    /* it must be marked with a comment */
    /* otherwise bug may be introduced */
case DEF:
    doSomethingElse();
    break;
	
default:
    break;
}
```

#### Control flow

Test whether you can return from a method instead of testing whether you should execute a block of code.

Instead of:
```java
public  void ... { 
    ...
    if (condition) {
        // long block of code
    }
}
```

write:
```java
public  void ... {
    ...
    if (!condition) {
        return;
    }

    // long block of code
}
```


#### White Space
##### Blank lines
One blank line should be *always* used in the following cases:
- Between static and non-static fields
- Between methods
- Between the local variables in the method and its first statement
- To improve readability between logical sections inside a method

##### Blank spaces
Blank spaces should be used in these cases:
- After a keyword, followed by a parenthesis
Note that a blank space shouldn't be used between a method name and parenthesis. This helps to separate keywords from method calls
```java
if (statement) {}
while (statement() {}
for (Object object : objectList) {}

public void methodOne(parameter) {
    methodTwo(variable);
}
```
- After commas in argument lists
```java
public void methodOne(int first, int second) {
    methodTwo(first, second);
}
```
- All binary operators, except ++ and -- operators
```java
int a = b + c - d;
a++;
```
- After type casts parenthesis
```java
methodOne((int) b);
```


#### Naming
- All naming is done with camel-case, except constants and packages
- Classes should be nouns, with the first letter of each word capitalized
- Interfaces — same as classes
- Methods should be verbs, in mixed case, started with a lowercase letter
- Variables should be short, but meaningful, started with a lowercase letter
- One-character variable names should be avoided except for temporary “throwaway” variables. Common names for temporary variables are `i, j, k, m` and `n` for integers; `c, d` and `e` for characters
- Constants *ALWAYS* should be all uppercase with words separated by underscores
- Avoid s- and m- prefixes in variables names, we ***DO NOT*** use Hungarian notation because all modern IDEs make visual separation for different variables, i.e. static, private/public etc.
- Packages, in general, should contain only letters and dots

#### Write Short Methods

When feasible, keep methods small and focused. We recognize that long methods are sometimes appropriate, so no hard limit is placed on method length. If a method exceeds 40 lines or so, think about whether it can be broken up without harming the structure of the program.

#### Programming practices
- Use interfaces instead of implementations if possible
- Do not forget to syncronize your Singletones objects if the're called from different threads
- Use lazy initialization  to defer creating the object until you need it
- Wherever possible try to use Primitive types instead of Wrapper classes
- @Override annotation should always used when overriding methods
- Negated boolean variable names must be avoided. The problem arise when the logical not operator is used and double negative arises. It is not immediately apparent what `!isNotError` means.
```java
boolean isError; // NOT: isNoError
boolean isFound; // NOT: isNotFound
```
- Singleton classes should return their sole instance through method `getInstance()`, not `get()` or `instance()` or anything else.
- Use Iterators for changing collections size while iterating
- Complex conditional expressions must be avoided. Introduce temporary boolean variables instead
```java
boolean isFinished = (elementNo < 0) || (elementNo > maxElement);
boolean isRepeatedEntry = elementNo == lastElement;
if (isFinished || isRepeatedEntry) {
    // Something
}

// NOT:
if ((elementNo < 0) 
        || (elementNo > maxElement)
		|| elementNo == lastElement) {
	// Something
}
```
- To convert a primitive to a String use String.valueOf(...). Don't use `"" + i` 
- To convert from a primitive use Integer.parseInt(...) and similar
- To be complemented...

#### Exception handling
##### Avoid catching exceptions by:
```java
catch (Exception e) {
    ...
}
```
Don't Catch Generic Exception.

This will not only catch all checked but also all non-checked and runtime exceptions (e.g. IllegalArgumentException, NullPointerException, etc.) which typically indicate problems in the application code and should not be hidden.

##### Don't Ignore Exceptions

It can be tempting to write code that completely ignores an exception, such as:
```java
void setServerPort(String value) {
    try {
        serverPort = Integer.parseInt(value);
    } catch (NumberFormatException e) { }
}
```

Do not do this. While you may think your code will never encounter this error condition or that it is not important to handle it, ignoring exceptions as above creates mines in your code for someone else to trigger some day. 

Acceptable alternatives (in order of preference) are:

-  Throw the exception up to the caller of your method.
```java
    void setServerPort(String value) throws NumberFormatException {
        serverPort = Integer.parseInt(value);
    }
```

-  Throw a new exception that's appropriate to your level of abstraction.
```java
    void setServerPort(String value) throws ConfigurationException {
        try {
            serverPort = Integer.parseInt(value);
        } catch (NumberFormatException e) {
            throw new ConfigurationException("Port " + value + " is not valid.");
        }
    }
```


#### Best Practices

To convert a primitive to a String use String.valueOf(...). Don't use "" + i. To convert from a primitive use Integer.parseInt(...) and similar.

Don't use StringBuffer unless you need threadsafety, use StringBuilder instead. Similarly don't use Vector, use ArrayList.

Code to interfaces instead of specific implementations (Collection or List instead of ArrayList). Never subclass Thread, always pass a Runnable into the constructor instead.

If equals is implemented in a class it is MANDATORY to implement hashCode as well, otherwise HashSets and other classes which rely on the contract of hashCode will not work.

Use enum instead of a bunch of static final int fields. Then you have type safety for related constants and more readable debugging output is possible because you get meaningful names instead of "magic" numbers.

Avoid the use of static methods and attributes if possible. This is not good object oriented programming style and it also makes testing your code more difficult. Testing

You should always write unit tests for your code to verify the behavior of your classes and methods and to make it easier for reviewers to understand what your code does and that you thought about some border cases.

Writing test for all features and bugs verifies the correctness of the code and prevents regressions that might be caused by other changes and fixes.

Unit tests should be written for all bug fixes and new features, as they can easily be run for continuous integration and thus can be used to determine whether a build passes or fails. They are also easily written to test edge conditions and can guarentee inputs and outputs.
