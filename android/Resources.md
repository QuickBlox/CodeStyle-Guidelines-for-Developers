<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**

- [AndroidManifest.xml](#androidmanifestxml)
- [Resource files naming](#resource-files-naming)
- [Indentation](#indentation)
- [Visual organization](#visual-organization)
- [Stub data for layouts](#stub-data-for-layouts)
- [ID naming](#id-naming)
- [Styles, Themes, Attributes and Dimens](#styles-themes-attributes-and-dimens)
- [Layout inflation](#layout-inflation)
- [Colors](#colors)
- [XML attributes ordering](#xml-attributes-ordering)
- [XML files formating](#xml-files-formating)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### AndroidManifest.xml
There is no need to include appVersion and appVersionCode to manifest, as they're obtained from build.gradle

### Resource files naming
- All resource file names are written in lowercase_underscore
- For layout files use `activity_`, `fragment_`, `view_`, `item_` prefixes, with the name the corresponding class has.
For example, `SplashActivity` layout file should be named `activity_splash`, for `MoneyView` layout file name should be `view_money` etc.
- Resource files in the values folder should be plural, e.g. `strings.xml, styles.xml, colors.xml, dimens.xml` etc.

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
- In the root element first `xlmns` declaration sits on the same line with opening tag
- Closing tag should be indented on the same level as an opening tag
- XML element closing `>` brace should not contain space before itself
- There should *always* be a space between a statement and `/>` brace. 
This helps to visualy separate closed elements and elements that can contain another elements.
- When an XML element doesn't have any content, you *must* use self closing tag

**BAD**
```xml
<!-- Don't do this -->
<RelativeLayout
    android:id="@+id/layout_container"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp">
</RelativeLayout>
```

**GOOD**
```xml
<RelativeLayout
    android:id="@+id/layout_container"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp" />
```


### Stub data for layouts
- Always use `tools` namespace for stub data in layout files
You can use it with any attribute like `tools:src` for ImageViews and `tools:text` for TextViews
Example:
```xml
<LinearLayout
    style="@style/WeightWidth"
    android:layout_height="wrap_content"
    android:orientation="horizontal">
    
    <ImageView
        android:id="@+id/image_dialog_icon"
        style="@style/ListItemIconStyle"
        tools:ignore="ContentDescription"
        tools:src="@drawable/ic_chat_group" />

    <TextView
        android:id="@+id/text_dialog_name"
        style="@style/DialogNameStyle"
        tools:text="Room name" />
</LinearLayout>
```


### ID naming
- Resource IDs and names are written in lowercase_underscore style
- IDs should be prefixed with the name of the element in lowercase underscore. For example:

| Element           | Prefix            |
| ----------------- | ----------------- |
| `***Layout`       | `layout_`         |
| `TextView`        | `text_`           |
| `ImageView`       | `image_`          |
| `Button`          | `button_`         |
| `Menu`            | `menu_`           |
- IDs should also contain a prefix that indentifies the section they belong to. 
For example `text_registration_username` or `image_profile_avatar`.
- View fields, otherwise, should be named with type at the end. 
For example:
```java
private TextView usernameTextView;
private ImageView avatarImageView
```

### Resource naming
It's a good idea in resource naming follow a simple convention.
What-Where-Description-Size
Let's describe principles:
- WHAT : Indicate what the resource actually represents, often a standard Android view class. e.g. MainActivity -> activity)
- WHERE : Describe where it logically belongs in the app. Resources used in multiple screens use all, all others use the custom part of the Android view subclass they are in. e.g. MainActivity -> main, ArticleDetailFragment -> articledetail
- DESCRIPTION : Differentiate multiple elements in one screen. e.g. title
- SIZE (OPTIONAL) : Either a precise size or size bucket. Optionally used for drawables and dimensions. e.g. 24dp, small

Examples:
- String resources:
```xml
articledetail_title - title of ArticleDetailFragment
feedback_explanation - feedback explanation in FeedbackFragment
```
- Dimensions resources:

| Element           | Prefix               |
| ----------------- | -------------------- |
| `***width`        | `width in dp`        |
| `height`          | `height in dp`       |
| `size`            | `if width == height` |
| `margin`          | `margin in dp`       |
| `padding`         | `padding in dp`      |
| `elevation`       | `elevation in dp`    |
| `textsize`        | `size of text in sp` |

 ```xml
height_toolbar: height of all toolbars
keyline_listtext: listitem text is aligned at this keyline
textsize_medium: medium size of all text
size_menu_icon: size of icons in menu
height_menu_profileimage: height of profile image in menu
```
For long words can use abbreviation:
For example: 
```xml
 <!--PointInformationFragment-->
    <dimen name="pif_info_item_text_margin">35dp</dimen>
    <dimen name="pif_info_item_layout_margin_left_right">20dp</dimen>
```

### Styles, Themes, Attributes and Dimens
- To be short: themes are used for global stuff like apps and activities, and styles are for local stuff, like widgets
- Create MatchParent, WrapContent, MatchWidth, MatchHeight styles and inherit your styles from those. It helps to reduce attributes in layouts.
- Use `app` namespace for custom view attributes
- Use dimens for repeated values, to ensure it'll be easy to change value in one file and not in ten different files
- Treat XML files like you treat java classes: keep it clean, readable and easy to change


### Layout inflation
You should always pass parent to inflator, with `attachToRoot` flag set to false. 
This will allow view to calculate it's `layout_` attributes correctly.
Of course, if there is no parent view, you shouldn't pass any views, pass `null`.

For example, in adapter:
```java
@Override
public View getView(int position, View convertView, ViewGroup parent) {
    ViewHolder holder;
    if (convertView == null) {
        holder = new ViewHolder();
        convertView = inflater.inflate(R.layout.list_item_message_text, parent, false);
        ...
```


### Colors
- It's suggested to write HEX color codes in lowercase
- Try to choose names that will describe purpose of color, not the color itself
For example:
```xml
<color name="color_primary">#ffffff</color>
<color name="color_primary_dark">#d0d0d0</color>
<color name="color_accent">#4ad24d</color>

<color name="background_app_color">#ffffff</color>
<color name="background_chat_color">#f5f6f5</color>

<color name="text_color_primary">#212121</color>
<color name="text_color_white">#ffffff</color>
<color name="text_color_black">#000000</color>
<color name="text_color_light_grey">#dedede</color>
<color name="text_color_medium_grey">#b1b1b1</color>
<color name="text_color_dark_grey">#6e6e6e</color>
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

### XML files formating
These settings can be achieved by doing:
```
1. Android Studio -> Preferences
2. Editor -> Code Style -> XML
3. Set from -> Predefined Style -> Android
```

Sometimes, after Android Studio restart, formatting settings are broken, you'll need to do this again.
Here is the issue in Android Issue Tracker, in version `1.5.1`: https://code.google.com/p/android/issues/detail?id=196833
