# android-gradle-maven-deployer
Gradle plugin for deploying Android and Java libraries to [Yandex artifactory](http://artifactory.yandex.net/webapp/).
Version 1.1.

```gradlew uploadArchives```

On local machine will upload to ```$HOME/.yandex-mobdev```, on teamcity
(if ```teamcity``` property in gradle is set with ```maven.username``` and ```maven.password```) will upload to artifactory.

# How to use

## Apply plugin

In top-level build file
~~~ gradle

buildscript {
    repositories {
        maven { url 'http://artifactory.yandex.net/artifactory/public/' }
    }
    dependencies {
        classpath 'com.yandex.android.vertical:deployer:0.1.1'
    }
}
~~~


In module-level build.gradle
~~~ gradle
apply plugin: 'com.yandex.android.vertical.deployer'

//and configure:
yaMavenDeployer {
//options
}
~~~

## Setup group

Define it for all projects
~~~ gradle
allprojects {
  group = 'com.yandex.android.vertical'
}
~~~

Or for one project ```group = 'com.yandex.android.vertical'```

Or in plugin config

~~~ gradle
yaMavenDeployer {
  group = 'com.yandex.android.vertical'
}
~~~

## Define artifactId

By default ```project.name``` is used, you can override it in plugin config:

~~~ gradle
yaMavenDeployer {
  artifactId = 'vertical-core'
}
~~~

## Define version

In project file ```version '0.1.1'```

Or in plugin config:

~~~ gradle
yaMavenDeployer {
  version = '0.1.1'
}
~~~

# Java artifacts

By default, plugin sets ```archives``` property to Android output file,
to enable jar upload, use following option:

~~~ gradle
yaMavenDeployer {
  androidArtifact = false
}
~~~

# Clearing artifacts (Android only)

To avoid artifacts like ```artifactId-release.aar```, ```artifactId-debug.aar```
in repo, plugin clears default artifacts.

To disable this behavior, use following option:

~~~ gradle
yaMavenDeployer {
  androidDoNotClearArtifacts = true
}
~~~

# Uploading as snapshot

By default artifact is pushed to release repository, if you want to push to snapshot repo, just add suffix "-SNAPSHOT" to your version string. Like this: ```version '0.1.1-SNAPSHOT'```.

# How to upload this plugin to maven repository

In build.gradle file set target maven repository url and credentials
~~~ gradle
publishing {
    repositories {
        maven {
            credentials {
                username "yandexmobiledeploy"
                password "yandexmobiledeploy"
            }
            url 'http://artifactory.yandex.net/artifactory/yandex_mobile_releases/'
        }
    }
}
~~~
Run gradle publish

