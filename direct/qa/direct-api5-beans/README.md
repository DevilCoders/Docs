# direct-api5-beans

## Для перегенереации бинов:
- Выполнить `mvn clean install`
- Для того, чтобы бины обновились в других модулях, достаточно добавить их в проект Idea вместе с `direct-api5-beans`
с помощью `Maven->Add Maven Projects`
- Для обновления wsdl-ок с беты поменять в `pom.xml` direct.url:

```diff
  --- direct/qa/direct-api5-beans/pom.xml (index)
  +++ direct/qa/direct-api5-beans/pom.xml (working tree)
  @@ -11,7 +11,7 @@

     <properties>
         <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
-        <direct.url>api.test.direct.yandex.ru</direct.url>
+        <direct.url>11051.beta4.direct.yandex.ru</direct.url>
     </properties>`
   ```


## Возможные ошибки и их решения:
- Ошибка вида `'dependencyManagement.dependencies.dependency.systemPath' for com.sun:tools:jar must specify an absolute path but is ${tools.jar}`:

Возникает на 11ой Java, стоит обновить Project SDK на 1.8 или 12 и выше.
- Ошибка `unable to find valid certification path to requested target`:

Добавить сертификат, генерируемый InstallCert.java - [инструкция](https://wiki.yandex-team.ru/direct/api/duty/commonproblems/#oshibkaperesborabinovponovojjwsdl.chto-totamprosertifikatrugaetsja)

