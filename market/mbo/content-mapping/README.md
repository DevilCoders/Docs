Локальный запуск:
=================
1. Создать проект в идее: `scripts/create-idea-project-with-libs.sh` (полезно этой командой, т.к. там есть `-D=YA_IDEA_BUILD=yes`, нужное, чтобы не собирать фронтенд каждый раз при генерации проекта в идее).
2. Запуск бэкенда в IDEA:
   - открыть `ContentMappingMainApp`
   - `Ctrl + Shift + F10` - создастся конфигурация запуска
   - надо прописать `Working Directory` на путь к проекту в Аркадии
   - запустить ещё раз (там есть всякие код, детектирующий локальный запуск и настраивающий конфиги и логгер)
3. Запуск фронтенда:
   - поставить локально NodeJS 10-ой версии (чтобы был доступен `npm` из консоли) - можно ставить через brew, apt, скачать официальный
   - `run-frontend.sh` - запуск фронтенда
     - собирает java (но не запускает)
     - получает `definitions.ts`, кладёт их в нужное место, устанавливает
     - делает `npm ci` - очистка зависимостей и свежая установка по `package.lock` файлику
     - делает `npm start` для запуска приложения
   - как альтернатива - `run-frontend-no-ci.sh` - не делает `npm ci`, т.к. это долгая операция (если хочется очень быстро - можно вообще руками запускать `npm start` в нужной папочке, самому контролируя актуальность definitions.ts - `scripts/build-definitions.ts.sh`)
4. Запуск фронтенда с произвольным бэкендом (тестингом или продом):
   - TODO: @goryunov-se может помочь
   
Если учения и недоступен etcd:
1. cкопировать datasources с aida: `scp aida.yandex.ru:/etc/yandex/market-datasources/datasources.properties content-mapping-app/src/main/properties.d/local/50-datasources.properties`
2. добавить -DDISABLE_ETCD=1

Короткое описание про проект, что вообще происходит
===================================================
Основные сущности:
------------------
1. Магазины (cm.shop, Shop) - добавляются или руками или при входе, данные берутся из mbi
2. Пользователи (cm.user, User) - супер минимум инфы, есть роли (Role {SUPERADMIN, ADMIN, SUPPORT, OPERATOR, MANAGER, NONE}), пользователи-магазины не сохраняются в БД, на лету проверяется доступ через mbi
3. Оферы/Модели (cm.shop_model, ShopModel) - по сути, офер + данные для карточки + немного процессинга.
4. Представление офера (ShopModelView) - подсчитанный офер, который отдаётся на фронтенд.
5. Правила параметр-параметр (cm.param_mapping, ParamMapping) - сопоставление параметра магазина и Маркета
6. Правила значение-значение (cm.param_mapping_rule, ParamMappingRule) - сопоставление значений (для enum-ов)
7. Статистика офера (cm.shop_model_statistics, ShopModelStatisticsItem) - короткая информация по модельке, которая а) маленькая по объёму б) рассчитывается с вычислимыми значениями.
8. Информация по валидациям офера (cm.offer_processing_data, OfferProcessingDataItem) - информация по ошибкам, заполняется при импорте из ЕОХ

Основные операции:
------------------
1. Оферы импортируются из ЕОХ, `LogbrokerDatacampOfferMessageHandler` как точка входа.
2. В оферы может догружаться доп. информация - `OfferImportService`, по сути, доливаются `shopValues` (которые yml-парамы в каком-то смысле).
3. Применение правил происходит рантайм `RuleEngineService` и далее.
4. Правила грузятся в кэш через `RulesLoadService`.
5. Редактирование и т.п. оферов (см. `ShopModelController`).
6. "Экспорт" обратно в ЕОХ заполненных оферов - создаётся запись в очередь экспорта, `cm.shop_model_for_export`, `ShopModelExportService`, дальше асинхронно выгружается через `stroller`.

Работа правил:
--------------
1. Сами правила могут быть "гипотезными", `isHypothesis` (перегруженный термин) - такие записывают результат в модельку, опять же, только как предположение. Они не выгружаются при экспорте.
2. Правила могут быть "категорийными" (по умолчанию - действует везде, где есть параметр, категорийные действуют только в поддереве)
3. Правила бывают нескольких видов (`ParamMappingType`):
    - маппинг для енумов
    - FORCE_MAPPING - если значение не найдётся - запишет просто гипотезу
    - DIRECT - для строковых полей, просто копирует
    - FIRST_PICTURE/PICTURE - для работы с картинками
4. У правил может быть "разделитель" - значит, что значение магазина надо посплитить по нему до обработки.
5. Сами значения для енумов так же могут быть `isHypothesis`, тоже записывается с низким качеством.
6. В рамках модельки всё "мержится" (`MarketValuesResolver`):
    - считаем максимум значений, которые можно посчитать
    - и для каждого источника (`ValueSource`, `FORMALIZATION < RULE < MANUAL`) собираем значения
    - выбирается всё для максимального источника
    - внутри тоже может быть приоритет, через `ParamMappingRule.rank` - выбирается то, что с наибольшим `rank`-ом, из этого получается массив значений
    - есть значение "нет значения" - для убийства формализации



Добавление пользователя:
=============
1. Получить uid пользователя - с паблика выполнить curl -s "http://blackbox-mimino.yandex.net/blackbox?method=userinfo&userip=127.0.0.1&login=<логин_пользователя_на_я>" (поле "login" в ответе)
2. Добавить пользователя в таблицу cm.user (id = uid, role = ADMIN или MANAGER)
3. Если добавляется пользователь с ролью MANAGER, добавить связку в таблицу user_shop (user_id = uid, shop_id = id магазина из КИ)

