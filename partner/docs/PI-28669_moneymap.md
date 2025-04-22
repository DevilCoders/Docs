### Структура

#### Код
Что лежит в каждой папке описано [по ссылке](https://wiki.yandex-team.ru/bigdata/statkey/moneymap/develop/#strukturaproekta). Кроме веба есть [sandbox таски](https://a.yandex-team.ru/arcadia/sandbox/projects/statkey/money_map)

#### Данные в базе 
Схема есть [на вики](https://wiki.yandex-team.ru/bigdata/statkey/moneymap/architecture/?from=%2Fstatbox%2Fstatkey%2Fmoneymap%2Farchitecture%2F#sxemabd)

Миграции схемы и данных нигде **не хранятся**. Делается наживую руками, сначала на препроде, потом в проде. Причина: с момента создания moneymap миграции приходилось делать редко, поэтому решили не тратить сил на написание скриптов, интеграции flyway, etc.

### Релизы

Для проекта подкючен [arcadia CI](https://a.yandex-team.ru/projects/moneymap/ci/releases/timeline?dir=statbox%2Fmoneymap&id=moneymap-release). Чтобы выложить новый код нужно
1. Нажать на большую синюю кнопку run release справа в верху. 
2. Создастся новая релизная ветка из транка и запустится процесс сборки. 
3. После этого автоматически релиз поедет на препрод. 
4. Когда завершится деплой нужно проверить, что работает базовая функциональность: редактирование, создание блоков и пейджей. 
5. Если все ок на карте релиза нажимаем кнопку выкладки в прод. 
6. После обновления прода нужно помониторить логи деплоя на наличие ошибок

[ссылка на вики](https://wiki.yandex-team.ru/bigdata/statkey/moneymap/duty/#deplojjkoda)

### Инфра

Сервис развернут в деплое на два стейджа: [препрод](https://deploy.yandex-team.ru/stages/preprod-moneymap) и [прод](https://deploy.yandex-team.ru/stages/prod_moneymap). Каждый стенд состоит из одного деплой юнита. В нем работают java backend, frontend на реакте (его сервит нода) и balancer в виде nginx. Каждому из боксов соответствует своя папка в коде. Джава пакуется через `ya make`, а фронтенд и nginx собираются в докер контейнеры. Приложение находится за [балансером](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/moneymap.yandex-team.ru) в няне. В mdb развернуто два кластера PG - по одному на каждое окружение. Кластер прода состоит из master-slave (sas,vla), в препроде одинокий master.  

[диаграмма архитектуры сервиса](https://wiki.yandex-team.ru/bigdata/statkey/moneymap/architecture/?from=%2Fstatbox%2Fstatkey%2Fmoneymap%2Farchitecture%2F#arxitekturaservisa)

### Мониторинг 

#### Графики
- [deploy](https://deploy.yandex-team.ru/stages/prod_moneymap/monitoring)

#### Алерты 
- [ping прода](https://juggler.yandex-team.ru/check_details/?host=money_map_production_backend&service=moneymap_production.availability&project=moneymap&last=1DAY)
- [ping препода](https://juggler.yandex-team.ru/check_details/?host=money_map_preprod.backend&service=moneymap_preprod.availability&project=moneymap&last=1DAY)

На стороне ПИ мы должны настроить алерты на 3 важных трансфера:
1. [0_CREATE_TMP_MM_SNAPSHOT](https://yc.yandex-team.ru/folders/akuvmhg74u0c9n6v48eh/data-transfer/transfer/dtt16i8brtu6qod28ooq/view) 
2. [transfer_prod_to_prerpod_mm](https://yc.yandex-team.ru/folders/akuvmhg74u0c9n6v48eh/data-transfer/transfer/dttpupdeer9238hoh351/view)
3. [mm-prod-mdb-postgres](https://yc.yandex-team.ru/folders/akuvmhg74u0c9n6v48eh/data-transfer/transfer/dtt3gstiiro1nu75n294/view)

### Фоновые задачи

В основном это sandbox таски, запускаемые из [реактора](https://reactor.yandex-team.ru/browse?selected=11725536). Они подготавливают данные из разных источников, сливают их в postgres манимапа и дампят в YT. Чтобы найти код реакции: проваливаемся из интерфейса `launches`, затем `attempts`. Из сендбокса попадаем в аркадию.

Поток данных хорошо иллюстрирует [диаграмма](https://wiki.yandex-team.ru/bigdata/statkey/moneymap/architecture/?from=%2Fstatbox%2Fstatkey%2Fmoneymap%2Farchitecture%2F)

Также есть логика по созданию тикетов о плохой разметке блоков и пейджей. Она совмещена с подготовкой сущностей в [реакции](https://reactor.yandex-team.ru/browse?selected=9228154). 
 
Каждую полночь по [кроновой реакции](https://reactor.yandex-team.ru/browse?selected=9199340) запускается [трансфер](https://yc.yandex-team.ru/folders/akuvmhg74u0c9n6v48eh/data-transfer/transfer/dttpupdeer9238hoh351/view) в MDB продовой базы в препродовую.

Есть совсем не фоновый, а realtime трансфер базы postgres в yt. Этот процесс настроен через трансфер [mm-prod-mdb-postgres](https://yc.yandex-team.ru/folders/akuvmhg74u0c9n6v48eh/data-transfer/transfer/dtt3gstiiro1nu75n294/view). Он может переодически падать

Доп описание на [вики дежурного](https://wiki.yandex-team.ru/bigdata/statkey/moneymap/duty/?from=%2Fstatbox%2Fstatkey%2Fmoneymap%2Fduty%2F#kratkoeopisanie)

### Походы во внешние сервисы

Ходим в апи abc за списком яндексовымх сервисов. И в пасспорт для авторизации пользователя на запросе. 

### Авторизация

Есть две роли:
- чтение
- редактирование

они получаются через IDM. процесс подробно описан в [инструкции для пользователя UI](https://wiki.yandex-team.ru/bigdata/statkey/moneymap/managersdoc/?from=%2Fstatbox%2Fstatkey%2Fmoneymap%2Fmanagersdoc%2F#dostupy). В коде проверяем наличие и в случае остуствия запрещаем доступ к ресурсу. 

### Доступы и секреты

Доступ к сервису выдан через [панчер](https://puncher.yandex-team.ru/?id=5fd0ae9da6bbdb48be74442f) всем, кто состоит в ABC сервисе ПИ. 
Актуальный список секретов лучше смотреть на [деплойном стейдже в боксе java](https://deploy.yandex-team.ru/stages/prod_moneymap/config/du-backend/box-javaApp). Доступы к секретам есть у ролей из ABC сервиса MoneyMap. 

### Тесты 

Тестов нет :( Продублирую из секции про релизы. Основная функциональность это

#### Создание пейджа

Создаем в YT таблицу с единственной колонкой - `page_id`. Добавляем туда как угодно (запросом через YT, CLI командой, etc) айди, которого на данный момент нет в базе ([пример](https://preprod.moneymap.in.yandex-team.ru/pages/?page_id=12312312&limit=20)). После чего делаем запрос из браузера в ручку `http://preprod.moneymap.in.yandex-team.ru/api/v1/yt/preload_pages?force=true&ytPath=//path/to/your/table`. В ответ мы должны получить OK, а пейдж станет доступным для разметки.

#### Создание блока

Алгоритм такой же, как для пейджей. Отличие только в том, что в таблице должно быть два поля: `page_id` и `block_id`.

#### Изменение блока, изменение пейджа

Заходим на препрод и меняем поля сущностей через интерфейс. 

#### Ручки ui fields

Проверяем `GET https://preprod.moneymap.in.yandex-team.ru/api/v1/ui/fields` и четыре комбинации параметров `?withBlocks=<bool>&partner=<bool>`. Код находится в [getUiFields](https://a.yandex-team.ru/arc_vcs/statbox/moneymap/backend/java/src/main/java/ru/yandex/statkey/moneymap/controllers/UIController.java?rev=r9520669#L50).

То же самое для `https://preprod.moneymap.in.yandex-team.ru/api/v1/ui/suggest_fields` с такими же двумя параметрами.

#### Suggest сервисов abc 

В него ходит джава из [MoneyMapService](https://a.yandex-team.ru/arc_vcs/partner/java/libs/extservice/src/main/java/ru/yandex/partner/libs/extservice/moneymap/MoneyMapService.java?rev=r9433668#L60) `GET https://preprod.moneymap.in.yandex-team.ru/api/v1/abc/suggest?text=<str>`. Можно либо напрямую сходить в MM, либо на ТС-е ПИ воспользоваться suggest. 


### Задачи 

Очередь http://st.yandex-team.ru/MONEYMAP содержит задачи на фич реквесты, баги и инфраструктурные улучшения. А https://st.yandex-team.ru/MONEYMAPRESOLVE является технической - туда приходят отибвки Оксане о неразмеченных сущностях. За формирование тикетов отвечает реакция [1_MONEYMAP_MONITORINGS_AND_NEW_ENTITIES](https://reactor.yandex-team.ru/reaction?id=9228154&mode=instances). Еще есть [чатик MoneyMap](https://t.me/joinchat/TZnLDYrdZl61VeUu) 

### Как запустить локально

описано в [инструкции для разработчиков](https://wiki.yandex-team.ru/bigdata/statkey/moneymap/develop/?from=%2Fstatbox%2Fstatkey%2Fmoneymap%2Fdevelop%2F) 

### API 

Есть swagger по ссылке `https://preprod.moneymap.in.yandex-team.ru/api/v1/swagger-ui.html`
