# Android Guidelines

This guide contains a series of recommendations and rules for android developers. The main purpose is to build maintainable,  scalable, flexible and easy to read code for others developers.

## 1.1 Project structure

The projects should follow the android gradle project structure. Gradle follows the concept of convention over configuration, providing sensible default option values when possible. The basic project starts with two components called “source sets”, one for the main source code and one for the test code. These live respectively in:

 - src/main/
 - src/androidTest/

Inside each of these directories there are subdirectories for each source component. For both the Java and Android plugin, the location of the Java source code and the Java resources are:

 - java/
 - resources/

For the Android plugin, extra files and folders specific to Android:
AndroidManifest.xml

 - res/
 - assets/
 - aidl/
 - rs/
 - jni/
 - jniLibs/

This means that *.java files for the main source set are located in src/main/java and the main manifest is src/main/AndroidManifest.xml

**Note**: src/androidTest/AndroidManifest.xml is not needed as it is created automatically.

Example:
```java
├─ library-foobar
├─ app
│  ├─ libs
│  ├─ src
│  │  ├─ androidTest
│  │  │  └─ java
│  │  │     └─ com/disblu/project
│  │  └─ main
│  │     ├─ java
│  │     │  └─ com/disblu/project
│  │     ├─ res
│  │     └─ AndroidManifest.xml
│  ├─ build.gradle
│  └─ proguard-rules.pro
├─ build.gradle
└─ settings.gradle
```
You can read more about the project structure on the  [Gradles user manual](http://tools.android.com/tech-docs/new-build-system/user-guide)

## 1.2 File naming

### 1.2.1 Class files
Class names are written in [UpperCamelCase](http://en.wikipedia.org/wiki/CamelCase).

For classes that extend an Android component, the name of the class should end with the name of the component; for example: `ChatActivity`, `SettingsFragment`, etc.

### 1.2.2 Resources files

Resources file names are written in __lowercase_underscore__.

#### 1.2.2.1 Drawable files

Naming conventions for drawables:


| Asset Type   | Prefix            |        Example               |
|--------------| ------------------|-----------------------------|
| Action bar   | `ab_`             | `ab_stacked.9.png`          |
| Button       | `btn_`             | `btn_send_pressed.9.png`    |
| Dialog       | `dialog_`         | `dialog_top.9.png`          |
| Divider      | `divider_`        | `divider_horizontal.9.png`  |
| Icon         | `ic_`              | `ic_star.png`               |
| Menu         | `menu_ `           | `menu_submenu_bg.9.png`     |
| Notification | `notification_`    | `notification_bg.9.png`     |
| Tabs         | `tab_`            | `tab_pressed.9.png`         |

Naming conventions for icons:

| Asset Type                      | Prefix             | Example                      |
| --------------------------------| ----------------   | ---------------------------- |
| Icons                           | `ic_`              | `ic_star.png`                |
| Launcher icons                  | `ic_launcher`      | `ic_launcher_calendar.png`   |
| Menu icons and Action Bar icons | `ic_menu`          | `ic_menu_archive.png`        |
| Status bar icons                | `ic_stat_notify`   | `ic_stat_notify_msg.png`     |
| Tab icons                       | `ic_tab`           | `ic_tab_recent.png`          |
| Dialog icons                    | `ic_dialog`        | `ic_dialog_info.png`         |

Naming conventions for selector states:

| State        | Suffix          | Example                     |
|--------------|-----------------|-----------------------------|
| Normal       | `_normal`       | `btn_order_normal.9.png`    |
| Pressed      | `_pressed`      | `btn_order_pressed.9.png`   |
| Focused      | `_focused`      | `btn_order_focused.9.png`   |
| Disabled     | `_disabled`     | `btn_order_disabled.9.png`  |
| Selected     | `_selected`     | `btn_order_selected.9.png`  |


#### 1.2.2.2 Layout files

Layout files should match the name of the Android components that they are intended for but moving the top level component name to the beginning. For example, if we are creating a layout for the `SignInActivity`, the name of the layout file should be `activity_sign_in.xml`.

| Component        | Class Name             | Layout Name                   |
| ---------------- | ---------------------- | ----------------------------- |
| Activity         | `UserProfileActivity`  | `activity_user_profile.xml`   |
| Fragment         | `SignUpFragment`       | `fragment_sign_up.xml`        |
| Dialog           | `ChangePasswordDialog` | `dialog_change_password.xml`  |
| AdapterView item | ---                    | `item_person.xml`             |
| Partial layout   | ---                    | `partial_stats_bar.xml`       |

#### 1.2.2.3 Menu files

Menu files should match the name of the component. For example, if we are defining a menu file that is going to be used in the `UserActivity`, then the name of the file should be `activity_user.xml`

A good practice is to not include the word `menu` as part of the name because these files are already located in the `menu` directory.

#### 1.2.2.4 Values files

Resource files in the values folder should be  in plural (Example: `strings.xml`, `styles.xml`, `colors.xml`, `dimens.xml`, `attrs.xml` )

# 2 Code guidelines

## 2.1 Java language rules

The code styles under this section are **strict rules**, **not guidelines** or **recommendations**.

### 2.1.1 Don't ignore exceptions

**Do not do this!** While you may think your code will never encounter this error condition or that it is not important to handle it, ignoring exceptions as above creates mines in your code for someone else to trigger some day. **You must handle every Exception in your code** in a principled way; the specific handling varies depending on the case.

```java
void setServerPort(String value) {
    try {
        serverPort = Integer.parseInt(value);
    } catch (NumberFormatException e) { }
}
```
### 2.1.2 Don't catch generic exception

You should not do this:

```java
try {
    someComplicatedIOFunction();        // may throw IOException
    someComplicatedParsingFunction();   // may throw ParsingException
    someComplicatedSecurityFunction();  // may throw SecurityException
    // phew, made it all the way
} catch (Exception e) {                 // I'll just catch all exceptions
    handleError();                      // with one generic handler!
}
```
In almost all cases it is inappropriate to catch generic Exception or Throwable . It is very dangerous because it means that Exceptions you never expected (including RuntimeExceptions like ClassCastException) get caught in application-level error handling. **It obscures the failure handling properties of your code,** meaning if someone adds a new type of Exception in the code you're calling, the compiler won't help you realize you need to handle the error differently.

### 2.1.3 Don't use finalizers

Android doesn't use finalizers. In most cases, you can do what you need from a finalizer with good exception handling. If you absolutely need it, define a close() method (or the like) and document exactly when that method needs to be called (see InputStream for an example). In this case it is appropriate but not required to print a short log message from the finalizer, as long as it is not expected to flood the logs.

### 2.1.4 Fully qualify imports

bad `import foo.*;`

good `import foo.Bar;`

Makes it obvious what classes are actually used and the code is more readable for maintainers.

## 2.2 Java style rules

These are conventions for using Android's Java libraries and tools.

### 2.2.1 Use Javadoc Standard Comments


Every file should have a copyright statement at the top, followed by package and import statements (each block separated by a blank line) and finally the class or interface declaration. In the Javadoc comments, describe what the class or interface does.

```java
/*
 * Copyright (C) 2015 The Android Open Source Project
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */

package com.android.internal.foo;

import android.os.Blah;
import android.view.Yada;

import java.sql.ResultSet;
import java.sql.SQLException;

/**
 * Does X and Y and provides an abstraction for Z.
 */

public class Foo {
    ...
}
```

You can read more about it on the Oracle  [Java Doc Guide](http://www.oracle.com/technetwork/java/javase/documentation/index-137868.html)

### 2.2.2 Write Short Methods

When feasible, keep methods small and focused. We recognize that long methods are sometimes appropriate, so no hard limit is placed on method length. If a method exceeds **40 lines** or so, think about whether it can be broken up without harming the structure of the program.

### 2.2.3 Define Fields in Standard Places

Define fields **always** at the top of the file or **immediately** before the methods that use them.


### 2.2.4 Limit Variable Scope

**Keep the scope of local variables to a minimum**. By doing so, you increase the readability and maintainability of your code and reduce the likelihood of error. Each variable should be declared in the innermost block that encloses all uses of the variable.

Local variables should be declared at the point they are first used. Nearly every local variable declaration should contain an initializer. **If you don't yet have enough information to initialize a variable sensibly, postpone the declaration until you do.**

### 2.2.5 Use Spaces for Indentation

Use four (4) space indents for blocks and never tabs. When in doubt, be consistent with the surrounding code.

Use eight (8) space indents for line wraps, including function calls and assignments. For example, this is correct:

good:

```java
Instrument i =
        someLongExpression(that, wouldNotFit, on, one, line);
```

bad:

```java
Instrument i =
    someLongExpression(that, wouldNotFit, on, one, line);
```

### 2.2.6 Follow Field Naming Conventions

- Non-public, non-static field names start with **m**.
- Static field names start with **s**.
- Other fields start with a **lower case** letter.
- Public static final fields (constants) are **ALL_CAPS_WITH_UNDERSCORES**.

Example:

```java
public class MyClass {
    public static final int SOME_CONSTANT = 42;
    public int publicField;
    private static MyClass sSingleton;
    int mPackagePrivate;
    private int mPrivate;
    protected int mProtected;
}
```

#### 2.2.6.1 Class member ordering
Besides there is no standard or a right solution we recommend to follow the next order.

- Constants
- Fields
    - Static variables  (public , protected and private in that order)
    - Instance variables (public, protected and private in that order)
- Constructors
- Override methods
- Public methods
- Private methds

### 2.2.7 Use Standard Brace Style

Example:

```java
class MyClass {
    int func() {
        if (something) {
            // ...
        } else if (somethingElse) {
            // ...
        } else {
            // ...
        }
    }
}
```

good:

```java
if (condition) {
    body();
}
```

acceptable:

```java
if (condition) body();
```

bad:

```java
if (condition)
    body();
```

### 2.2.8 Limit Line Length

Each line of text in your code should be at most **100 characters** long. Import lines can go over the limit because humans rarely see them (this also simplifies tool writing).

### 2.2.9 Treat Acronyms as Words

| Good           | Bad            |
| -------------- | -------------- |
| `XmlHttpRequest` | `XMLHTTPRequest` |
| `getCustomerId`  | `getCustomerID`  |
| `String url`     | `String URL`     |
| `long id`        | `long ID`        |

### 2.2.10 TODO Comments

Use TODO comments whenever the code below is not perfect or is a hot fix.

```java
// TODO: Remove this code after the UrlTable2 has been checked in.
```

## 2.3 XML style rules

### 2.3.1 Closing tags

If the element doesn't have any content,  you must user self closing tags.

good:

```java
<EditText
    android:id="@+id/edit_text_profile"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" />
```

bad:
```java
<EditText
    android:id="@+id/edit_text_profile"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" >
</EditText>
```

### 2.3.2 Resource naming

Resource names are written using snake convention.

Example:

```java
<TextView
    android:id="@+id/text_view_profile"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content" />
```

#### 2.3.2.1 Id Naming

Should be prefixed with the name of the element.

| Element            | Prefix            |
| -----------------  | ----------------- |
| `TextView`           | `text_`             |
| `ImageView`          | `image_`            |
| `Button`             | `button_`           |
| `Menu`               | `menu_`             |

### 2.3.3 String naming

Strings start with a prefix of the section they belong.

| Prefix             | Description                           |
| -----------------  | --------------------------------------|
| `error_`             | An error message                      |
| `msg_`               | A regular information message         |
| `title_`             | A title, i.e. a dialog title          |
| `action_`            | An action such as "Save" or "Create"  |


### 2.3.4 Order of attributes

There is no general rule, but we recommend the next order:

-  View Id
-  Style
-  Layout width and layout height
- Other layout attributes, sorted alphabetically
-  Remaining attributes, sorted alphabetically


# Thanks to

This guide takes information from differences sources,   without them this guide couldn't exists:

[Code Style for Contributors](https://source.android.com/source/code-style.html)

[Android Best Practices](https://github.com/futurice/android-best-practices)

[Stack-overflow](http://stackoverflow.com)
