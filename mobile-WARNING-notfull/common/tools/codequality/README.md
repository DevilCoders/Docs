gradle-android-codequality-plugin
=========================

Плагин для упрощения подключения [Checkstyle](http://checkstyle.sourceforge.net/), [Pmd](http://pmd.sourceforge.net/) при использовании [Gradle](http://www.gradle.org/) и [Android New Build System](http://tools.android.com/tech-docs/new-build-system/user-guide).<br>
Производит базовую настройку тасков для использования с New Build System, предоставляет наборы правил по умолчанию, позволяет переопределять настройки по умолчанию.

###Подключение###

    buildscript {
        repositories {
            mavenCentral()
            maven {url 'http://maven.yandex.net/nexus/content/repositories/yandex_mobile/'}
        }
        dependencies {
            // version can change, see latest version on maven
            classpath ('com.yandex.android.tools:codequality:0.9-SNAPSHOT')
        }
    }

    apply plugin: 'android' // or 'android-library'
    apply plugin: 'codequality'

    repositories {
        mavenCentral()
    }

###Базовое использование###

При запуске сборки в виде

    ./gradlew assembleDebug

запуск соответствующих проверок кода имеет вид

    ./gradlew codequalityDebug

Можно запускать проверки по одной:

    ./gradlew checkstyleDebug
    ./gradlew pmdDebug

Репорты появляются в папке

    $buildDir/reports

###Возможные настройки###
Все настройки выполняются в блоке codequality.

    codequality {

        checkstyle {
            ...
        }

        pmd {
            ...
        }
    }

Все эти таски наследуются от [Source Task](http://www.gradle.org/docs/current/groovydoc/org/gradle/api/tasks/SourceTask.html).<br/>
Также, сам плагин предоставляет две дополнительных настройки для всех плагинов:

    codequality {
        checkstyle {
            xsl '<path-to-xsl-transformation-file>'
            cleanUp false
        }
        // same for pmd
    }

**xsl** - принимает путь к xsl файлу, с помощью которого из xml отчета будет генерироваться html отчет.<br/>
**cleanUp** - если выставлен в false, не очищает файлы конфигурации и xsl преобразования после выполнения тасков. Может быть полезно, если нужно посмотреть их.

Специфичные для тасков настройки можно найти здесь:<br/>
[Gradle Checkstyle docs](http://www.gradle.org/docs/current/dsl/org.gradle.api.plugins.quality.Checkstyle.html)<br/>
[Gradle Pmd docs](http://www.gradle.org/docs/current/dsl/org.gradle.api.plugins.quality.PmdExtension.html)
