# Концепт

Этот раздел помогает начать решать технические задачи на выдаче.

## Виджеты выдачи

Скриншот страницы выдачи | Скриншот страницы выдачи в раскраске
:---: | :---:
![Скриншот страницы выдачи](./_assets/search-page-default.png) | ![Скриншот страницы выдачи в раскраске](./_assets/search-page-widgets.png)

Выдача строится из множества виджетов: тайтла, сортировки, фильтров, результатов, пагинации и других. Можно подключить эти виджеты в любом количестве, в любом порядке, и они будут синхронизированы как на сервере, так и на клиенте.

Виджеты выдачи группируются при помощи CMS-разметки в формате JSON. Стили, цвета и отступы можно настроить все в той же разметке. Никаких внешних отступов по-умолчанию виджеты не имеют: все настраивается сверху. Кроме стилей виджеты ожидают ключ дедупликации (searchPlace), а также могут принимать простые скалярные параметры отображения.

## Доступность и встраиваемость выдачи

Виджеты выдачи можно подключить где угодно: код выдачи не зависит от платформы. Одновременно один и тот же код выдачи может использоваться и в десктопе, и на промо-странице, и в таче, и в мобильном приложении (FAPI), и на выдаче в приложении Яндекс Go.

Так как выдача построена на виджетной системе, ее можно легко встроить в промо-лендинг, и при это ленивизировать.

## "Hello World" виджет выдачи

