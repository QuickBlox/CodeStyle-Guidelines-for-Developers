<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**

- [Resource files naming](#resource-files-naming)
- [Indentation](#indentation)
- [Visual organization](#visual-organization)
- [ID naming](#id-naming)
- [XML attributes ordering](#xml-attributes-ordering)
  - [XML files formating](#xml-files-formating)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### Resource files naming
- All resource file names are written in lowercase_underscore
- For layout files use ```activity_```, ```fragment_```, ```view_```, ```item_``` prefixes, with the name the corresponding class has.
For example, ```SplashActivity``` layout file should be named ```activity_splash```, for ```MoneyView``` layout file name should be ```view_money``` etc.
- Resource files in the values folder should be plural, e.g. ```strings.xml, styles.xml, colors.xml, dimens.xml``` etc.

### Indentation
Four spaces should be used for indentation everywhere, as well as in Java code.

**BAD**
```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="match_parent"
              android:layout_height="match_parent"
              android:orientation="vertical">
```

**GOOD**
```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">
```


### Visual organization
- In the root element first ```xlmns``` declaration sits on the same line with opening tag
- Closing tag should be indented on the same level as an opening tag
- XML element closing ```>``` brace should not contain space before itself
- There should *always* be a space between a statement and ```/>``` brace. 
This helps to visualy separate closed elements and elements that can contain another elements.
- When an XML element doesn't have any content, you *must* use self closing tag

**BAD**
```xml
<!-- Don't do this -->
<RelativeLayout
    android:id="@+id/container"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp">
</RelativeLayout>
```

**GOOD**
```xml
<RelativeLayout
    android:id="@+id/container"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp" />
```


### ID naming
- Resource IDs and names are written in lowercase_underscore style
- IDs should be prefixed with the name of the element in lowercase underscore. For example:

| Element           | Prefix            |
| ----------------- | ----------------- |
| `TextView`        | `text_`           |
| `ImageView`       | `image_`          |
| `Button`          | `button_`         |
| `Menu`            | `menu_`           |
- IDs should also contain a prefix that indentifies the section they belong to. 
For example ```text_registration_username``` or ```image_profile_avatar```.
- View fields, otherwise, should be named with type at the end. 
For example:
```java
private TextView usernameTextView;
private ImageView avatarImageView
```


### XML attributes ordering
1. xlmns:*, starting with xlmns:android
2. android:id
3. style:*
4. android:layout_width
5. android:layout_height
6. android:layout_weight
7. android:layout_*, sorted alphabetically
8. android:*, sorted alphabetically
9. tools:


#### XML files formating
These settings can be achieved by doing:
```
1. Android Studio -> Preferences
2. Editor -> Code Style -> XML
3. Set from -> Predefined Style -> Android
```

Sometimes, after Android Studio restart, formatting settings are broken, you'll need to do this again.