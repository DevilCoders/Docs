## Transport manager
Компонент, выполняющий оркестрацию перемещения между логистическими точками. Основная документация находится [здесь](https://wiki.yandex-team.ru/delivery/development/apps/tm/)

### Обновленный локальный запуск
1) Запустить `beforelaunch.sh`, находясь в той же директории, в которой лежит скрипт
2) Проверить, что IDEA подтянула конфигурацию(особо уделить внимание пути до пропертей)

Если проект не запустится, то следовать инструкции ниже.

### Локальный запуск
Для запуска компонента необходимо:

1) Заполнить в Spring boot шаблоне опции:
- VM options:  `--add-opens=java.base/java.util=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED`
- Working directory: `$MODULE_WORKING_DIR$`
- Environment variables: `PROPERTIES_DIR=<абсолютный путь до properties.d в arc>`
- Active profiles: `local`
2) Скопировать `application.properties.dist` из local-директории в `application.properties`
3) Перед запуском запустить стабы
`cd dependency-stub && docker-compose up -d`
Для простоты можно настроить конфигурацию с запуском стабов по кнопке.

### Тесты
Для работы тестов необходимо также добавить опцию (проще всего сразу в `Edit configuration templates...` в меню)
- `--add-opens=java.base/java.util=ALL-UNNAMED --add-opens=java.base/java.lang=ALL-UNNAMED`

### Репозиторий
В компоненте используется mybatis.
Мапперы находятся тут: `ru.yandex.market.delivery.transport_manager.repository`.
Xml для них находятся в `resources/mappers`.
Рекомендуется использовать удобный плагин для idea: https://plugins.jetbrains.com/plugin/8321-free-mybatis-plugin

Каждый метод маппера обязательно нужно покрывать интеграционными тестами.
