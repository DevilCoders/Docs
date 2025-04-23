# Ручки для получения ЧПУ сервиса

Нужно для построения сайтмапа, cost+ и прочих сервисов, которые хотят получить ЧПУ сервиса.

### Документация
[Как добавить новый фильтр на листинге](./addFilterListing.md)
[Как добавить новый паттерн на листинг](./addPatternListing.md)

## Вторичка

Принимает оффер, возвращает все урлы по вторички, включая разводящие и главную страницу.

`POST` `/friendlyUrls/offer/search/`

[Модель входных данных, оффера.](https://a.yandex-team.ru/arcadia/classifieds/realty-frontend/realty-seo-api/types/friendlyUrls/searchOffer.ts#L21)
[Пример запроса.](https://paste.yandex-team.ru/10313279)

## КП

Принимает оффер, возвращает все урлы по коттеджным посёлкам, включая разводящие и главную страницу.

`POST` `/friendlyUrls/offer/villageSearch/`

[Модель входных данных, оффера.](https://a.yandex-team.ru/arcadia/classifieds/realty-frontend/realty-seo-api/types/friendlyUrls/villageSearchOffer.ts#L4)
[Пример запроса.](https://paste.yandex-team.ru/10313285)

## Новостройки

Принимает оффер. Возвращает все урлы по коттеджным посёлкам, включая разводящие и главную страницу.

`POST` `/friendlyUrls/offer/newbuildingSearch/`

[Модель входных данных, оффера.](https://a.yandex-team.ru/arcadia/classifieds/realty-frontend/realty-seo-api/types/friendlyUrls/newbuildingOffer.ts#L7)
[Пример запроса.](https://paste.yandex-team.ru/10313292)

## Автор

Принимает оффер, информацию об автор. Сейчас это страницы про агенства/агента.

`POST` `/friendlyUrls/offer/author/`

[Модель входных данных, оффера.](https://a.yandex-team.ru/arcadia/classifieds/realty-frontend/realty-seo-api/types/friendlyUrls/authorOffer.ts#L3)
[Пример запроса.](https://paste.yandex-team.ru/10313296)

## Ипотека

Принимает оффер банка. Разводящая по ипотеки, по банку и т.д.

`POST` `/friendlyUrls/offer/mortgage/`

[Модель входных данных, оффера.](https://a.yandex-team.ru/arcadia/classifieds/realty-frontend/realty-seo-api/types/friendlyUrls/mortgageSearchOffer.ts#L3)
[Пример запроса.](https://paste.yandex-team.ru/10313297)

## Застройщик

Принимает оффер застройщика. Сейчас это только разводящие по застройщику.

`POST` `/friendlyUrls/offer/developer/`

[Модель входных данных, оффера.](https://a.yandex-team.ru/arcadia/classifieds/realty-frontend/realty-seo-api/types/friendlyUrls/mortgageSearchOffer.ts#L3)
[Пример запроса.](https://paste.yandex-team.ru/10313301)


## Базовые урлы сервиса

Возвращает статические урлы и урлы которым не требуются на вход данные, например страница `/alfabank/`

`GET` `/friendlyUrls/common/`
[Пример запроса.](https://paste.yandex-team.ru/10313302)
