# Обновление MJ
## Что нового
- Обновлена **Java** `11` -> `17`
- Обновлен Spring
    - **Spring Framework** `5.1.6.RELEASE` -> `5.3.18`
    - **Spring Boot** `2.1.4.RELEASE` -> `2.6.6`
    - **Spring Security** `5.1.5.RELEASE` -> `5.6.1`
    - ... и другие библиотеки спринга
- Обновлен **OpenAPI Generator** `5.1.1` -> `5.4.0`
- **Springfox** заменен на **SpringDoc**, как следствие **Swagger 2** заменен на **Swagger 3**
- Обновлены [сопутствующие библиотеки](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/mj/v1/mj_dependency_management.inc)
## Как обновиться
### 1. В *service.yaml* добавить поле `latest_mj_version: true` в блок `java_service`
![](https://wiki.yandex-team.ru/market/development/developer-experience/mj-framework/obnovlenie-mj/.files/image.png)

### 2. Проверить основной и тестовый ya.make
- Убрать из него явное указание версии java: `JDK_VERSION(...)`
- Убрать `INCLUDE`-ы, ссылающиеся на прочие dependency management файлы, во избежание неявного переопределения версий из нашего файла
- Убрать из `PEERDIR` явное задание версий библиотек, которые уже указаны в [dependency management файле](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/mj/v1/mj_dependency_management.inc)
- Убедиться, что у вас есть строки в основном *ya.make*:
  ```
  SET(MJ_VERSION v1)
  INCLUDE(ya.make.modules/modules.ya.make) <- Добавляется автоматически при перегенерации
  INCLUDE(
  ${ARCADIA_ROOT}/market/infra/java-application/mj/${MJ_VERSION}/mj.ya.make
  )
  ```
  В тестовом:
  ```
  SET(MJ_VERSION v1)
  INCLUDE(ya.make.test.modules/test.modules.ya.make) <- Добавляется автоматически при перегенерации
  INCLUDE(
  ${ARCADIA_ROOT}/market/infra/java-application/mj/${MJ_VERSION}/mj.test.ya.make
  )
  ```

### 3. Перегенерировать проект и перезапустить идею
![](https://wiki.yandex-team.ru/market/development/developer-experience/mj-framework/obnovlenie-mj/.files/image-1.png)

### 4. Перейти в *File -> Project Structure...* и поменять версию Java на 17
![](https://wiki.yandex-team.ru/market/development/developer-experience/mj-framework/obnovlenie-mj/.files/image-2.png)

### 5. Кто использовал в своих проектах [FrameworkWebSecurityConfigurer](https://a.yandex-team.ru/search?search=FrameworkWebSecurityConfigurer,,,arcadia,,200&repo=arc), надо будет заменить его на `org.springframework.security.config.annotation.web.configuration.WebSecurityCustomizer`
В логике ничего менять не придется. Суть интерфейса та же, но теперь она предоставляется спрингом.
### 6. Попытаться запуститься и, если это не удастся, то начинать разбираться с ошибками
На этом этапе ознакомьтесь с следующим разделом, а если не нашли решение, приходите в [чат](https://t.me/joinchat/RImGNXqbohFkOTg6).  
*Если быстро не удается решить возникшие ошибки, то всегда можно удалить или перевести в `false` флажок `latest_mj_version`, перегенерировать проект и перезапустить идею.*

## Возможные проблемы и их решения
### class file has wrong version 61.0, should be 55.0
Проблема скорее всего в том, что в идее не выбрали 17 версию java. См. п.4.
### java.lang.NoClassDefFoundError
Проблема в несовместимости каких-то библиотек. У нас появился [dependency management файл](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/mj/v1/mj_dependency_management.inc), в котором собраны совместимые версии библиотек. Он основан на спринговом [dependency management](https://docs.spring.io/spring-boot/docs/2.6.3/reference/html/dependency-versions.html), но многих библиотек нет в аркадии (такие зависимости закомменчены в нашем файле). Многие зависимости мы добавили в аркадию, но далеко не все. Поэтому, если у вас возникла такого рода проблема, то следуйте инструкции:
1. Разобраться, какая библиотека ищет этот класс (Обычно это понятно по стэктрейсу)
2. Вызвать `ya java classpath`. Узнать версию этой библиотеки. Проверить откуда прилетает эта библиотека через `ya java dependency-tree`.
3. Поискать проблемную библиотеку в нашем [dependency management файле](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/mj/v1/mj_dependency_management.inc). Если она закомменчена, то загрузить библиотеку через `ya maven import` и раскомментить в нашем [файле](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/mj/v1/mj_dependency_management.inc). Если она отсутствует, то найти совместимую версию и добавить в наш [dependency management файл](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/mj/v1/mj_dependency_management.inc).

### java.lang.reflect.InaccessibleObjectException
Пример более подробного текста ошибки:
```
java.lang.reflect.InaccessibleObjectException: Unable to make field private final java.time.LocalDateTime java.time.OffsetDateTime.dateTime accessible: module java.base does not "opens java.time" to unnamed module @3327bd23
```
Это означает, что ваш код или код какой-то библиотеки, которую вы используете (например, `GSON`), хочет через reflection получить доступ до non-public элементов.
Начиная с 16 JDK, такое поведение [по-умолчанию запрещено](https://docs.oracle.com/en/java/javase/16/migrate/migrating-jdk-8-later-jdk-releases.html#GUID-7BB28E4D-99B3-4078-BDC4-FC24180CE82B).

Но если очень нужно, то такой доступ [можно разрешить с помощью рантайм опции](https://docs.oracle.com/en/java/javase/16/migrate/migrating-jdk-8-later-jdk-releases.html#GUID-12F945EB-71D6-46AF-8C3D-D354FD0B1781):
```
--add-opens module/package=target-module(,target-module)*
```

Опция позволяет модулю `module` открыть доступ до пакета `package` для модуля `target-module`.
В `target-module` можно указать значение `ALL-UNNAMED`, тогда доступ будет дан для всех неименованных модулей.

Например, чтобы полечить ошибку `InaccessibleObjectException`, связанную с использованием `GSON`, необходимо добавить:
```
--add-opens=java.base/java.lang=ALL-UNNAMED
--add-opens=java.base/java.time=ALL-UNNAMED
```

Добавить это нужно в `ya.make` секцию `GENERATE_SCRIPT`, например:
```
GENERATE_SCRIPT(
    TEMPLATE ${ARCADIA_ROOT}/market/infra/java-application/core/src/main/bin/application-start.sh
    OUT ${BINDIR}/bin/mj-service-start.sh
    CUSTOM_PROPERTY appName mj-service
    CUSTOM_PROPERTY mainClass ru.yandex.market.javaframework.main.ApplicationMain
    CUSTOM_PROPERTY defaultJvmArgs
    -Xmx1g
    -Xms1g
    -Dspring.profiles.active=\$ENVIRONMENT
    --illegal-access=warn
    --add-opens=java.base/java.lang=ALL-UNNAMED
    --add-opens=java.base/java.time=ALL-UNNAMED
)
```

Для тестов, нужно в тестовый `ya.make` добавить следующее:
```
JVM_ARGS(
    --add-opens=java.base/java.lang=ALL-UNNAMED
    --add-opens=java.base/java.time=ALL-UNNAMED
)
```

### *Будем дополнять по мере общения в чате...*

