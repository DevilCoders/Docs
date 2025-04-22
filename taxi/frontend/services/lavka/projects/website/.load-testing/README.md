## Нагрузочное тестирование

### Генерация патронов

Можно использовать YQL скрипт:

```SQL
USE hahn;
PRAGMA yt.InferSchema;
PRAGMA yt.QueryCacheTtl = '2h';

SELECT
    count(request) AS cnt, method, request
FROM range (
    '//home/logfeller/logs/taxi-access-log/1h',
    '2021-12-07T14:00:00',
    '2021-12-07T15:00:00'
)
WHERE http_host = 'lavka.yandex.ru'
    AND method = 'GET'
    AND request != '/ping'
    AND request NOT LIKE '/api/orders/status%'
    AND request NOT LIKE '%.js%'
    AND request NOT LIKE '%.json%'
    AND request NOT LIKE '%.png%'
    AND request NOT LIKE '%.txt%'
    AND request NOT LIKE '%.ico%'
GROUP BY method, request
ORDER BY cnt DESC
```

Где `range` можно выбрать
из [nginx логов](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/taxi-access-log) сервисов такси

Результаты сохраняем в файл `.load-testing/files/nginx-yt-json.txt`

Запускаем генератор патронов исходя из формулы:

- `TOP` — верхнее значение RPS в стрельбах
- `MAX_LOOP = 0.3 * TOP` — максимальное количество одинаковых запросов
- `MAX_AMMO = 10 * TOP` — максимальное количество патронов

```bash
MAX_LOOP=15 \
MAX_AMMO=150 \
node scripts/load-testing/generate-ammo.js \
    .load-testing/files/nginx-yt-json.txt \
    .load-testing/files/ammo.txt
```

### Сброс моков

Чтобы сбросить кэш запросов можно изменить версию в параметре `recordingName` в файле `.load-testing/config.js`.

Второй способ, это вызвать скрипт с инстанса мишени:

```bash
# из папки "/var/www/html/projects/website/"
node scripts/load-testing/flush-api-mocks.js

# перезапускаем приложение
supervisorctl restart npm
```
