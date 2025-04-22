# Observatorium - микро-сервис со всякими полезными штуками

* работа с Juggler и даунтаймами
* визуализация межрелизных зависимостей
* удобые фильтры для Startrek
* прикольный граф из тикетов
* визуализация схемы репликации бд
* удобный поиск по балансерам
* живет здесь observatorium.da.yandex.ru

### Сборка и выкладка
Просто сделать ```ya package direct/infra/observatorium --debian pkg.json``` и выложить пакетик ```yandex-du-observatorium``` на ppcback'и.

### Разработка
Чтобы запустить приложение локально (например, в PyCharm), нужно лишь выставить переменные окружения c токенами и запустить ```app/run_app.py```. Если для отладки новой функциональности какой-нибудь токен не нужен, можно выставить его пустым (список токенов можно посмотреть в ```lib/tools/settings.py```).

    cd ~/arcadia/direct/infra/observatorium
    PYTHONPATH=~/arcadia DIRECT_PPC_STARTREK_TOKEN='...' \
         SOLOMON_ROBOT_OAUTH_TOKEN='...' JUGGLER_TOKEN='...' \
         python2 ./app/run_app.py

P.S. если появляется ошибка при импорте, это значит, что надо раскидать пустые ```__init__.py``` в рабочей копии на пути от корня аркадии до папки с Observatorium, чтобы python увидел модули.
