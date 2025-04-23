# SearchSPA в fiji

## Запуск тестов Картинок/Видео с использованием SearchSPA
В fiji есть возможность запустить имеющиеся тесты для AJAX-переходов с `web4`. Эта возможность реализована с помощью проксирования в хамстер и изменением команы `goURL`.

Для удобства можно пользоваться командами:
- `npm run hermione:gui:spas:images`
- `npm run hermione:gui:spas:video`
Они включают всё необходимое для быстрого запуска.

Полезные переменные окружения для тестов:
- `SPAS_TEST=1` — включает запуск тестов с использованием `SearchSPA`.
- `SPAS_SCRIPT_SRC` — позволяет заменить в тестах путь до статики `search-spa`.

## Запуск Картинок/Видео и Веб-поиска для локальной разработки
В fiji есть возможность проксировать запросы в другую локальную бету, позволяя запускать на одном хосте и Картинки/Видео, и Веб-поиск. Это нужно для удобной отладки AJAX-переходов с использованием `SearchSPA`.

Как пользоваться:
1. запускаем fiji командой `PROXY_SERVICE=web4 npm run dev`. По умолчанию запросы `web4` проксируются на хамстер, это можно изменив с помощью переменной окружения `PROXY_WEB4_ORIGIN`.
2. Для локального запуска `web4` одновременно с картинками нужно изменить порт (нужно установить свойство `--port` в команде запуска), так же потребуется подменить dns-port: `npm run dev -- --dns-port 8882`. (Если параметры не подходят, то можно попробовать префикс `--kotik-{свойство}`)
3. теперь web4 доступен на ориджине fiji: https://${хост}:3333/search/touch?text=котики - прокируется в локальную бету поиска

## Ссылочки
1. Middleware для kotik, обеспечивающая проксирование https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/fiji/.config/kotik/middlewares/proxy-service.js
2. Хелперы для сервера https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/fiji/sakhalin/src/spas/server/bem.ts
3. Код команды `SearchSPA` перехода для тестов https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/fiji/runner/hermione/commands/goSPASUrl.js