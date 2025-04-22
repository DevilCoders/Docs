# Варианты использования

Существует несколько способов использования schema-registry в проекте:

* подключая как внешний jar-пакет
* подключая как код (рекомендуемый способ в реалиях Аркадии)

## Использование schema-registry JAR

1. Создать PR с необходимыми изменениями в proto-файлах.
2. Добиться, чтобы все проверки были зелёными
3. Вмержить PR
4. Определить, в какую версию попали ваши изменения, воспользовавшись [историей](https://a.yandex-team.ru/arcadia/history/classifieds/schema-registry).
5. Дождаться завершения сборки нужной схемы, следить за процессом можно [здесь](https://a.yandex-team.ru/projects/verticals/ci/actions/launches?dir=classifieds%2Fschema-registry&id=build)
6. Подключить свежеопубликованную версию в своем проекте:

    Maven:
    ```xml
    <dependency>
        <groupId>ru.yandex.vertis</groupId>
        <artifactId>schema-registry</artifactId>
        <version>v0.0.5986</version>
    </dependency>

    <dependency>
        <groupId>ru.yandex.vertis</groupId>
        <artifactId>schema-registry-scalapb_2.13</artifactId>
        <version>v0.0.5986</version>
    </dependency>
    ```

    sbt:
    ```build
    libraryDependencies += "ru.yandex.vertis" % "schema-registry" % "v0.0.5986"
    libraryDependencies += "ru.yandex.vertis" %% "schema-registry-scalapb" % "v0.0.5986"
    ```

### Публикация в локальный m2-репозиторий
Во время разработки может понадобится локально собрать и опубликовать jar со схемой.

Для этого можно воспользоваться скриптами из репозитория schema-registry, вызвав их со следующими параметрами:

* Java: `./ci/publish_jar.sh -l java`
* Scala 2.12: `./ci/publish_jar.sh -l scala-2.12`
* Scala 2.13: `./ci/publish_jar.sh -l scala-2.13`

По умолчанию будет собрана и опубликована версия `dev-SNAPSHOT`, но можно задать свою через флаг `-v`.

## Использование schema-registry как кода
После переезда в Аркадию schema-registry лежит в папке [/classifieds/schema-registry](https://a.yandex-team.ru/arcadia/classifieds/schema-registry), и теоретически каждый проект может завязаться на ее код, отказавшись от использования JAR.

Это позволило бы не ждать завершения процесса сборки и публикации схемы при разработке своих сервисов, что порой достигает 30 минут.
Правда придется как-то ограничивать используемые директории как [поиск](https://a.yandex-team.ru/arcadia/classifieds/vs/build.sbt?rev=r9663515#L29) или [недвижимость](https://a.yandex-team.ru/arcadia/classifieds/realty/schema-registry/build.gradle?rev=r9663551#L9) (попутно прикручивая кеширование)

Подобным образом schema-registry также [используется](https://docs.yandex-team.ru/classifieds-infra/verticals-backend/development/schema-registry) в verticals-backend, где скорость сборки обеспечивает bazel.


{% note warning %}

Так как версия schema-registry инкрементится отдельным [коммитом](./ci.md#автоматический-pipeline-после-мержа-pr), сервисы должны дожидаться мержа этого коммита перед сборкой, если они зависят от схемы по коду.

{% endnote %}

