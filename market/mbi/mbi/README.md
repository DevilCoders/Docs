## MBI

#### Локальный запуск

Проперти, необходимые для локального запуска компонентов, скопированы внутрь компонентов. Их можно найти в директориях `src/main/properties.d/local`.<br>
Для импорта пропертей из [dev-датасорсов](https://github.yandex-team.ru/cs-admin/datasources-ng-dev/blob/master/development/etcd.yml) можно воспользоваться скриптом `dumpDatasources.sh` из корня проекта. Скрипт разложит проперти в файлы `local-datasources.properties` по всем компонентам.<br>
Запускать приложения необходимо с флагами: 
- `-Denvironment=local`
- `-Dconfigs.path=<путь_до_properties.d>`<br>

Тогда проперти из датасорсов будут прорастать автоматически.

