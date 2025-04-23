# Прочее

### Обновление версии самого Nginx

{% note warning %}

Если вы задумали обновить версию самого Nginx - посоветуйтесь с [opyakin-roman](https://staff.yandex-team.ru/opyakin-roman) или [ibiryulin](https://staff.yandex-team.ru/ibiryulin)

{% endnote %}

Мы используем кастомную сборку Аркадийного Nginx с [правками](https://a.yandex-team.ru/review/2265916/details) для **p0f**. В связи с этим нельзя просто поменять версия на более новую - надо пересобирать пакет из ветки.

### Логи

Логи с Nginx отправляются в [Вертикальные логи](https://docs.yandex-team.ru/classifieds-infra/logs/quick-start) через [fluent-bit-golp](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-ansible/roles/fluent-bit-golp).
В тестинге дополнительно логируем тело запросов.

Пример поиска: [https://grafana.vertis.yandex-team.ru/s/t/3Of-9Dy356SaZr](https://grafana.vertis.yandex-team.ru/s/t/3Of-9Dy356SaZr)

### Бэкап логов

Помимо отправки логов в Вертикальные логи, мы также заливаем их в S3.
Для этого сейчас сделана роль в vertis-ansible `backup-lb-logs`. Она привозит на все балансировщики скрипты для заливки логов в S3.

Скрипт синхронизирует все пожатые логи в S3 в бакет **vertis-backups** в `prod/logs/<hostname>`. На стороне S3 выставлен TTL в год.

### Общие параметры проксирования

В пакете `yandex-vertis-config-nginx-common` привозятся общие инклюды, которые располагаются в `/etc/nginx/include/common`.

Отдельного внимания требуют параметры проксирования:
- `proxy-params-ext-*` используются, если настраиваемый `location` находится в виртуальном хосте, смотрящем наружу (слушают порт 80 или 443);
- `proxy-params-int-*` используется, если настраиваемый `location` находится в виртуальном хосте, НЕ смотрящем наружу (слушают порт 1111). Обычно используется для хостов связанных с auto.ru, так как перед ними есть общий хост проверяющий GDPR;
- `*-with-host.inc` используется для проксирования, где не надо переопределять заголовок `Host` и надо просто проксировать имеющийся;
- `*-wo-host.inc` используется для проксирования, где мы переопределяем заголовок `Host`. Например, если трафик приходит на домен auto.ru, а далее мы его проксируем в сервис, отвечающий по доменному имени af-chat-http.vrts-slb.prod.vertis.yandex.net.

