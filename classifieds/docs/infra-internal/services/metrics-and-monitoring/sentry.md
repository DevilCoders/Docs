# Вертикальный Sentry

## Адреса:

Тестинг: [https://sentry.test.vertis.yandex.net/](https://sentry.test.vertis.yandex.net/)
Прод: [https://sentry.vertis.yandex.net](https://sentry.vertis.yandex.net)

Авторизация с помощью доменного логина и пароля.


## Используемые ресурсы:

### БД:
  - PGaaS [https://yc.yandex-team.ru/folders/foof1m2t24sjktbjo7ej/managed-postgresql/cluster/mdbpbnp4e0hegc1vgpq5](https://yc.yandex-team.ru/folders/foof1m2t24sjktbjo7ej/managed-postgresql/cluster/mdbpbnp4e0hegc1vgpq5)
  - Redis [https://yc.yandex-team.ru/folders/foof1m2t24sjktbjo7ej/managed-redis/cluster/mdbe5l3ehgrjaeqrod6s](https://yc.yandex-team.ru/folders/foof1m2t24sjktbjo7ej/managed-redis/cluster/mdbe5l3ehgrjaeqrod6s)

Графики: [https://grafana.vertis.yandex-team.ru/d/h3gbTzDZk/sentry?orgId=1&refresh=1m](https://grafana.vertis.yandex-team.ru/d/h3gbTzDZk/sentry?orgId=1&refresh=1m)

# Deploy

На машинах с Sentry работает `ansible-pull`
Плейбуки для прода: [https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/vertis_prod_sentry.yml](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/vertis_prod_sentry.yml)
Для тестинга: [https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/vertis_vtest_sentry.yml](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/vertis_vtest_sentry.yml)


## Особенности инсталляции:
**Docker образ**
 - Добавлены сертификаты (для подключения к PGaaS)
 - Доставлены пакеты для использования ldap.
 - Добавлен statsd_exporter для экспорта метрик.

Конфигурация сервиса и окружение описаны в compose файле и файле env в роли:

[https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/roles/sentry](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/roles/sentry)


Ссылка на Dockerfile: [https://a.yandex-team.ru/arc_vcs/classifieds/infra/admin-dockerfiles/sentry](https://a.yandex-team.ru/arc_vcs/classifieds/infra/admin-dockerfiles/sentry)
Сборка TeamCity: [https://t.vertis.yandex-team.ru/project/VertisAdmin_Sentry?mode=builds#404943](https://t.vertis.yandex-team.ru/project/VertisAdmin_Sentry?mode=builds#404943)

**Pgaas**
Включено расширение citext (Sentry умеет это при инициализации но для этого нужны права суперпользователя).


## Компоненты:

**Sentry Web**:
Конфиг для nginx [https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-packages/yandex-vertis-config-nginx-front/src/etc/nginx/sites-enabled/sentry.vertis.yandex.net](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-packages/yandex-vertis-config-nginx-front/src/etc/nginx/sites-enabled/sentry.vertis.yandex.net)

**Sentry Worker** :
Производит обработку полученных событий.
Запускается как отдельный контейнер.

**Sentry Cron** :
Запускает переодические задачи.
Например: формирование и отправка отчетов.

**queue_exporter** :
Компонент отправляющий метрики, находится в контейнере с Sentry, так как требует окружение и использует некоторые библиотеки самого Sentry.

**statsd_exporter** :
Сторонний сервис для отправки некоторых метрик самого Sentry, запускается в отдельном контейнере на машине.

**Healthcheck** :
Простой скрипт, проверяющий живость Веб-интерфейса.

## Запуск/Остановка/Рестарт:

На машинах с sentry есть systemd unit, можно использовать стандартные команды: `service sentry (stop|start|restart)`

## Восстановление:

Если нужно налить машину с Sentry. Достаточно прогнать плейбуку, и по окончанию проверить, что все сервисы поднялись.
