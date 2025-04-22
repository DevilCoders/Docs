### Настройка логброкера для выгрузки событий из системы счетов
1) Используем учетку [billing](https://logbroker.yandex-team.ru/lbkx/accounts/billing?page=browser&type=account) в lbkx
   Используем общую т.к.
   * в lbkx трудно заводить учетки
   * в одной проще управлять квотой

2) Чтобы создавать/конфигурировать сущности в учетке нужна любая роль в сервисе [Новый Биллинг](https://abc.yandex-team.ru/services/newbilling/)
   Достаточно роли Разработчик, да и вообще любой.
   В учетке billing-accounts на logbroker Денису dskut@ еще давали явно все права. Но здесь не надо т.к. он руководитель сервиса

3) Создаем топик
   * для теста
   `logbroker -s lbkx schema create topic /billing/test/accounts-events -p 2 --responsible "igogor@, lightrevan@"`
   * для прода
   `logbroker -s lbkx schema create topic /billing/prod/accounts-events -p 2 --responsible "igogor@, lightrevan@"`

4) Выдаем права на запись
   * Продовый tvm lbexporter - 2026552@tvm [ссылка](https://abc.yandex-team.ru/services/newbillingaccountupdater/resources/?search=2026552&view=consuming&layout=cards&show-resource=28379567)
   `logbroker -s lbkx permissions grant --path /billing/prod/accounts-events --subject 2026552@tvm --permissions WriteTopic`

   * Тестовый tvm lbexporter - 2026300@tvm [ссылка](https://abc.yandex-team.ru/services/newbillingaccountupdater/resources/?search=2026300&view=consuming&layout=cards&show-resource=28076897)
   `logbroker -s lbkx permissions grant --path /billing/test/accounts-events --subject 2026300@tvm --permissions WriteTopic`

5) Настройка логфеллера
   Наши конфиги лежат в аркадии:
   logfeller/configs/logs/common_arnold_logs.json
   logfeller/configs/logs/common_arnold_streams.json
   logfeller/configs/logs/common_hahn_logs.json
   logfeller/configs/logs/common_hahn_streams.json

   См пр https://a.yandex-team.ru/review/1824216/details

   * Примечание. В конфигах логфеллера в качестве урла геораспределенной инсталляции используется урл `bs-prod.logbroker.yandex.net`
     Этот урл нигде в доке логброкера не указан, но это то же самое что и `lbkx.logbroker.yandex.net`
     Вопрос зачем традиционно остается открытым.

6) Настройка поставки в YT
   Грузим в hahn и в arnold
   ```bash
   logbroker -s lbkx yt-delivery add --topic /billing/test/accounts-events --yt hahn
   logbroker -s lbkx yt-delivery add --topic /billing/prod/accounts-events --yt hahn
   logbroker -s lbkx yt-delivery add --topic /billing/test/accounts-events --yt arnold
   logbroker -s lbkx yt-delivery add --topic /billing/prod/accounts-events --yt arnold
   ```
