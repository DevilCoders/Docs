# GradleAspectJ-Android
[![AspectJ](https://img.shields.io/badge/AspectJ-4.3.0-brightgreen.svg)](http://www.eclipse.org/aspectj/) [![Kotlin](https://img.shields.io/badge/Kotlin-1.4.10-blue.svg)](http://kotlinlang.org) [ ![Download](https://api.bintray.com/packages/archinamon/maven/android-gradle-aspectj/images/download.svg) ](https://bintray.com/archinamon/maven/android-gradle-aspectj/_latestVersion)<br />
[![Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-AspectJ%20Gradle-brightgreen.svg?style=flat)](http://android-arsenal.com/details/1/4578) ![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg) [![](https://jitpack.io/v/Archinamon/GradleAspectJ-Android.svg)](https://jitpack.io/#Archinamon/GradleAspectJ-Android) [![GitHub license](https://img.shields.io/badge/license-Apache%20License%202.0-blue.svg?style=flat)](http://www.apache.org/licenses/LICENSE-2.0)

A Gradle plugin which enables AspectJ for Android builds.
Supports writing code with AspectJ-lang in `.aj` files and in java-annotation style.
Full support of Android product flavors and build types.
Support Kotlin, Groovy, Scala and any other languages that compiles into java bytecode.

Actual version supporting of AGP 4.1.+: `com.archinamon:android-gradle-aspectj:4.3.0`.<br />
<br />
Friendly with <a href="https://zeroturnaround.com/software/jrebel-for-android/" target="_blank">jRebel for Android</a>!

This plugin is completely friendly with <a href="https://bitbucket.org/hvisser/android-apt" target="_blank">APT</a> (Android Annotation Processing Tools) and <a href="https://github.com/evant/gradle-retrolambda/" target="_blank">Retrolambda</a> project (but Java 8 not supported in .aj files).
<a href="https://github.com/excilys/androidannotations" target="_blank">AndroidAnnotations</a>, <a href="https://github.com/square/dagger" target="_blank">Dagger</a> are also supported and works fine.

This plugin has many ideas from the others similar projects, but no one of them grants full pack of features like this one.
Nowadays it has been completely re-written using Transform API.

Key features
-----

Augments Java, Kotlin, Groovy bytecode simultaneously!<br />
Works with background mechanics of jvm-based languages out-of-box!<br />
[How to teach Android Studio to understand the AspectJ!](IDE)<br />
May not work properly for AS 3.0 :(

It is easy to isolate your code with aspect classes, that will be simply injected via cross-point functions, named `advices`, into your core application. The main idea is — code less, do more!

AspectJ-Gradle plugin provides supply of all known JVM-based languages, such as Groovy, Kotlin, etc. That means you can easily write cool stuff which may be inject into any JVM language, not only Java itself! :)

To start from you may look at my <a href="https://github.com/Archinamon/AspectJExampleAndroid" target="_blank">example project</a>. And also you may find useful to look at <a href="https://eclipse.org/aspectj/doc/next/quick5.pdf" target="_blank">reference manual</a> of AspectJ language and simple <a href="https://eclipse.org/aspectj/sample-code.html" target="_blank">code snippets</a>. In case aspectj-native not supported by Android Studio (even with IDE-plugin it's using is complicated), you may write a java-classes with aspectj annotations.

Two simple rules you may consider when writing aspect classes.
- Do not write aspects outside the `src/$flavor/aspectj` source set! These aj-classes will be excluded from java compiler.
- Do not try to access aspect classes from java/kotlin/etc. In case java compiler doesn't know anything about aspectj, it will lead to compile errors on javac step.

These rules affects only in case you're writing in native aj-syntax.
You may write aspects in java-annotation style and being free from these limitations.

Usage
-----

First add a maven repo link into your `repositories` block of module build file:
```kotlin
mavenCentral()
```
Don't forget to add `mavenCentral()` due to some dependencies inside AspectJ-gradle module.

Add the plugin to your `buildscript`'s `dependencies` section:
<details open><summary>Kotlin</summary>

```kotlin
classpath("com.archinamon:android-gradle-aspectj:4.3.0")
```

</details>
<details><summary>Groovy</summary>

```groovy
classpath 'com.archinamon:android-gradle-aspectj:4.3.0'
```

</details>

<br />
Apply the `aspectj` plugin:

<details open><summary>Kotlin</summary>

```kotlin
plugins {
    id("com.android.application")
    id("com.archinamon.aspectj")
}
```

</details>
<details><summary>Groovy</summary>

```groovy
plugins {
    id 'com.android.application'
    id 'com.archinamon.aspectj'
}
```

</details>

<br />
Now you can write aspects using annotation style or native (even without IntelliJ IDEA Ultimate edition).
Let's write simple Application advice:

```java
import android.app.Application;
import android.app.NotificationManager;
import android.content.Context;
import android.support.v4.app.NotificationCompat;

aspect AppStartNotifier {

    pointcut postInit(): within(Application+) && execution(* Application+.onCreate());

    after() returning: postInit() {
        Application app = (Application) thisJoinPoint.getTarget();
        NotificationManager nmng = (NotificationManager) app.getSystemService(Context.NOTIFICATION_SERVICE);
        nmng.notify(9999, new NotificationCompat.Builder(app)
            .setTicker("Hello AspectJ")
            .setContentTitle("Notification from aspectJ")
            .setContentText("privileged aspect AppAdvice")
            .setSmallIcon(R.drawable.ic_launcher)
            .build());
    }
}
```

Tune extension
-------
<details open><summary>Kotlin</summary>

```kotlin
aspectj {
    compileTests = true // default value

    ajc = "1.9.4" // default value
    java = JavaVersion.VERSION_1_7 // default value

    /* @see Ext plugin config **/
    includeAllJars = false // default value
    includeJar.addAll(arrayOf("design", "support-v4", "dagger")) // default is empty
    excludeJar.addAll(arrayOf("support-v7", "joda")) // default is empty
    extendClasspath = true // default value

    includeAspectsFromJar.addAll(arrayOf("my-aj-logger-lib", "any-other-libs-with-aspects")) // default is empty
    ajcArgs.apply {
        add("-warn:deprecation")
        add("-referenceInfo")
    }

    weaveInfo = true // default value
    debugInfo = false // default value
    addSerialVersionUID = false // default value
    noInlineAround = false // default value
    ignoreErrors = false // default value
    
    breakOnError = true // default value
    experimental = false // default value
    buildTimeLog = true // default value

    transformLogFile = "ajc-transform.log" // default value
    compilationLogFile = "ajc-compile.log" // default value
}
```

</details>
<details><summary>Groovy</summary>

```groovy
aspectj {
    dryRun false // default value
    compileTests true // default value

    ajc '1.9.4' // default value
    java = JavaVersion.VERSION_1_7 // default value

    /* @see Ext plugin config **/
    includeAllJars false // default value
    includeJar 'design', 'support-v4', 'dagger' // default is empty
    excludeJar 'support-v7', 'joda' // default is empty
    extendClasspath true // default value

    includeAspectsFromJar 'my-aj-logger-lib', 'any-other-libs-with-aspects'  // default is empty
    ajcArgs << '-referenceInfo' << '-warn:deprecation'

    weaveInfo true // default value
    debugInfo false // default value
    addSerialVersionUID false // default value
    noInlineAround false // default value
    ignoreErrors false // default value
    
    breakOnError true // default value
    experimental false // default value
    buildTimeLog true // default value

    transformLogFile 'ajc-transform.log' // default value
    compilationLogFile 'ajc-compile.log' // default value
}
```

</details>

<br />
Note that you may not include all these options!

All the extension parameters are have default values (all of them are described above, except of includeJar/Aspects/ajcArgs options).
So no need to define them manually.

- `compileTests` Workaround to disable `compileDebugUnitTestAspectJ` for unitTest variant

- `ajc` Allows to define the aspectj runtime jar version manually (1.8.12 current)
- `java` What jvmTarget will ajc use to compile bytecode into
- `extendClasspath` Explicitly controls whether plugin should mutate the classpath with aspectj-runtime itself

- `includeAllJars` Explicitly include all available jar-files into -inpath to proceed by AJ-compiler
- `includeJar` Name filter to include any jar/aar which name or path satisfies the filter
- `excludeJar` Name filter to exclude any jar/aar which name or path satisfies the filter
- `includeAspectsFromJar` Name filter to include any jar/aar with compiled binary aspects you wanna affect your project
- `ajcExtraArgs` Additional parameters for aspectj compiler

- `weaveInfo` Enables printing info messages from Aj compiler
- `debugInfo` Adds special debug info in aspect's bytecode
- `addSerialVersionUID` Adds serialVersionUID field for Serializable-implemented aspect classes
- `noInlineAround` Strict ajc to inline around advice's body into the target methods
- `ignoreErrors` Prevent compiler from aborting if errors occurs during processing the sources

- `breakOnError` Allows to continue project building when ajc fails or throws any errors
- `experimental` Enables experimental ajc options: `-XhasMember` and `-Xjoinpoints:synchronization,arrayconstruction`. More details in <a href="https://github.com/Archinamon/GradleAspectJ-Android/issues/18" target="_blank">issue #18</a>

- `buildTimeLog` Appends a BuildTimeListener to current module that prints time spent for every task in build flow, granularity in millis

- `transformLogFile` Defines name for the log file where all Aj compiler info writes to, new separated for Transformer
- `compilationLogFile` Defines name for the log file where all Aj compiler info writes to, new separated for CompileTask

Extended plugin config
-----------------
<details open><summary>Kotlin</summary>

```kotlin
plugins {
    id("com.android.application")
    id("com.archinamon.aspectj-ext")
}
```

</details>
<details><summary>Groovy</summary>

```groovy
plugins {
    id 'com.android.application'
    id 'com.archinamon.aspectj-ext'
}
```

</details>

<br />
Ext config:
- allows usage of `includeJar` and `includeAllJars` parameters, with workaround to avoid `Multiple dex files exception`
- supports `multiDex`
- supports `Instrumented tests`

Currently it has some limitations:
- `InstantRun` must be switched off (Plugin detects IR status and fails build if IR will be found).

Provider plugin config
-----------------
<details open><summary>Kotlin</summary>

```kotlin
plugins {
    id("com.android.application")
    id("com.archinamon.aspectj-provides")
}
```

</details>
<details><summary>Groovy</summary>

```groovy
plugins {
    id 'com.android.application'
    id 'com.archinamon.aspectj-provides'
}
```

</details>

<br />
Plugin-provider may be useful for that cases when you need to extract aspect-sources into separate module and include it on demand to that modules where you only need it.
Therefor this behavior will save you build-time due to bypassing aspectj-transformers in provide-only modules.

You ain't limited to describe as much provider-modules as you need and then include them using `includeAspectsFromJar` parameter in the module which code or dependencies you may want to augment.

With <a href="https://github.com/Archinamon/AspectJExampleAndroid" target="_blank">example project</a> you could learn how to write such provider-module.

DryRun plugin config
-----------------
<details open><summary>Kotlin</summary>

```kotlin
plugins {
    id("com.android.application")
    id("com.archinamon.aspectj-dryRun")
}
```

</details>
<details><summary>Groovy</summary>

```groovy
plugins {
    id 'com.android.application'
    id 'com.archinamon.aspectj-dryRun'
}
```

</details>

<br />
Disables aspectj-compiler and transformation task for the hole project.

Working tests
-------
<details open><summary>Kotlin</summary>

```kotlin
plugins {
    id("com.android.application")
    id("com.archinamon.aspectj-junit")
}
```

</details>
<details><summary>Groovy</summary>

```groovy
plugins {
    id 'com.android.application'
    id 'com.archinamon.aspectj-junit'
}
```

</details>

<br />
Test scope overloads JUnit compilation flow with AJC instead of JavaC. So any aspects has been written within `test` directory will be compiled with all java sources and aspects will weave them if need. 

ProGuard
-------
Correct tuning will depends on your own usage of aspect classes. So if you declares inter-type injections you'll have to predict side-effects and define your annotations/interfaces which you inject into java classes/methods/etc. in proguard config.

Basic rules you'll need to declare for your project:
```
-adaptclassstrings
-keepattributes InnerClasses, EnclosingMethod, Signature, *Annotation*

-keepnames @org.aspectj.lang.annotation.Aspect class * {
    ajc* <methods>;
}
```

If you will face problems with lambda factories, you may need to explicitly suppress them. That could happen not in aspect classes but in any arbitrary java-class if you're using Retrolambda.
So concrete rule is:
```
-keep class *$Lambda* { <methods>; }
-keepclassmembernames public class * {
    *** lambda*(...);
}
```

Known limitations
-------
* You can't speak with sources in aspectj folder due to excluding it from java compiler;
* Doesn't support gradle-experimental plugin;

All these limits are fighting on and I'll be glad to introduce new build as soon as I solve these problems.

License
-------

    Copyright 2015 Eduard "Archinamon" Matsukov.

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
