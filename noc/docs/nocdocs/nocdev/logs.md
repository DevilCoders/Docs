# Логи приложений в YT

## Движение логов с высоты птичьего полёта
Большинство приложений развёрнутых на железе NOCDEV (и в будущем в k8s) поставляют логи в [YT][yt-nocdev-logs] через [LogBroker][lb-nocdev-logs].
Для ускорения запросов используется ClickHouse над данными, лежащими в YT (`ClickHouse over YT` или просто `CHYT`)
Процесс поставки можно описать такими шагами:
1. Приложение пишет лог в journald/файл, rsyslog или напрямую по udp:10514 в unified-agent
2. unified-agent забирать логи из описанного источника и отправляет их в LogBroker
3. На стороне YT работает логфеллер, который занимается сбором логов из LB и раскладыванием их по табличкам

Табличка с логом - это таблица YT с логами за определённый период (30min, 1h, 1d ... )</br>

**Важно**
Стоит обратить внимание, что в YT таблицы формируются с задержкой, которая в худшем случае может достигать пары часов.
В связи с этим кластер стоит использовать в качестве источника исторических данных, нежели real-time поток.

### Особый кейс с noc-syslog (или куда пропал all.log)
На вендорское оборудование и switchdev хосты либо нельзя, либо сложно поставить unified-agent и нормально настроить поставку в LogBroker.
Такие источники пишут логи в выделенный кластер syslog-ов за балансером `noc-syslog.yandex.net`.
Дальнейший путь логов с кластера syslog-ов подходит под описание из предыдущего пункта.


# Как быстро найти и грепнуть лог.
Основная точка входа для поиска лога и поиска по найденному логу - это [yql.yandex-team.ru][yqlui]
- Прежде всего, чтобы было меньше вопросов, рекомендую попрактиковаться в [tutorial][yql-tutorial]-е.
- В интерфейсе YQL переходим на левой панельке в `Sources`, дальше нужно от корня пройти до каталога `logs`
- Путь будет таким `/ YT / hahn / logs `, набиваем в `Filter by name` фильтр `noc` (все логи nocdev названы по схеме `nocdev-{appname}-log` есть одно исключение `hbf-access-log`)
- Заходим в каталог с логами одного приложения и спускаемся по иерархии каталогов до табличек. Например `/nocdev-cvs-log/1d`
- Кликнув на любой табличке, можно подставить её путь в запрос, либо вставить новый запрос с `FROM` из этой таблички. (Такой запрос уже можно запустить и посмотреть результат)

Актуальная инструкция с картинками есть в [документации YQL][yqldoc]

## Примеры
Так как поиск производится через `CHYT`, необходимо использовать синтаксис `ClickHouse`. В интерфейсе yql над `path` находится кнопка `New query in SQL syntax`, у неё есть опции (галочка справа)

### Базовый поиск
Пример автоматически сгенерированного запроса.
```SQL
USE chyt.hahn;
SELECT
    `_logfeller_index_bucket`,
    `_logfeller_timestamp`,
    `_rest`,
    `_stbx`,
    `facility`,
    `fromhost`,
    `fromhost-ip`,
    `host`,
    `iso_eventtime`,
    `msg`,
    `severity`,
    `source`,
    `source_uri`,
    `syslog-tag`,
    `timegenerated`,
    `timestamp`
FROM `//logs/nocdev-syslog-log/1d/2022-07-10`
LIMIT 100;
```
Обычно  присутствует наиболее интересное поле `msg`, по которому хочется выполнить поиск. Обрати внимание на `LIMIT 100`, он скорее всего не нужен, удали его.
Грепнуть лог за день или за полчаса можно по соответствующей табличке.</br>
Например все логи за сутки `2022-07-10` для одного хоста `vla1-5s102`
где в `msg` есть вхождение `error` без учёта регистра.

```SQL
USE chyt.hahn;
SELECT
    `host`,
    `iso_eventtime`,
    `msg`
FROM `//logs/nocdev-syslog-log/1d/2022-07-10`
WHERE `host` == 'vla1-5s102'
AND `msg` ilike '%error%';
```

### Грепнуть по нескольким табличкам за раз
Из доки YQL [Обращение к нескольким таблицам в одном запросе][yqlmanytables] сработает для запросов в YT, но не сработает для CHYT.
Для CHYT есть свой раздел в доке YT [ClickHouse over YT (CHYT)][chyt].
На примере выше, грепнуть все получасовые таблицы за 3 часа, для этого используем функцию `concatYtTablesRange`

```SQL
USE chyt.hahn;
SELECT
    `host`,
    `iso_eventtime`,
    `msg`
FROM concatYtTablesRange('//logs/nocdev-syslog-log/30min', '2022-07-11T03:00:00', '2022-07-11T06:30:00')
WHERE `host` == 'vla1-5s102'
AND `msg` ilike '%error%';
```

# Если каких-то логов нет в YQL
Возможно просто нет прав, нужно запросить доступ на чтение каталога с логами в YT. Приходи в дежурный чат.

Или мы просто упустили их во время работы над задачей [NOCDEV-7205](https://st.yandex-team.ru/NOCDEV-7205)</br>
Достаточно завести задачу на подключение и воспользоваться опцией "сделай сам" или "сделайте, пожалуйста".

## Полезное
### Видео с презентации работы схемы
<video src="https://jing.yandex-team.ru/files/kglushen/Logs_pres.mp4"
width="640" height="480" controls="controls">

[Презентация][logs-presentation]

[yt-nocdev-logs]: <https://yt.yandex-team.ru/hahn/navigation?filter=noc&path=//logs>
[lb-nocdev-logs]: <https://lb.yandex-team.ru/logbroker/accounts/noc/nocdev>
[yqlui]: <https://yql.yandex-team.ru?type=CLICKHOUSE>
[yqldoc]: <https://yql.yandex-team.ru/docs/yt/guides/beginners>
[yqlmanytables]: <https://yql.yandex-team.ru/docs/yt/syntax/select#concat>
[chyt]: <https://yt.yandex-team.ru/docs/description/chyt/about_chyt>
[yql-tutorial]: <https://yql.yandex-team.ru/Tutorial/yt_01_Select_all_columns>
[logs-presentation]:<https://nda.ya.ru/t/ClwNXcRC5EU3jC>
