# Создание нового сервиса

1) В [карте сервисов](https://a.yandex-team.ru/arc_vcs/classifieds/services) создать файлы
   - `deploy/service-name.yml`
   - `maps/service-name.yml`
2) создать папку с проектом или сгенерировать скелет по шаблону
3) создать таргет `shiva_service`
4) вызвать `make gen/yaml` для генерации `a.yaml`, используемого CI.
