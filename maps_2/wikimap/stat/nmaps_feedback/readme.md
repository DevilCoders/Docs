# Отчет Метрики Фидбэка

Этот скрипт расчитывает отчет [Метрики фидбэка](https://stat.yandex-team.ru/Maps.Wiki/Others/NmapsFeedback) о полезности и скорости разбора фидбэка.

На основе части этого отчета составлен [дашборд](https://datalens.yandex-team.ru/71ela79srnhq3-fidbek-iz-form) по фидбэку из форм (fbapi).

## Регулярный расчет

Реактор: https://reactor.yandex-team.ru/browse?selected=1849843

Нирвана: https://nirvana.yandex-team.ru/flow/c1edfee5-ac5b-4c24-a4d0-866c85f89e61

## Ручной запуск

Выполняется из `bin/local_run` после `ya make`. Требует наличия токенов YT, stat и AB с нужными правами (есть в [секретнице robot-wikimap](https://nda.ya.ru/t/VVoUk0WH3WKMMX)). Стоит использовать последнюю доступную `--dump-date` (*вчерашнюю*) независимо от расчитываемых дат: требуюся дампы [пользователей (nmaps-users-dump-log)](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/logfeller/logs/nmaps-users-dump-log/1d) и [fbapi-issue](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/core/nmaps/analytics/feedback/fbapi).

Перерасчет с 21 по 25 июля включительно:
```
STATFACE_TOKEN=`ya vault get version --only-value robot-wikimap-stat-token sec-01cpqs004vh9nxcv6p26zk4k9b` \
YT_TOKEN=`ya vault get version --only-value robot-wikimap-yt-token sec-01cpqs004vh9nxcv6p26zk4k9b` \
./local_run --from-date 2020-07-21 --to-date 2020-07-25 --statface-prod --dump-date 2020-08-02
```

## Дополнительные размерности для фидбэка из FBAPI

Для фидбэка из источников **fbapi** и **fbapi_sprav** размерность **source_path** выглядит так:

`'_total_' > 'fbapi' >  ('toponym|sprav') > client_id > form_id > form_type [ > form_context_id > application_version]`

*Последние 2 уровня этого дерева могут отсутствовать.*

Для **fbapi** к основным данным join-ится [дамп, содержащий данные fbapi-issue](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/maps/core/nmaps/analytics/feedback/fbapi&). Для **fbapi_sprav**: [YT-реплика feedback-int](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/dynamic/replica/fbapi).

Описание полей fbapi-issue: [тут](https://github.yandex-team.ru/maps/feedback-int/blob/master/docs/README.md).

## Особенности

Вопрос о качестве потока фидбэка решается через подсчёт метрик по различным группам фидбэк-заданий. Исходное дизайн-решение (и состояние на данный момент) в том, чтобы считать их на группе фидбэка, **разобранного** в день X. Это позволяет накапливать метрики аддитивно по дням -- метрики в прошлом не изменяются при перерасчете.

В качестве альтернативы в данном случае можно было бы считать качество на основе фидбэка, **созданного** в день X. С некоторой точки зрения это лучше бы отвечало реальности -- можно делать предположение о локальности качества по времени создания; по времени разбора -- вряд ли. То есть, если у нас изменилось качество источника фидбэка (начиная с какого-то определенного дня), то это может быть явно заметно на графике качества по времени создания фидбэка; по времени разбора это будет значительно размазано.
Но недостаток этого подхода как раз в том, что надо пересчитывать данные в прошлом, по мере разбора фидбэка.

Это в большей степени относится к метрикам по дням. Расчет метрик в окнах сглаживает недостатки обоих подходов. Правда, не исчезает вопрос того, как строить выборку фидбэка для подсчета.
