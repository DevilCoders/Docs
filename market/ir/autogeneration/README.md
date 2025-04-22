# Autogeneration

В данном репозитории содержатся 4 компонента:

autogeneration-api, gutgin-tms, contentreceiving-api и psku-post-processor

Сборка и выкладка компонентов autogeneration-api, gutgin-tms, contentreceiving-api происходит в
CD-pipeline https://tsum.yandex-team.ru/pipe/projects/ir/delivery-dashboard/autogeneration_tms_cd_arcadia

Сборку и выкладку компонента psku-post-processor нужно производить через релизный пайплайн в ЦУМе:
https://tsum.yandex-team.ru/pipe/projects/ir/delivery-dashboard/autogeneration_cd_arcadia

# Как работать с проектом в аркадии

1) Для начала нужно настроить все для аркадии по гайду https://docs.yandex-team.ru/devtools/intro/quick-start-guide
2) Создать папку за границами аркадии для хранения временных файлов проекта, например ~/projects/autogeneration-arcadia
3) Сгенерировать проект: ya ide idea --stat --yt-store --group-modules tree --with-content-root-modules
   --with-common-jvm-args-in-junit-template --local -r ~/projects/autogeneration-arcadia
4) После генерации проекта в консоле будет инструкция как настроить аркадийный стиль
5) Открыть (не импортировать) проект в IDEA в папке ~/projects/autogeneration-arcadia
6) Для локального запуска тестов использовать ya make -tt (это аналог ./gradlew build)
7) Тесты в дебаге запускаются так же, как и при работе с градлом

# Локальный запуск компонент

* у каждого компонента в корневом пакете есть main-класс (см. AutogenerationApiMain, ContentReceivingApiMain, ...)
* для запуска необходимы 2 переменные окружения:
    * **PROPERTIES_DIR** - путь к каталогу **properties.d** соотетстующего сериса
    * **ENVIRONMENT** - назание окружения, которое определяет каталог для загрузки настроек **внутри** каталога **PROPERTIES_DIR**

# Обновление JOOQ-маппингов

* БД гутгина: ./updateGGJOOQ.sh
* БД psku-post-processor: ./updatePPPJOOQ.sh

При добавлении новых моделей не забыть добавить новые файлы (см. скрипты).

# Тесты
## Периодически "падающие" тесты
В большинстве тестов используется embedded-pg, который не всегда корректно завершает свою работу.
В этом случае часть тестов может "падать" из-за непустой БД.
Чаще всего помогает ручное завершение embedded-pg:
* результат команды: **ps aux | grep postgres** не должен содержать процессов embedded-pg
* если такие процессы есть, то их нужно "убить": kill -9 <PID>
