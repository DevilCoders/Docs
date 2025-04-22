# Обработка запросов из AppHost

Данная информация будет полезна в тех случаях, если вы предполагаете использовать перенаправление трафика из AppHost на локальную бету.
Apphost ходит в tunneler, когда вы используете [srcrwr](https://docs.yandex-team.ru/apphost/pages/cgi#srcrwr) в url запроса или в kotik задаете опцию [localRendererSourceRewrites](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/projects/infratest/packages/kotik/README.md#localrenderersourcerewrites-5), которая внутри также использует srcrwr.

### Как AppHost работает с локальной бетой

Локальная бета поднимается за туннелем («публичная бета»), а запросы AppHost к источнику перенаправляются в этот туннель параметром srcrwr.

![Схема работы](./images/general_scheme.png)

### Диагностика проблем

Если при использовании srcrwr страница не открывается, проверьте доступы.

Для диагностики проблемы с доступами получите RequestID вашего запроса и посмотрите его трейс в [SETrace](https://wiki.yandex-team.ru/setrace/). Если под APP_HOST видите ошибку `"Error: timeout"`, вероятно она относится к запросу в tunneler:

![Пример](./images/example_setrace.png)

В этом случае проверьте доступ от хостов в AppHost до tunneler:

1. посмотрите, с какого хоста был отправлен запрос:

    ![Пример определения хоста](./images/host_in_apphost.png)

2. [проверьте](https://puncher.yandex-team.ru/?destination=tun-balancer.si.yandex-team.ru&protocol=tcp&ports=443&rules=exclude_rejected&values=all&sort=destination) в Puncher доступ от этого хоста до tunneler

Если доступа нет, то закажите его.

В других случаях пишите в [infraduty](https://wiki.yandex-team.ru/infraduty/form/).

### Заказ доступов

Во время диагностики вы выяснили хост. Теперь определите, в каком макросе он находится. Для этого найдите этот макрос в [racktables](https://racktables.yandex-team.ru/):

![Пример поиска в racktables](./images/example_search_in_racktable.png)

Найденный `Firewall macro for IP` и есть необходимый вам макрос.

Затем [закажите доступы](./access.md) от этого макроса до балансера.
