## Собирает статистику скринтестов Белого фронта

Минимальный набор переменных окружения для запуска шедулера:

- `STARTREK_TOKEN` – токен робота в Стартреке, от лица которого будем удалять комментарии.

- `TRACKER_FILTER` – фильтр Стартрека по которому ищем список тикетов. Например, `Queue: MARKETFRONT and Status: Open`.

- `ROBOTS_NAMES` – никнеймы роботов через точку с запятой `;`, комментарии которых будем парсить. Например, `robot-metatron,robot-market-infra`.

- `FEATURES` – уникальные признаки комментариев через точку с запятой `;`. По ним отличаем комментарии с прогонами gemini-тестов. Например, `%%prestable-touch%%;%%prestable-desktop%%`

- `YT_TOKEN` - токен с правами для записи в таблицу `https://beta.yt.yandex-team.ru/hahn/navigation?navmode=acl&path=//home/market/users/lengl/screentest_stat&`. (https://nda.ya.ru/t/r2VjtkUu3Vx935)
