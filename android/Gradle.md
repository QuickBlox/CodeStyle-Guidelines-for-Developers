<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**

- [Main build.gradle](#main-buildgradle)
- [Project build.gradle](#project-buildgradle)
- [Dependencies](#dependencies)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### Main build.gradle
If you project contains 2+ projects in it, it is suggested to specify `compileSdk`, `buildTools`, `minSdk`, `targetSdk` and dependencies versions in the root `build.gradle` file, in the `ext {...}` section, to make sure dependencies version are shared between all projects and are the same.

### Project build.gradle
If specified in the main `build.gradle` file versions may be assigned like these:
```
android {
    compileSdkVersion rootProject.compileSdkVersion
    ...
}

dependencies {
    compile "com.android.support:support-v4:${rootProject.supportV4Version}"
}
```

### Dependencies
- Prefer `jcentral()` over `mavenCentral()`. Android Studio does it by default, because it's faster to operate with
- Prefer remote dependencies over local `*.jar` and `*.aar`, because local libraries are hard to maintain
- Specify exact dependency version, without using `+` sign, because it leads to unrepeatable builds, if dependency library gets an update

**BAD**
```
compile "com.android.support:support-v4:23.+"
```
**GOOD**
```
compile "com.android.support:support-v4:23.1.1"
```