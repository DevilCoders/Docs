## Общие библиотеки для автотестов вертикальных сервисов

### Настройка проекта

1. Сгенерить код HTTP-клиентов
`mvn clean install -DskipTests`

2. Если Maven не может найти зависимости, например:
`Cannot resolve ru.yandex.qatools.selenium:selenium-grid-client:1.0-SNAPSHOT`

То нужно взять `settings.xml` [отсюда](https://github.com/YandexClassifieds/maven-settings/blob/master/settings.xml) и скопировать к себе в `~/.m2/settings.xml`.
После этого можно вернуться к пункту 1.

3. Запустить Reimport All Maven Project в IDEA.

После мержа новая версия артефактов проекта собирается автоматически.

### Версии
Версия 1.4-SNAPSHOT содержит webdriver4  
Все предыдущие версии с webdriver3

### Модули

1. **commons** общие утильные методы
```
 <dependency>
     <groupId>ru.vertis.tests</groupId>
     <artifactId>commons</artifactId>
     <version>1.0-SNAPSHOT</version>
 </dependency>
 ```
В проекте нужно добавить папку **META-INF** с **aop.xml**
```
<aspectj>
    <aspects>
        <aspect name="io.qameta.allure.aspects.Allure1TestCaseAspects"/>
        <aspect name="io.qameta.allure.aspects.Allure1StepsAspects"/>
        <aspect name="io.qameta.allure.aspects.Allure1AttachAspects"/>
        <aspect name="io.qameta.allure.assertj.AllureAspectJ"/>
        <aspect name="io.qameta.allure.junit4.AllureJunit4ListenerAspect"/>
    </aspects>
    <weaver options="">
        <include within="io.qameta.allure..*"/>
        <include within="org.assertj.core..*"/>
        <include within="org.junit.runner..*"/>
        <include within="any.your.package..*"/>
    </weaver>
</aspectj>
```
где any.your.package..* пакет проекта

2. **сommons-ra** репорт для rest-assured
```
 <dependency>
     <groupId>ru.vertis.tests</groupId>
     <artifactId>commons-ra</artifactId>
     <version>1.0-SNAPSHOT</version>
 </dependency>
```
 3. **guice-junit** базовые модули, провайдеры, рулы для guice
```
 <dependency>
     <groupId>ru.vertis.tests</groupId>
     <artifactId>guice-junit</artifactId>
     <version>1.0-SNAPSHOT</version>
 </dependency>
```
4. **guice-webdriver** то же самое для webdriver
(включает в себя guice-junit)
```
 <dependency>
     <groupId>ru.vertis.tests</groupId>
     <artifactId>guice-webdriver</artifactId>
     <version>1.0-SNAPSHOT</version>
 </dependency>
```
5. **passport-commons** общие рулы и объекты для работы с аккаунтами (нужен для пасспортных модулей)
6. **passport-vertis** клиент для вертикального пасспорта, необходим для создания аккаунта в auto.ru (включает passport-commons)
```
 <dependency>
     <groupId>ru.vertis.tests</groupId>
     <artifactId>passport-vertis</artifactId>
     <version>1.0-SNAPSHOT</version>
 </dependency>
```
7. **passport-yandex** клиент для яндексовского пасспорта, необходим для создания аккаунта в realty.yandex.ru (включает passport-commons)
```
 <dependency>
     <groupId>ru.vertis.tests</groupId>
     <artifactId>passport-yandex</artifactId>
     <version>1.0-SNAPSHOT</version>
 </dependency>
```
8. **diff-matchers** матчеры для организации a/b тестирования
```
 <dependency>
     <groupId>ru.vertis.tests</groupId>
     <artifactId>diff-matchers</artifactId>
     <version>1.0-SNAPSHOT</version>
 </dependency>
```

    
