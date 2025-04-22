# Nginx в Вертикалях

### Как сделать изменения

Конфигурация Nginx у нас раскатывается через пакеты. Их можно найти [тут](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-packages).

Что где лежит:
* [yandex-vertis-config-nginx-common](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-packages/yandex-vertis-config-nginx-common)  - common include, например форматы логов, параметры проксирования;
* [yandex-vertis-config-nginx-front](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-packages/yandex-vertis-config-nginx-front)  - конфиги auto.ru, rabota, banker;
* [yandex-vertis-config-nginx-front-external](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-packages/yandex-vertis-config-nginx-front-external)  - external сервисы, которые открыты в тестинге наружу (например, hub и chat-api);
* [yandex-vertis-config-nginx-front-internal](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-packages/yandex-vertis-config-nginx-front-internal)  - конфиги внутренних сервисов (например, uploader и octopus);
* [yandex-vertis-config-nginx-front-realty](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-packages/yandex-vertis-config-nginx-front-realty)  - конфиги Яндекс.Недвижимости;

Подтягиваем актуальный **trunk**, создаем новый бранч и делаем там необходимые изменения.

Создаем пулл-реквест в репозиторий. Создаем тикет в очередь `VASUP` с этим пулл-реквестом.

Как выглядит процесс выкладки изменений:
- Из пулл-реквест-а собирается новый пакет и выкатывается в тестинг;
- Автор PR-а призывается в тикет, чтобы проверить изменения в тестинге и окнуть деплой прод;
- Если все ок, то пулл-реквест мержится в **trunk** и пакет выкатывается в тестинг и сразу в прод.

### Логи

Посмотреть логи Nginx можно через [Вертикальные логи](../observability/logs/quick-start.md). Все логи Nginx помечаются лейблами:
- `_service=nginx` (если этой внешний балансировщик) или `_service=nginx-int` (если этой внутренний балансировщик)
- `_layer=prod` или `_layer=test` в зависимости от окружения