Новый виджет выдачи можно создать из примера ([https://a.yandex-team.ru/arc_vcs/market/front/apps/marketfront/src/widgets/content/search/_Example](https://a.yandex-team.ru/arc_vcs/market/front/apps/marketfront/src/widgets/content/search/_Example)).

## Лэйаут выдачи

Подключение виджетов выдачи — это вызов виджета `CmsLayout` с двумя параметрами: разметкой в формате JSON и списком виджетов.

Разметка в JSON описывает верстку и подключаемые виджеты.

```json
{
    "entity": "box",
    "props": {
        "type": "row",
        "layout": true,
        "grid": 24
    },
    "name": "Grid24",
    "nodes": [
        {
            "entity": "box",
            "props": {
                "type": "column",
                "width": 18,
                "breakpoints": [
                    {
                        "breakpoint": "s",
                        "width": 27
                    }
                ]
            },
            "nodes": [
                {
                    "entity": "widget",
                    "name": "SearchPager",
                    "id": "SearchPager",
                    "wrapperProps": {
                        "margins": {
                            "top": "5"
                        }
                    },
                    "props": {
                        "searchPlace": "__search-place__",
                        "scrollToAnchor": "serpTop"
                    }
                }
            ]
        }
    ]
}
```

Этот JSON означает, что мы хотим подключить виджет `SearchPager` с отступом сверху в `5 * 4px = 20px` в 24-колоночной сетке.

Удобство такого подхода заключается в том, что можно расставить виджеты в произвольном порядке с произвольными отступами и цветами, при этом сами виджеты ничего не будут знать об этом.

Такой JSON можно накликать через CMS, и запрашивать при старте страницы из бэкенда `templator`.

## Виджет выдачи

Все виджеты выдачи похожи между собой. Часто они переиспользуют общий код, поэтому выдача в совокупности — экономное решение.

Каждый виджет выдачи сам запрашивает все данные. Контроллер может выглядеть например вот так:

```js
export default function controller(ctx: Context, {wrapperProps, props}: Options) {
    const searchResultPromise = resolveSearchByInitialParams(ctx, {
        searchPlace: props && props.searchPlace,
    })
        .catch(() => SEARCH_RESULT_STUB);

    return {
        data: searchResultPromise.then(({result}) => ({
            visibleSearchResultId: isRedirect(result) ? null : result,
            wrapperProps,
            scrollToAnchor: props.scrollToAnchor,
            hidePaginationInfo: props.hidePaginationInfo,
        })),
        collections: searchResultPromise.then(({
            collections: {
                searchResult,
                visibleSearchResult,
                intent,
            },
        }) => ({
            searchResult,
            visibleSearchResult,
            intent,
        })),
    };
}
```

Все данные виджет готовит не сам, а вызывает общий резолвер выдачи (`resolveSearchByInitialParams`). Этот резолвер кэшируется на запрос, поэтому все виджеты получают одинаковые данные, единый `visibleSearchResultId`.

Виджет не передает никакие параметры в резолвер выдачи кроме `searchPlace`. Такой подход обеспечивает дедупликацию запросов за выдачей.

Виджеты привозят только необходимые для себя коллекции. Например, для виджета `Title` не нужны фильтры.

## Параметры Репорта

Фронт общается с Репортом через параметры. Параметров очень много, к ним постоянно добавляются новые.

Не все, но многие параметры хорошо документированы. Некоторые не задокументированны вообще.
- Фронтовая документация по всем параметрам выдачи ([https://a.yandex-team.ru/arc_vcs/market/front/apps/marketfront/src/resources/report/fetchPrime/index.js](/src/resources/report/fetchPrime/index.js))
- Фронтовая документация по общим параметрам ([https://a.yandex-team.ru/arc_vcs/market/front/apps/marketfront/src/resources/report/params/index.js](/src/resources/report/params/index.js))
- Автодокументация Репорта (https://wiki.yandex-team.ru/users/vlmarkov/dokumentacija-osnovnogo-api-report)
- Ручная документация от Димы Полякова (https://wiki.yandex-team.ru/market/verstka/report-query-params)

Среди параметров можно выделить две группы: фильтры и поисковые параметры. `hid`, `nid`, `numdoc`, `text` — поисковые параметры. `glprice`, `free-delivery`, `good-state` — фильтры. Путать группы параметров нельзя. Если, скажем, `hid` посчитать за фильтр, произойдет конфликт при слиянии параметров, и вся логика "фильтра hid" будет перезаписана search-параметром `hid`.

Одной из задач фронта является правильно распарсить query-запрос, получить параметры Репорта и отправить только нужные. Тем не менее интерфейс выдачи фронта не является интерфейсом выдачи Репорта. На фронте могут использоваться отличные от Репорта термины (`count` вместо `numdoc`, `NavnodeId` вместо `nid`).

## Параметры запроса выдачи

Параметры для запроса в Репорт аккумулируются через резолвер. В качестве параметров этот резолвер должен использовать только контекст и параметр `searchPlace`.

```js
const commonParamsPromise = resolveCommonReportParams(ctx, {
    usePerks: true,
    useDisabledPromoThresholds: true,
    useAdult: true,
    useCart: resolvePriceDropIsAvailableSync(ctx),
    useAllowedPromos: IS_SECRET_SALE_ACTIVE,
    additionalParams,
});

const queryParamsPromise = resolveQueryParams(ctx);
const placeParamsPromise = resolveSearchPlaceParams(ctx, {searchPlace});
const filterParams = resolveFilterParamsSync(ctx);
const requestParams = resolveRequestParamsSync(ctx);

return Promise.all([
    commonParamsPromise,
    queryParamsPromise,
    placeParamsPromise,
])
    .then(async ([
        commonParams,
        queryParams,
        placeParams,
    ]) => {
        const params = {
            ...commonParams,
            ...filterParams,
            ...requestParams,
            ...queryParams,
            // при первом запросе страницы параметры конфигурации имеют наивысший приоритет,
            // т.к. являются инциализирующими
            ...placeParams,
        };
    });
```

Все параметры разделены на пять множеств:
- общие параметры Репорта: единый набор опций, подходящих для любого запроса в Репорт;
- фильтры;
- query-параметры;
- request-параметры: все параметры, что не query и не фильтры;
- place-параметры: параметры из cms-конфига по ключу `searchPlace`.

## Жизнь в рантайме

Все виджеты выдачи обращаются в единый резолвер. Резолвер кэширует все запросы, и возвращает для всех потребителей один результат: нормализованный стейт выдачи.

![Схема обращения виджетов к резолверу](./_assets/widgets-to-resource.jpeg)

Центральная сущность в ответе: `VisibleSearchResult`. Эта сущность ссылается на все страницы выдачи, результаты поиска, сортировки, товары и прочее. Все виджеты выдачи через ссылку (`visibleSearchResultId`) подписываются на эту центральную сущность, слушают ее и обновляются в случае обновлении коллекции `VisibleSearchResult` и других коллекций. Например, виджет фильтров обновится при обновлении коллекций VisibleSearchResult, Filter, FilterValue и FilterToValues.

Именно по той причине, что все виджеты подписаны на VSR, не стоит лишний раз добавлять поля именно в эту сущность: если это возможно, лучше добавить новое поле в любую саб-сущность выдачи.

![Связь всех виджетов с сущностью VSR](./_assets/widget-vsr-relation.png)

Глобальные эпики обновления выдачи также привязаны к VSR. Все последующие страницы выдачи (действия при пагинации, применении фильтров или сортировок) привязаны к одному и тому же `VisibleSearchResult`.

Обновление выдачи происходит через экшн `FETCH_SEARCH_RESULT` и эпик `obtainSearchResultEpic`.
