# Apphost в Морде

Ликбез экспромтом про то, с чем и как работает Аппхост и откуда он берёт графы и бэкенды: [запись с Зума](https://moderator.video.yandex-team.ru/m/film-info?service=video-nda&n=8449)

## Список nanny-сервисов аппхоста для морды
https://nanny.yandex-team.ru/ui/#/services/catalog/stable-portal-apphost-sas/
https://nanny.yandex-team.ru/ui/#/services/catalog/stable-portal-apphost-man/
https://nanny.yandex-team.ru/ui/#/services/catalog/stable-portal-apphost-vla/
https://nanny.yandex-team.ru/ui/#/services/catalog/stable-portal-app-apphost-sas/
https://nanny.yandex-team.ru/ui/#/services/catalog/stable-portal-app-apphost-man/
https://nanny.yandex-team.ru/ui/#/services/catalog/stable-portal-app-apphost-vla/
https://nanny.yandex-team.ru/ui/#/services/catalog/portal-hamster/
https://nanny.yandex-team.ru/ui/#/services/catalog/testing-portal-apphost/

https://nanny.yandex-team.ru/ui/#/services/catalog/stable-avocado-apphost-vla/
https://nanny.yandex-team.ru/ui/#/services/catalog/stable-avocado-apphost-man/
https://nanny.yandex-team.ru/ui/#/services/catalog/stable-avocado-apphost-sas/
https://nanny.yandex-team.ru/ui/#/services/catalog/hamster-avocado-apphost/
https://nanny.yandex-team.ru/ui/#/services/catalog/testing-avocado-apphost/


## Конфиги аппхоста {#apphost-configs}
Конфиг аппхоста и его http_adapter'а собирается [combinator'ом](https://a.yandex-team.ru/arc/trunk/arcadia/apphost/conf/combinator)
* [Список вариантов конфигов по ctype](https://a.yandex-team.ru/arc/trunk/arcadia/apphost/conf/combinator/configs_source/gen_config.json)
* Конфиги собираются из частей, расширяя основной конфиг по [инструкции](https://a.yandex-team.ru/arc/trunk/arcadia/apphost/conf/combinator/configs_source/config_specs/app_host_json.json?rev=r8456140#L21)

https://a.yandex-team.ru/arc/trunk/arcadia/apphost/conf/combinator/configs_source/pieces/app_host/installation/morda.json

## Как собрать панель в Головане {#how-to-generate-panel-in-golovan}

У Дзена есть [удобный скрипт](https://wiki.yandex-team.ru/zen/tech/Rekomender-pod-apxostom/#kaksgenerirovattipovojjdashborddljagrafa) для генерации панелек. Чтобы не трогать их репозиторий и сохранять описания графов, в Морде есть [форк](https://github.yandex-team.ru/morda/zen).

1. Склонируйте Git-репозиторий Дзена:
    ```
    git clone https://github.yandex-team.ru/morda/zen.git
    ```

2. Убедитесь, что у вас установлен Python второй версии. Говорят, что с третьим Питоном скрипт не работает.
    ```
    $ python -V
    Python 2.7.12
    $ python2 -V
    Python 2.7.12
    $ python3 -V
    Python 3.5.2
    ```
    Команда `python` служит alias'ом для второй или третьей версии интерпретатора в зависимости от конфигурации и свежести ОС.
3. Установите недостающий пакет `click`:
    ```
    pip2 install click
    ```
4. Откройте файл [`scripts/apphost_alerts.py`](https://github.yandex-team.ru/recommender/zen/blob/master/scripts/apphost_alerts.py), добавьте в переменную `GRAPHS` описание графа и его вершин, для которого нужно собрать панельку. Пример для графа, обслуживающего запросы из ПП:

    ```python
    Graph(name="morda_searchapp",         # Имя графа в Horizon.
          pronounce="м+орда сёрч апп",    # Как будет произносить Железная тётка имя графа в звонках. Через плюс можно указать ударение.
          owner="yanykin",          
          sources=[
              Source("PERL_SRC_SETUP",              # Имя вершины в графе.
                  pronounce="перл эсэрц+э сет+ап",  # Произношение Железной тёткой.
                  is_important=True,                # Источник графа на главном пути исполнения графа, его неответ приводит к неответу всего графа. Таймаут такого источника не будет учитываться в сигнале графа про 5xx
                  with_hedgeds=True,                # Источник графа с включенными hedged запросами, на его график ошибок будет добавлен сигнал HedgedRequests
                  need_alerts=True,                 # Для источника нужно создать алерты на ошибки
              ),
              Source("PERL_LEGACY",        pronounce="перл л+егаси",           is_important=True, with_hedgeds=True, need_alerts=True),
              Source("PERL_INIT",          pronounce="перл ин+ит",             is_important=True, with_hedgeds=True, need_alerts=True),
              Source("PATCHER",            pronounce="п+атчер",                is_important=True, with_hedgeds=True, need_alerts=True),
              Source("TOPNEWS_SUBGRAPH",   pronounce="подгр+аф Новостей",      is_important=True, with_hedgeds=True, need_alerts=True),
              Source("SHORTCUT_SRC_SETUP", pronounce="шотк+ат эсэрц+э сет+ап", is_important=True, with_hedgeds=True, need_alerts=True),
          ],
          vert="MORDA",
          prj="morda"),
    ```
   Не забудьте закоммитить внесённые изменения в список графов. 
5. Запустите скрипт, указав имя желаемого графа и инсталляцию `ctype`. В примере явно указан Python второй версии:
    ```
    $ python2 apphost_alerts.py create morda_searchapp --ctype prod
    Created panel https://yasm.yandex-team.ru/panel/yanykin.prod-morda_searchapp
    ```
6. Панельки генерируются с тэгом `itype=apphost`, но для некоторых графов сигналы приходят с другим значением. Например, граф `top_news` обслуживается Аппхостом на хостах Геохелпера, поэтому тэгом будет `itype=geohelper`. В этом случае нужно отредактировать полученный шаблон панели в Головане как JSON и заменить все вхождения `itype=apphost` на `itype=geohelper`.
