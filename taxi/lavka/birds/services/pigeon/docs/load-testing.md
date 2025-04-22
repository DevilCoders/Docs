## Нагрузочное тестирование

### Схема работы

- _TC(auto release)_: запускает таску _TC(loadtest)_
- _TC(loadtest)_: сборка и deploy на _TankPod_
- _TankPod_:
    - (раз в 30 секунд) ищем открытый релизный тикет, пока не найдем
    - отбиваем в тикет, что начинаем нагрузочное тестирование
    - раскатываем дамп БД
    - запускаем тесты импорта (всегда insert 50% / update 50%)
        - N строк + баркод + картинка
    - отбиваем в тикет результаты импорта
    - запускаем Firestarter
    - отбиваем в тикет ссылку на Лунапарк

Необходимые доступы и токены на _TankPod_:

- Sandbox
- StarTrek
- AWS

### Генерация патронов

Можно использовать YQL скрипт:

```SQL
USE hahn;
PRAGMA yt.InferSchema;
PRAGMA yt.QueryCacheTtl = '2h';

SELECT
    count(url) AS cnt, method, url, body
FROM range (
    '//home/logfeller/logs/taxi/production/taxi-lavka-pigeon-app-log/1d',
    '2021-11-08',
    '2021-11-12'
)
WHERE url IS NOT NULL
    AND env = 'production'
    AND url != '/api/v1/upload'
    AND url != '/api/v1/import/upload'
GROUP BY method, url, body
ORDER BY cnt DESC
```

Где `range` можно выбрать
из [логов приложения](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/taxi/production/taxi-lavka-pigeon-app-log/1d)

Результаты сохраняем в файл `.load-testing/files/app-yt-json.txt`

Запускаем генератор патронов исходя из формулы:

- `TOP` — верхнее значение RPS в стрельбах
- `MAX_LOOP = 0.3 * TOP` — максимальное количество одинаковых запросов
- `MAX_AMMO = 10 * TOP` — максимальное количество патронов

```bash
pigeon load-testing generate-ammo \
    --source=.load-testing/files/app-yt-json.txt \
    --dest=.load-testing/files/ammo.txt \
    --maxAmmo=500 \
    --maxLoop=15
```

### Сброс моков

Чтобы сбросить кэш запросов можно изменить версию в параметре `recordingName` в файле `src/config/load-testing.ts`.

Второй способ, это вызвать скрипт с инстанса мишени:

```bash
# из папки "/usr/local/app/"
pigeon load-testing flush-api-mocks
```
