# generate-jooq-with-postgres

Generate-jooq предназначен для кодогенерации классов на основе БД схемы.

На вход принимает 2 файла: 
- jooq.xml - настройки конфигурации кодогенерации
- changelog.xml - корневой ченджлог liquibase скриптов

На выходе генерирует классы и помещает их переданную папку.

## Пример использования:
```
RUN_JAVA_PROGRAM(
    -Dgeneratejooq.jooq.config.path=${CURDIR}/src/main/resources/custom_jooq.xml
    -Dsql.liquibase.changelog=classpath:/sql/content-lab-main.xml
    -Dsql.schema=content_lab
    -Dgeneratejooq.output.path=${BINDIR}/generated
    -Djava.io.tmpdir=${BINDIR}
    ru.yandex.market.generate.jooq.GenerateJooqSpringMain
    OUT_DIR ${BINDIR}/generated
    CLASSPATH market/jlibrary/generate-jooq market/mbo/content-lab/content-lab-db
)
JAVA_SRCS(SRCDIR ${BINDIR}/generated **/*)
```

Если в jooq.xml используются кастомные классы, то можно добавить их к класспасу:
```
RUN_JAVA_PROGRAM(
    -Dgeneratejooq.jooq.config.path=${CURDIR}/src/main/resources/custom_jooq.xml
    ...
    CLASSPATH market/mbo/content-lab/generate-jooq market/mbo/project/custom-classes
)
JAVA_SRCS(SRCDIR ${BINDIR}/generated **/*)
```

## Пример использования для gradle
```groovy
apply plugin: 'mbuild-java'

ext {
    generatedSources = "${buildDir}/generated/src/java/"
}

sourceSets {
    generated {
        java.srcDir generatedSources
    }
}

configurations {
    generated
}

dependencies {
    compile project(":content-lab-db")
    compile "ru.yandex:generate-jooq:${revision}"

    generated "org.jooq:jooq"
    generated "org.jooq:jooq-meta"
    generated "javax.validation:validation-api:2.0.1.Final"
    generated "com.google.code.findbugs:jsr305:3.0.1"
}

task generateJooq(type: JavaExec) {
    systemProperty 'generatejooq.jooq.config.path', "${projectDir}/jooq.xml"
    systemProperty 'sql.liquibase.changelog', "classpath:/sql/content-lab-main.xml"
    systemProperty 'sql.schema', "content_lab"
    systemProperty 'generatejooq.output.path', generatedSources
    main = 'ru.yandex.market.generate.jooq.GenerateJooqSpringMain'
    outputs.dir(generatedSources)
    classpath = sourceSets.main.runtimeClasspath
}

checkstyle {
    checkstyleGenerated.exclude '**/ru/yandex/market/clab/db/jooq/generated/**'
}

compileGeneratedJava {
    dependsOn(generateJooq)
    classpath = configurations.generated
}

task generatedJar(type: Jar, dependsOn: 'generateJooq') {
    group 'build'
    baseName = "content-lab-jooq-generated"
    from sourceSets.generated.output
}

artifacts {
    generated generatedJar
}

build.dependsOn generatedJar
```
А дальше в другом модуле:
```groovy
dependencies {
    compile project(path: ':content-lab-jooq', configuration: 'generated')
}
```