Копирование магазина из прода с тестинг:
=============
1) Сдампить нужный продовый магазин MT в XSL (Идея сохраняет файл в кривом формате, так что вероятно его придется открыть в эксене и пересохранить)

```
select shop_sku,
       name,
       description,
       shop_category_name            as category,
       shop_vendor                   as vendor,
       coalesce((select string_agg(pic ->> 'url', ', ') from (select jsonb_array_elements(pictures) pic) as e),
                'http://link.link/') as "Ссылка на сайт",
       bar_code,
       vendor_code,
       'Россия'                      as "Страна производства"
from cm.shop_model m
where shop_id = 645435
```

2) Зайти на [cm-testing.market.yandex-team.ru](http://cm-testing.market.yandex-team.ru) и выбрать любого не нужного никому поставщика (желательно подтвердить что он никому не нужен через чатик MBO)

3) Перейти на [https://admin.market.fslb.yandex.ru/admin.html](https://admin.market.fslb.yandex.ru/admin.html) (manager.only / onlymarket1) и для выбранного поставщика в параметрах поставщика (звездочка в правой части интерфейса) поставить галки:

 - Признак доступности создания good-контента поставщиком

 - Признак доступности пайплайна 'Неси контент' в работе с ассортиментом

4) Зайти на [cm-testing.market.yandex-team.ru](http://cm-testing.market.yandex-team.ru) и проимпортировать XSL файл через Импорт/Экспорт → Импортировать XSL

5) Перезагрузить страницу, выбрать все офферы, и отправить в обработку (Ассортимент → Отправить в обработку)

6) Добавить магазин в MT, в качестве имени можно выбрать любое, в качестве id - id из 2го пункта

7) Готово. Через несколько минут сдампленные офферы пролезут из КИ в МТ

Как вернуть тестовые магазины в исходное неоскверненное состояние (на примере тестовых магазинов "Ножи 1-2" и "Музмарт 1-2"):
=============
delete from cm.shop_model where shop_id in (10451772,10453271,10421757,10411130);
delete from cm.param_mapping_rule where param_mapping_id in (
    select id from cm.param_mapping where shop_id in (10451772,10453271, 10421757, 10411130)
);
delete from cm.param_mapping where shop_id in (10451772,10453271, 10421757, 10411130)

Затем запустить:
https://ct-testing.market.yandex.ru/api/offers/update?shopId=10451772
https://ct-testing.market.yandex.ru/api/offers/update?shopId=10453271
https://ct-testing.market.yandex.ru/api/offers/update?shopId=10421757
https://ct-testing.market.yandex.ru/api/offers/update?shopId=10411130

Возможные проблемы:
=============
Если локально ругается на отсутствие библиотеки тикет-парсера (java.lang.UnsatisfiedLinkError: no ticket_parser2_java in java.library.path), то следует воспользоваться решением с https://wiki.yandex-team.ru/passport/tvm2/library/

Если ругается так:
```
Can't find getter for 'arg0' 
```

Надо добавить в Kotlin Compiler в настройках идеи опцию компилятора -java-parameters , и поставить пробел в проблемном классе, чтобы сбросились кэши

Полезные ручки
==============
- /api/internal/list-uploads - посмотреть последние загрузки
- /api/internal/list-uploads?shopId=1234 - посмотреть последние загрузки по магазину
- /api/internal/blob?blobId=161 - чтобы скачать загруженный пользователем файл

Ручно запуск миграции в ЕОХ
==============
--выбираем магазины - кандидаты на миграцию
SELECT string_agg(id::text, ',')
FROM cm.shop
WHERE migrating_status = 'NOT_MIGRATED' and id <> business_id;

--выбираем id из yt:
-- use hahn;
-- SELECT String::JoinFromList(AGGREGATE_LIST_DISTINCT(CAST(current.id AS String)), ',')
-- FROM `//home/market/production/mbi/dictionaries/partner_biz_snapshot/latest` as current
-- where current.type='SUPPLIER' and `is_united_catalog`=1
--   and current.id in (?????????????????)
--https://yql.yandex-team.ru/Operations/YQvGc_MBw8T5GojSBfbqsl4iuhi7-8AwORyCb0FvTvY=


-- проверяем и убеждаемся, что все ок(подставляем результат из предыдыщего запроса):
SELECT *
FROM cm.shop s
WHERE id in (?????????????????)
and id <> business_id
and exists(select * from cm.shop ss where ss.id = s.business_id);


-- Создаем таски в тасккью:
insert into taskqueue.task_queue (task_type, task_data, task_data_version, task_state, created_ts, next_run_ts)
(
select 'DatacampMigrationTask',
('{"shopId":' || s.id::text || '}')::json,
1,
'ACTIVE',
now(),
now()
from cm.shop s
WHERE id in (?????????????????)
and migrating_status = 'NOT_MIGRATED'
and id <> business_id
and exists(select * from cm.shop ss where ss.id = s.business_id)
);


-- проверяем результаты:
select *
from taskqueue.task_queue
where task_type = 'DatacampMigrationTask'
and (task_data->>'shopId')::bigint in (?????????????????)


-- и еще так:
SELECT migrating_status, is_locked, count(*)
FROM cm.shop s
WHERE id in (?????????????????)
and id <> business_id
and exists(select * from cm.shop ss where ss.id = s.business_id)
group by migrating_status, is_locked
order by migrating_status, is_locked;
