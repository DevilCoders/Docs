# Автотесты не работают

Ниже будут описаны примеры того, как именно тесты "ломаются" и даны советы по починке

## Не установлен корневой сертификат { #no-interanl-certs }
### Как проявляется
Тест падает на Class Configuration — потому что не может получить из монги данные тестового пользователя или токены из секретницы.

В консоли или логах встретится **javax.net.ssl.SSLHandshakeException** **PKIX path building failed**.
Примеры:
- ошибка получения из секретницы
   ```text
   - Failed to fetch secret sec-01efxvd1kdn7m8hq41jp412xty
   javax.net.ssl.SSLHandshakeException: PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target
   ```
- ошибка подключения к монге
   ```text
   - Retrieving user from mongo: at-direct-super
   - 1 * Sending client request on thread main
   1 > GET https://mongo-bean-templates.qart.yandex-team.ru/BeanTemplates/TestUsers?filter=%7Blogin%3A%22at-direct-super%22%7D&count=&pagesize=1000
   > Accept: application/json
   
   - javax.ws.rs.ProcessingException: javax.net.ssl.SSLHandshakeException: PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target
   ```

### Решение 1
Установить внутрияндексовый корневой сертификат в доверенное хранилище JVM.

Инструкция в кластере безопасников: для [Windonws](https://wiki.yandex-team.ru/security/ssl/sslclientfix/#windows),
под [MacOS](https://wiki.yandex-team.ru/security/ssl/sslclientfix/#macosx)
и для [Linux](https://wiki.yandex-team.ru/security/ssl/sslclientfi#ubuntu1).

Так же можно посмотреть [нашу инструкцию](../initial-setup/autotests-local-setup.md#java-add-yandex-cert).

Если не помогло — возможно у вас больше одной java-машины и сертификаты вы установили в одну, а тесты запускаете — другой.
В таком случае варианта два:
- установить сертификаты в другую jvm (инструкция та же, но правильные пути к _keytool_ и _cacerts_ надо будет указать руками)
- запускать тесты правильной JVM (указать в конфигурации проекта в IDEA, или переменной JAVA_HOME в консоли)

### Решение 2
Использовать яндексовую сборку Java.

Путь к ней можно узнать командами:
- `ya tool java11 --print-path` — для 11ый версии
- `ya tool java --print-path` — для 8ой

Из пути надо отбросить `/bin/java` и можно использовать при добавлении JDK в проекте IDEA или в качестве JAVA_HOME.

Есть минус: jvm может удалиться — при удалении кеша сборки и сборочных тулов.


## Протух OAuth-токен { #expired-token }
### Как выглядит
Тест падает с **Authorization error**:
```text
{
  "error_code": 53,
  "error_string": "Authorization error
",
  "error_detail": "Invalid OAuth token",
  "DetailMessage": "java.lang.Exception"
}
    at java.base/jdk.internal.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
    at java.base/jdk.internal.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:64)
    at java.base/jdk.internal.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
    at
```
### Что делать
1. Открываем в рукояточнике [данные пользователя](https://direct-handles.qart.yandex-team.ru/testdata/userActions.html)
1. Вбиваем нужный логин из нашего теста, нажимам **Прочитать**
1. Открываем браузер в инкогнито, [логинимся](https://passport.yandex.ru/) тестовым пользователем. **ТЕЛЕФОН НЕ ПРИВЯЗЫВАЕМ**
1. Там же в инкогнито открываем [ссылку](https://oauth.yandex.ru/authorize?response_type=token&client_id=ae99016820074f809e5c268e564bebad) для получения нового токена
1. Разрешаем доступ
1. Вставляем полученный токен на странице рукояточника, жмем **Сохранить**


## Тест работает в акве, но зависает локально {#hangs}
### Пример
Такое встречается для тестов песочницы или некоторых финансовых тестов — они ходят в баланс/паспорт и локально нет дырок.

Для примера, тест песочницы **GetCreditLimitsTest** висит на:
```text
=====REQUEST:=======================================================================================
GET http://blackbox-mimino.yandex.net/blackbox?method=userinfo&login=at-agency-sandbox-3&userip=127.0.0.1&emails=getall&regname=yes&format=json HTTP/1.1
X-Ya-Service-Ticket: 3:serv:CKJ5EOTDhP8FIgcIudZ6EO8B:-----


=====END OF REQUEST:================================================================================
```
Видно попытку подключения к паспорту — локально такой дырки нет, и скорее всего никогда не будет.

### Решение
#### blackbox
В `direct.test.run.properties` есть замена паспорта на нашу прокси:
```text
# Раскомментировать для локального запуска
# direct.passport.blackbox.url=http://ppcdev2.yandex.ru:7088/blackbox
```
Нужно расскомментировать эту строчку


## Странные падения b2b-reports { #b2b-reports }
### Как выглядят
При **локальном** прогоне тест падает с NPE:
```text
STATUS CODE: 200
- Unable to communicate with elliptics, cause: 402 Payment Required...
- ожидаемый отчёт берём из файла в elliptics: http://aqua.yandex-team.ru/storage/get/direct-reports5/2020-12-21-JFcXY/filteringbyeveryfield/responses/1.xml
- полученный отчёт записан в файл в elliptics: http://aqua.yandex-team.ru/storage/get/direct-reports5/2020-12-21-GccNq/filteringbyeveryfield/1.xml
- Unable to communicate with elliptics, cause: 404 Not Found...

java.lang.NullPointerException: Cannot invoke "String.length()" because "s" is null

    at java.base/java.io.StringReader.<init>(StringReader.java:50)
    at ru.yandex.qatools.pagediffer.utils.PageDifferUtils.canonizeXml(PageDifferUtils.java:34)
    at ru.yandex.qatools.pagediffer.document.XmlDocument.canonize(XmlDocument.java:28)
    at ru.yandex.qatools.pagediffer.PageDiffer.diff(PageDiffer.java:20)
    at ru.yandex.autotests.directapi.reports.backtoback.CompareReportsTest.test(CompareReportsTest.java:107)
```
### Решение
Надо включить использование ТСных эталонов.
Для этого в `direct.test.run.properties` раскомментировать:
```text
# Параметр стоит использовать при локальном запуске b2b на бете, чтобы сравнивать с ТСными эталонами
# direct.api5.reports.backtoback.responses.in.indefinite.storage=true
```

## Java не той версии { #bad-java-version }
### Как выглядит
В IDEA — тесты не компилируются. В логах (event или build) встречаются такие сообщения:
```
java: java.lang.UnsupportedClassVersionError: ru/yandex/aqua/project/ProjectAnnotationProcessor has been compiled by a more recent version of the Java Runtime (class file version 56.0), this version of the Java Runtime only recognizes class file versions up to 52.0
```
```
Warning:java: /Users/ppalex/.m2/repository/ru/yandex/aqua/aqua-annotations/2.5.3/aqua-annotations-2.5.3.jar!/ru/yandex/aqua/annotations/project/Aqua.class: major version    56 is newer than 55, the highest major version supported by this compiler.
 It is recommended that the compiler be upgraded.
```
```
java: Compilation failed: internal java compiler error
```
При запуске сборки через maven:
```
[WARNING] Error injecting: ru.yandex.aqua.project.ProjectProcessorPlugin
java.lang.TypeNotPresentException: Type ru.yandex.aqua.project.ProjectProcessorPlugin not present
...
Caused by: java.lang.UnsupportedClassVersionError: ru/yandex/aqua/project/ProjectProcessorPlugin has been compiled by a more recent version of the Java Runtime (class file version 56.0), this version of the Java Runtime only recognizes class file versions up to 55.0
```
```
[ERROR] Failed to execute goal ru.yandex.aqua:aqua-project-generator-plugin:2.5.3:generate-xsl (default) on project directapi-finance: Execution default of goal ru.yandex.aqua:aqua-project-generator-plugin:2.5.3:generate-xsl failed: Unable to load the mojo 'generate-xsl' in the plugin 'ru.yandex.aqua:aqua-project-generator-plugin:2.5.3' due to an API incompatibility: org.codehaus.plexus.component.repository.exception.ComponentLookupException: ru/yandex/aqua/project/ProjectProcessorPlugin has been compiled by a more recent version of the Java Runtime (class file version 56.0), this version of the Java Runtime only recognizes class file versions up to 55.0
```
```
[ERROR] 'dependencyManagement.dependencies.dependency.systemPath' for com.sun:tools:jar must specify an absolute path but is ${tools.jar} @ com.sun.xml.ws:jaxws-ri-bom:2.2.8
```
### Решение
Поменяйте JRE, из под которой работает maven: **IntelliJ IDEA** → **Preferences** → **Build, Execution, Deployment** → **Build Tools** → **Maven** → **Importing** — JDK for importer.
Вместо `Use internal JRE` надо указать 8 или 12+ версию.
Применить настройки, после этого сделать **Reload All Maven Project** (Reimport).

При работе в консоли (через mvn) решается через указанием переменной окружения JAVA_HOME на правильную версию JRE.

Плюс убедитесь, что сами тесты запускаются с нужной java, в **File** → **Project structure**:
- Project SDK — должен быть 8 или 12+
- Project language level — 8
