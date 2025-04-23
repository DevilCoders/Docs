Dashboard generation
====================

Данный репозиторий содержит инструменты для генерации и загрузки дашбордов для Grafana
на основе yaml конфигураций.

Конфигурационные файлы могут быть найдены здесь https://a.yandex-team.ru/arc_vcs/taxi/infra/infra-cfg-graphs.

См. https://wiki.yandex-team.ru/taxi/backend/graphite/#generacijadashbordov для остальной информации.

Пример команды запуска скрипта генерации (из корня репозитория dashboards):
 ./generate_dashboard_from_yaml <path-to-yaml-config> --upload --verbose

Для запуска понадобится PyYAML и libyaml, на macOS после установки libyaml
нужно установить PyYAML командой  python setup.py --with-libyaml install (подробнее).
Флаг upload означает заливку дашборда в графану, иначе результат будет выдан в виде json на stdout.

Для заливки дашборда должна быть выставлена переменная окружения GRAFANA_TOKEN с вашим OAuth-токеном.

Для получения токена нужно перейти по ссылке
https://oauth.yandex-team.ru/authorize?response_type=token&client_id=9590d99772e74c7386610688d4a5c1b3.

После внесения изменений нужно запустить сборку релиза: https://teamcity.taxi.yandex-team.ru/viewType.html?buildTypeId=YandexTaxiProjects_Tools_InternalPackages_YandexTaxiDashboardss_A, 
а если изменения также влияют на YAML-конфигурации, то поднять версию сабмодуля dashboards в репозитории infra-cfg-graphs.
