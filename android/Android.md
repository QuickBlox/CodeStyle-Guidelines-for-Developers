<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**

- [Ordering](#ordering)
  - [Class member ordering](#class-member-ordering)
  - [Parameter ordering](#parameter-ordering)
- [String constants, naming and values](#string-constants-naming-and-values)
- [Arguments in Fragments and Activities](#arguments-in-fragments-and-activities)
- [Method chain case](#method-chain-case)
- [Long parameters case](#long-parameters-case)
- [Java files naming](#java-files-naming)
- [Logging](#logging)
- [Annotations](#annotations)
- [Package structure](#package-structure)
- [Errors](#errors)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### Ordering
#### Class member ordering
There is no single correct solution for this but using a logical and consistent order will improve code learnability and readability.

It is recommended to use the following order:

1. Constants
2. Fields
3. Constructors or Fabric methods (`start()` for Activities and `newInstance()` for Fragments)
4. Override methods and callbacks (public or private)
5. Public methods
6. Private methods
7. Inner classes or interfaces

If your class is extending and Android component such as an Activity or a Fragment, it is a good practise to order the override methods so that they match the component's lifecycle.

#### Parameter ordering
When programming for Android, it is quite common to define methods that take a Context. 
If you are writing a method like this, then the Context *must* be the *first* parameter.
The opposite case are *callback* interfaces that should always be the *last* parameter.


### String constants, naming and values
- SharedPreferences prefix should be `PREF_`
- Bundle prefix should be `BUNDLE_`
- Fragment Arguments prefix should be `ARGS_`
- Intent extra prefix should be `EXTRA_`
- Intent action prefix should be `ACTION_`

Note that the arguments of a Fragment are also a `Bundle`. 
However, because this is a quite common use of Bundles, we define a different prefix for them.

### Arguments in Fragments and Activities
When data is passed into an Activity or Fragment via Intents or a Bundles, the keys for the different values must follow the rules described in the section above.
When an Activity or Fragment expect arguments, it should provide a static public method that facilitates the creation of the Fragment or activity start.
In the case of `Activity` the method is usually called `start()`, 
for `Fragment` it's named `newInstance()` and it handles the creation of the Fragment with the right arguments, 
for `DialogFragment` it's called `show()` and has `FragmentManager` as it's *first* argument.

*Note 1*: these methods should go at the top of the class before onCreate()

*Note 2*: if we provide the methods described above, the keys for extras and arguments should be private because there is not need for them to be exposed outside the class.

### Method chain case
When multiple methods are chained in the same line, for example when using Builders,
every call to a method should go in its own line, breaking the line before the `.`
```java
Picasso.with(context).load(url).into(imageView);
```

```java
Picasso.with(context)
    .load(url)
	.into(imageView);
```

### Long parameters case
When a method has many parameters or its parameters are very long we should break the line after comma `,`
```java
loadPicture(context, url, imageViewProfilePicture, clickListener, "Title of the picture");
```

```java
loadPicture(context, url, 
		imageViewProfilePicture, 
		clickListener, 
		"Title of the picture");
```

### Java files naming
- For classes that extend an Android component, the name of the class should end with the name of the component; 
for example: `SplashActivity, SignInFragment, QBChatService, ChangePasswordDialogFragment`
- Try to not overlap Android component names in your own classes if not extending, 
i.e. creating class with name `NetworkService` or without extending `Service` class
- When creating activity or fragment that will be a core class in the hierarchy use Base- prefix, i.e. `BaseActivity, BaseFragment`
- Treat acronyms as words. I.e. instead of `XMLHTTPRequest` or `getURL()` write `XmlHttpRequest` and `getUrl()`
- When extending from `Application` class it's suggested to name your class as `App` for it's shortness and readability

### Logging
- As a general rule, we use the class name as tag and we define it as a static final field at the top of the file.
- Errors should be logged with `ERROR`, `WARNING` and `WTF` levels.
- Method calls, full server responses and other useful, but massive volumes of information, should be logged with `VERBOSE` or `DEBUG` levels.
For example:
```java
public class MyClass {
    private static final String TAG = MyClass.class.getSimpleName();

    public myMethod(Exception e) {
        Log.e(TAG, "My error message", e);
    }
}
```

`VERBOSE` and `DEBUG` logs must be disable on relase builds. 
It is also recommendable to disable `INFORMATION, WARNING` and `ERROR` logs but you may want to keep them enable 
if you think they may be useful to identify issues on release builds. 
If you decide to leave them enable, you have to make sure that they are not leaking private information such as email addresses, user ids, etc.

### Annotations
Support annotations can be found [here](https://sites.google.com/a/android.com/tools/tech-docs/support-annotations), they're suggested to use, since they can help to avoid common mistakes

### Package structure
Should look similar to this:
- com.your.package
  - db
  - net
  - service
  - ui
    - activity
    - fragment
    - widget
  - utils
  

### Errors
- Ignoring errors doesn't save your time. 
It'll be spend later, when you'll try to figure out why does app work as not intended
- Don't show system errors for user, make them human-readable