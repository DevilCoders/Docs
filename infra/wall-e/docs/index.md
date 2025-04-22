
![wall-e.gif](_assets/wall-e.gif)

# Wall-E

[Wall-E](https://wall-e.yandex-team.ru/) - это Hardware as a Service для вашего кластера: высокоуровневая надстройка над сервисами управления железа в Яндексе ([Бот](https://wiki.yandex-team.ru/bot), [RackTables](https://wiki.yandex-team.ru/NOC/RackTables), [Einstellung](https://wiki.yandex-team.ru/einstellung), [Setup/LUI](https://setup.yandex-team.ru/)), которая предоставляет единый API для работы с машинами, отданными в разные проекты и находящимися под управлением разных наливочных систем ([Einstellung](https://wiki.yandex-team.ru/einstellung), [Setup/LUI](https://setup.yandex-team.ru/)), единая точка, в которую приходят запросы на проведение каких-либо действий с машиной, которая берет на себя все заботы по взаимодействию с остальными системами управления железом в Яндексе - в том числе по синхронизации данных действий.

В Wall-E реализованы основные сценарии работы с железом, начиная от его преднастройки, имея только информацию о закупленных серверах, и заканчивая сопровождением этих серверов, переводом из одного проекта в другой, а также автоматической починкой машин через ребут/переналивку.

Более подробное описание текущей реализации можно найти в [инструкции по работе с Wall-E](guide/general.md).

По всем вопросам можно обращаться в [st:/WALLESUPPORT](https://st.yandex-team.ru/WALLESUPPORT).


## Ссылки

[Production Wall-E](https://wall-e.yandex-team.ru/)
[Wall-E API](https://api.wall-e.yandex-team.ru/)

[Prestable Wall-E](https://wall-e-test.yandex-team.ru/)
[Prestable Wall-E API](https://api.wall-e-test.yandex-team.ru/)

## Документация
[Автоматика Wall-E](automation/general.md)
[Интеграция Wall-E с CMS проекта](cms/general.md)
[JSON-schema последней версии CMS API](cms/v1.4.md)
[Бандл wall-e проверок для juggler-а](checks_bundle.md)

## Поддержка
[walle-emergency@](https://telegram.me/joinchat/BvdM3T9IC0GFEcqdw--ArA) -- конференция в telegram, *только про факапы*;
[st:/WALLESUPPORT](https://st.yandex-team.ru/WALLESUPPORT) -- очередь поддержки в трекере;
[st:/BURNE](https://st.yandex-team.ru/BURNE/) -- тикеты на починку хостов для владельцев проектов;

## Очередь задач
[st:/WALLE: Разработка бэкенда](https://st.yandex-team.ru/WALLE/)
[st:/WALLEUI: Разработка фронтенда](https://st.yandex-team.ru/WALLEUI/)

## Мониторинг
[Основные метрики бэкенда](https://yasm.yandex-team.ru/template/panel/wall-e-metrics/ctype=prod)
[Метрики по проверкам здоровья хостов](https://yasm.yandex-team.ru/template/panel/wall-e-health-checks-statuses/ctype=prod)
[События от Juggler](https://yasm.yandex-team.ru/template/panel/wall-e-juggler-push/)
[Дашборд в Juggler](https://juggler.yandex-team.ru/dashboards/wall-e/)

## Рядом стоящие проекты
[Няня](https://wiki.yandex-team.ru/runtime-cloud/nanny/)
[Juggler](https://docs.yandex-team.ru/juggler/)
[Netmon](https://wiki.yandex-team.ru/netmon/)
