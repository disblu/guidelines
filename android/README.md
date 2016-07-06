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
```
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
