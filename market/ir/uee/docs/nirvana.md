<!-- markdownlint-disable MD013 MD033 -->
## Кубик Nirvana
[start-and-await-uee-enrichment-process](https://nirvana.yandex-team.ru/alias/start-and-await-uee-enrichment-process)

<span style="color:red">Обновить пример</span>

[Пример](https://nirvana.yandex-team.ru/flow/af01571f-42b5-4616-b8d4-06f731304c69/c312e89c-0cb3-4aee-abd4-8bcccb0ee93d/graph)

Кубик принимает на вход MR-таблицу и JSON с конфигурацией. Работа кубика включает в себя ожидание завершения обогащения и возвращает обогащенную MR-таблицу. Процесс обогащения ничем не отличается от работы через интерфейс.

Для использования кубика необходимо получить специальный **токен** [здесь](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=1d8711512ae2492896b8437885875c94) - он используется для авторизации при обращении к UEE-API.

В логах кубика можно найти, какой номер задачи присвоен вашему процессу. Наш кубик композитный, поэтому необходимо его развернуть и посмотреть лог внутреннего кубика "Wait for UEE enrichment", там внизу будет строка вида
> Requesting enrichment process 325 status...
Вместо 325 будет ваш номер операции, перейти на соответствующую страничку UI можно по ссылке вида https://ir-ui.market.yandex-team.ru/#/uee/task/325 - где в конце нужно подставить ваш номер. Если кубик вызывается от вашего имени, то операция будет доступна на главной странице https://ir-ui.market.yandex-team.ru/#/uee/tasks/

Кубику необходимо передать JSON-ресурс с маппингом названий столбцов на типы выходных данных (в интерфейсе это делается через выпадающие списки). Актуальные доступные маппинги для столбцов можно подсмотреть в [коде сервиса](https://a.yandex-team.ru/arc_vcs/market/ir/uee/uee-api/src/main/java/ru/yandex/market/ir/uee/api/config/TaskConfig.java?blame=true&rev=r8465772). Они отличаются для разных типов обогащения, основные перечислены ниже

**Для обогащения Смартматчером (SM)**
- title
- category_id - идентификатор маркетной категории (hid)
- vendor_id

**Для обогащения Ультраконтроллером**
- title
- description
- price
- vendor
- isbn
- barcode
- params - YML параметры в одном из трех форматов - JSON, табулированный или XML (//пока пытаемся сами внутри подобрать парсер, если будут проблемы - обращайтесь в поддержку//)

Чтобы в результате работы кубика был полный ответ от УК, необходимо включить галку includeUCFullResponse

![full_uc_settings](_assets/full_uc_settings.png)

