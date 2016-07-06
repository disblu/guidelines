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
