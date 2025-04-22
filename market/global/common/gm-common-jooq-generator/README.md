#JOOQ генератор
Ваш проект должен содержать Liquibase changelog файл с миграциями для Postgress.

При старте поднимет Embedded Postgress, проливает Liquibase миграции и затем,
по получившейся схеме, генерирует POJO и DAO классы для работы с базой.

##Как подключить

1) Создать в своем проекте файл jooq.xml. [Вот пример](https://a.yandex-team.ru/arc_vcs/market/global/partner/src/main/resources/jooq/jooq.xml?rev=r8666239)
1) Создать в проете jooq.ya.make вот с таким содержимым
```
PEERDIR(
    contrib/java/org/jooq/jooq/3.14.4
    contrib/java/org/jooq/jooq-meta/3.14.4
    contrib/java/org/jooq/jooq-codegen/3.14.4
)

SET(JOOQ_XML ${CURDIR}/src/main/resources/jooq/jooq.xml)
SET(LQUIBASE_DIR ${CURDIR}/src/liquibase)
SET(CHANGELOG_XML ${LQUIBASE_DIR}/changelog.xml)
SET(OUTPUT ${BINDIR}/generated)

RUN_JAVA_PROGRAM(
    -Djava.io.tmpdir=${BINDIR} # !!! This is ultimately needed for build not to fail
    -Dliquibase.changelog.file=${CHANGELOG_XML}
    -Djooq.configuration.file=${JOOQ_XML}
    -Djooq.output.dir=${OUTPUT}
    ru.yandex.market.global.jooq.JooqGeneratorApp
    IN_DIR ${LQUIBASE_DIR}
    IN ${CHANGELOG_XML} ${JOOQ_XML}
    OUT_DIR ${OUTPUT}
    CLASSPATH market/global/common/gm-common-jooq-generator
)

JAVA_SRCS(SRCDIR ${OUTPUT} **/*.java)
```
3) Заменить в этом файле пути к JOOQ_XML и CHANGELOG_XML на пути к вашим jooq.xml и Liquibase changelog файлам
3) Добавить jooq.ya.make в основной ya.make
```INCLUDE(ya.make.modules/jooq.ya.make)```
