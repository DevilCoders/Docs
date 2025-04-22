## TODO

-   [x] Продумать отдачу прогресса поиска на странице региона и странице отеля.
-   [x] Пины -- детализировать.
-   [ ] Типы питания: нужно продумать, что с типами питания; как расширять их на беке? Обратить внимание на OfferMealType.
-   [ ] Проброс произвольных параметров с фронта на бек.
    -   Протаскивать relev (а-ля srcparams)
-   [ ] Фильтры по поставщикам.
-   [ ] Отладачная информация:
    -   показывать permalink
    -   id-ы у поставщиков
    -   geo-req-ids
    -   front-req-id
-   [ ] Сниппет расстояния до метро
-   [ ] Обсудить:
    -   локализация цен и названий?
-   [ ] Заботливая галка
-   [ ] Атрибуция

## Термины

-   Атом -- техническая строка для кодирования фильтра по признакам отелей. Атом = id+value. Для транспортного протокола считаем, что атом -- это строка. Для интуитивного понимания можно считать, что атом это строка вида "star:two", "star:three", "rating:4+", "wi_fi:1".
-   Поллинг - Процесс уточнения результатов, состоящий из нескольких запросов к бэкенду.

## Методы

-   `searchHotels`:: `/api/hotels_portal/v1/search_hotels`
-   `countHotels`:: `/api/hotels_portal/v1/count_hotels`

---

## Общие объяснения

### Желаемые свойства

-   Те отели, что есть в списке, должны быть и на карте.
-   В списке не должно быть отелей без цен (на карте -- могут).
-   Карта должна быть отзывчивой.

---

## Требования к бекенду

### Передача параметров

-   Если указан bbox и geoId, то geoId далее игнорируется в работе поиска.

### Информация о регионе поиска

-   Вычислять регион поиска исходя из топа (топ-10) отелей в выдаче ГП как наименьший общий регион.

### Фильтры

-   Атом распадается на пары (id, value), которые 1-в-1 пробрасываются в business_filter в ГП.

### Пагинация

-   Пагинация по токену должна смещать выдачу на `pageHotelCount` отелей.
    -   Таким образом, у двух соседних запросов выдачи могут пересекаться.

### Поллинг

-   Один запрос в бэкенд = один запрос в ГП, с фиксированным размером страницы
-   Каждый отель отсылается на фронт максимум два раза: первый раз с IsFinished=false, второй - с IsFinished=true
-   Идемпотентность обеспечивается за счет сохранения состояния поиска в context

---

## Требования к фронту

В описании ниже подразумеваются две константы -- `FrontHotelsInMap` и `FrontHotelsInList` -- определяемые на фронте в зависимости от платформы (desktop, touch, mobile, ...) и регулирующие число отелей на карте и в списке.

### Передача параметров

-   При первом запросе к `searchHotels` передается `geoId`, в ответе получается `bbox`.
-   При всех последующих запросах передается `bbox` + `content`.
-   Передается состояние фильтров (см. `IFilterParams`).
-   Передается информация о состоянии поллинга (см. секцию про поллинг).
-   Передаются константы на количество отелей в списке и на карте.

### Информация о регионе поиска

-   Отрисовывается на основе ответа бекенда.

### Фильтры

-   Состояние фильтров определяется переменными типа `IFilterParams`. Визуальные и интерактивные свойства фильтров вычисляются на основе данных переменных. Далее `state ~ IFilterParams`.
-   Быстрые фильтры: 1 быстрый фильтр `f` описывается 1 объектом типа `IQuickFilter`.
    -   Нажат (toggled): если все atomsOn - есть в state, и ни одного atomsOff - нету.
    -   Выключен (disabled): `f.enabled == false`.
    -   При нажатии на фильтр: `state.atoms = state.atoms \cup f.atomsOn \setminus f.atomsOff`.
    -   При отжатии фильтра: `state.atoms = state.atoms \setminus f.atomsOn`.
-   Группа фильтров: 1 группа `g` описывается 1 объектом типа `IBasicFilterGroup`.
    -   Если `g.type == 'multi'`, то рисуется группа чекбоксов.
        -   1 чекбокс `f` описывается 1 объектом `IBasicFilter`.
        -   Выбран (checked): `f.atoms \subseteq state.atoms`.
        -   Выключен (disabled): `f.enabled == false`
        -   При взведении галочки: `state.atoms = state.atoms \cup f.atoms`
        -   При снятии галочки: `state.atoms = state.atoms \setminus f.atoms`
    -   Если `g.type == 'single'`, то рисуется группа радиобаттонов.
        -   1 опция `f` описывается 1 объектом `IBasicFilter`.
        -   Индекс выбранной опции (selected-index): `min i : g.items[i].atoms \subseteq state.atoms`
        -   Опция выключена (disabled): `f.eabled == false`
        -   При выборе новой опции `j` вместо опции `i`: `state.atoms = (state.atoms \setminus g.items[i]) \cup g.items[j]`

### Поллинг

Поллинг стартует с начала при следующих событиях:

-   Смена фильтра
-   Сдвиг/зум карты (по сути, это тоже смена фильтра)
-   Смена параметров поиска (даты, гости)
-   Переход на другую страницу (паджинация)

При первом запросе:

-   Нужно очистить список отелей
-   Карта очищается только в случае смены фильтрации. При паджинации или драге карту очищать не нужно.
-   Очиститить operatorById
-   Новому поллингу присваивается новый номер `pollEpoch`, его нужно передать в параметрах
-   Передать pollIteration = 0 и context - из предыдущего полученного ответа (если был)

При каждом последующем запросе:

-   Передать текущий `pollEpoch`
-   Передать pollIteration = (pollIteration из предыдущего запроса) + 1 и context - из предыдущего полученного ответа

При получении ответа:

-   Ответ необходимо отбросить, если
    -   Если ответ относится к более старой эпохе.
    -   Если ответ относится к более старой итерации в текущей эпохе.
-   Взять searchRegion/geoId в качестве geoId для использования в последующих запросах и отображения в шапке
-   Взять поля из offerSearchParams для последующих запросов и отображения в шапке
-   Взять первые pricedHotelCount отелей из hotels и добавить их в конец списка отелей, но так, чтобы размер списка не превысил pageHotelCount.
-   Взять все отели из hotels и обновить карту. Отели по которым нет обновлений, не посылаются.
-   Фронт должен сам следить за количеством отелей на карте, чтобы не лопнуть
-   Обновить operatorById пришедшими данными
-   Запомнить context для последующего запроса
-   Если offerSearchProgress.finished = true, то поллинг завершается
-   Если offerSearchProgress.finished = false, то нужно сделать следующий запрос через 3 секунды, с pollIteration = pollIteration + 1
    Если ответ не получен (или получен с HTTP Code != 200), то нужно повторить запрос с теми же значениями pollIteration (без увеличения) и context.

Поллинг, паджинация, фильтры и bbox.

-   В рамках одной эпохи поллинга надо передавать строго одинаковые параметры фильтрации (атомы, цены, даты, гости...)
-   Аналогично - должен быть одинаковый bbox.
-   При паджинации применяются те же правила. Должны быть ровно те же фильтры, и ровно тот же bbox.
-   Единственное исключение - если bbox изначально неизвестен, то в первом запросе поллинга самой первой страницы, его можно не передавать. Во все следующие запросы поллинга и паджинации необходимо передать bbox, полученный из первого ответа.

### Пагинация

-   Под списком есть две кнопки -- назад и вперед -- при клике на которые происходит проброс навигационного токена.

### Карта (логика на фронте)

-   Поддерживается хранилище ограниченного информации об отелях: `permalink -> IHotelWithOffers`.
-   Добавляются только отели, где `searchIsFinished == true`.
-   Удаляются отели согласно убыванию расстояния от центра bbox-а до отеля.
    -   https://en.wikipedia.org/wiki/Great-circle_distance
    -   https://en.wikipedia.org/wiki/Haversine_formula
    -   https://www.movable-type.co.uk/scripts/latlong.html

---

#### Алгоритм обработки поллинга на бэкенде (детали реализации)

Состояние поллинга поддерживается в контексте запроса. В состояние входят следующие данные:

-   Offset - текущее смещение паджинации
-   FirstGeoPage - Первая страница геопоиска, опрошенная в текущем поллинге
-   FirstPermalink - (Опционально) Первый пермалинк, который требуется показать
-   GeoPage - Текущая страница геопоиска
-   GeoPageFirstAccess - Флаг первичного обращения к текущей странице геопоиска
-   SentInProgressHotels - Список отелей на текущей странице геопоиска, которые еще не актуализированы
-   SentPricedHotelCount - Количество отелей с ценами, которые мы отослали фронту

Кроме того, в контексте хранится список известных страниц. Про каждую страницу известно следующее:

-   Offset - смещение паджинации
-   FirstGeoPage - первая страница геопоиска с полезными результатами
-   FirstPermalink - первый пермалинк, который нужно показать на странице

Действия бэкенда при старте поллинга:

-   Начало поллинга детектируется по pollIteration == 0.
-   Очищаем context.PollingState
-   В случае, если токен навигации не задан, то забываем страницы навигации в браузере - считаем, что произошла смена фильтров или bbox-а. В этом случае, в context.PollingState выставляем Offset=0, FirstGeoPage=0, GeoPage=0, GeoPageFirstAccess=true
-   В случае, если токен навигации задан, то вычленяем из токена Offset, и ищем такую страницу в context. В context.PollingState копируем Offset, FirstGeoPage и FirstPermalink. Ставим GeoPageFirstAccess=true. Из контекста удаляем все страницы с Offset >= текущего.

При продолжении поллинга никаких особенных действий не предпринимается.

В ГП посылается запрос, limit = req.totalHotelLimit, page = context.GeoPage.

Обработка ответа от ГП:

-   Если задан context.FirstPermalink - пропускаем все отели до него
-   Если context.GeoPageFirstAccess == true, то:
    -   В context.SentInProgressHotels помещаем те, которые IsFinished=false
-   Если context.GeoPageFirstAccess == false, то:
    -   Пропускаем отели, которые не находятся в context.SentInProgressHotels
    -   Пропускаем отели, у которых IsFinished=false
    -   Из context.SentInProgressHotels удаляем те, которые IsFinished=true
-   Если отель IsFinished и цены есть, и ранее не видели отели с IsFinished=false, то увеличиваем context.SentPricedHotelCount, вытаскиваем такие отели в начало списка
-   Когда context.SentPricedHotelCount становится равен 1, в context.Pages добавляем информацию о текущей странице (для навигации назад на неё)
-   Когда context.SentPricedHotelCount становится равен 1 + pageHotelCont, в context.Pages добавляем информацию о следующей странице (для навигации вперёд на неё)
-   После обработки всех отелей смотрим:
    -   если есть отели с IsFinished=false, то отдаём ответ фронту с IsFinished=false, поллинг будет продолжен
    -   иначе, если context.SentPricedHotelCount >= (1 + PricedHotelLimit), отдаем ответ с IsFinished=true, поллинг останавливается
    -   иначе увеличиваем context.GeoPage. Если context.(GeoPage - FirstGeoPage) > N, останавливаемся (IsFinished=true), иначе - поллинг продолжается.
-   Токены навигации проставляются по наличию информации о соответствующих страницах в контексте.

### Пример сессии поллинга

```
(Epoch=0, Iteration=0)
В запросе передаем pageHotelCount=10, pricedHotelLimit=20, totalHotelLimit=50.
* Очищаем список
* и карту (кроме случая паджинации)

В ответе pricedHotelCount=5, offerSearchProgress.isFinished == false.
=> добавляем в список 5 первых отелей (они - с ценами)
=> все отели наносим на карту (из них >=5 с ценами; оценка снизу, так как в хвосте выдачи могут быть отели с ценой);
=> продолжаем поллинг.

(Epoch=0, Iteration=1)
В запросе передаем pageHotelCount=10, pricedHotelLimit=20, totalHotelLimit=50, context из предыдущего ответа

В ответе pricedHotelCount=10, offerSearchProgress.isFinished == false.
=> добавляем в список 5 отелей (можно было и 10, но у нас есть ограничение pageHotelCount=10)
=> все полученные отели обновляем на карте
=> продолжаем поллинг.

(Epoch=0, Iteration=2)
В запросе передаем pageHotelCount=10, pricedHotelLimit=20, totalHotelLimit=50.

В ответе pricedHotelCount=3, offerSearchProgress.isFinished == true.
=> В список уже ничего не добалвяем, он и так полный
=> все полученные отели обновляем на карте
=> останавливаем поллинг.
```

## Пример данных (старый)

```
Request: TRequest {
    GeoId: "213";
    Bbox: "37.0408809,55.311850~38.20412732,56.18961995"; // "lon,lat~lon,lat"

    CheckIn: "2019-09-01",
    CheckOut: "2019-09-02",

    // Или одной строкой
    Occupancy: "2-3,4",
    // Или раскрыто
    Adults: 2,
    ChildAges: [3, 4],

    Ctx: "...",

    FilterAtoms: "star:three,star:four,rating:4+,wi_fi:1",
    FilterPriceFrom: 15000,
    FilterPriceTo: null,
}

Response: TResponse {
    SearchView: TSearchView {
        CheckIn: "2019-09-01",
        CheckOut: "2019-09-02",
        Occupancy: "2-3,4",
        DisplayCheckInShort: "1 сен",
        DisplayCheckOutShort: "2 сен",
        DisplayOccupancy: "2 взрослых и двое детей (3 и 4 года)"
    },
    RegionView: TRegionView {
        GeoId: 213;
        Bbox: "37.0408809,55.311850~38.20412732,56.18961995"; // "lon,lat~lon,lat"
        DisplayName: "Москва"
    },
    FilterView: TFilterView {
        State: TFilterState {
            // Будут включены:
            // - быстрый фильтр "Высокий рейтинг"
            // - быстрый фильтр "Интернет"
            Atoms: Set<TAtom> [
                { Id: "star", Value: "three" },
                { Id: "star", Value: "four" },
                { Id: "rating", Value: "4+" },
                { Id: "wi_fi", Value: "1" },
            ],
            PriceFrom: 15000,
            PriceTo: null,
        }
        Corrections: TFilterCorrections {
            StateWasReset: False,
            TextWasCorrected: False,
            OriginalText: null,
            CorrectedText: null,
        }
        EstimatedHitCount: 13,
        TotalHitCount: 1286,
        QuickFilters: List<TBasicFilter> [
            TBasicFilter {
                DisplayName: "С завтраком",
                Atoms: [
                    { Id: "has_breakfast", Value: "1" }
                ]
                // остальные поля в макете сейчас не используются
            },
            TBasicFilter {
                DisplayName: "С отменой брони",
                Atoms: [
                    { Id: "free_cancellation", Value: "1" }
                ]
                // остальные поля в макете сейчас не используются
            },
            TBasicFilter {
                DisplayName: "3* и выше",
                Atoms: [
                    { Id: "star", Value: "three" },
                    { Id: "star", Value: "four" },
                    { Id: "star", Value: "five" }
                ]
                // остальные поля в макете сейчас не используются
            },
            TBasicFilter {
                DisplayName: "Интернет",
                Atoms: [
                    { Id: "wi_fi", Value: "1" }
                ]
                // остальные поля в макете сейчас не используются
            },
            TBasicFilter {
                DisplayName: "Парковка",
                Atoms: [
                    { Id: "has_parking", Value: "1" }
                ]
                // остальные поля в макете сейчас не используются
            },
            TBasicFilter {
                DisplayName: "Высокий рейтинг",
                Atoms: [
                    { Id: "rating", Value: "4+" }
                ]
                // остальные поля в макете сейчас не используются
            }
        ],
        DetailedFilters: List<TBasicFilterGroup> [
            {
                DisplayName: "Звёздность",
                DisplayType: Multi,
                Items: List<TBasicFilter> [
                    TBasicFilter {
                        DisplayName: "2* и ниже",
                        DisplayClass: null,
                        HitCount: 130,
                        MinPrice: 500,
                        Atoms: [
                            { Id: "star", Value: "one" },
                            { Id: "star", Value: "two" }
                        ]
                    },
                    TBasicFilter {
                        DisplayName: "3*",
                        DisplayClass: null,
                        HitCount: 400,
                        MinPrice: 3870,
                        Atoms: [ { Id: "star", Value: "three" } ]
                    },
                    TBasicFilter {
                        DisplayName: "4*",
                        DisplayClass: null,
                        HitCount: 560,
                        MinPrice: 8505,
                        Atoms: [ { Id: "star", Value: "four" } ]
                    },
                    TBasicFilter {
                        DisplayName: "5*",
                        DisplayClass: null,
                        HitCount: 1023,
                        MinPrice: 13500,
                        Atoms: [ { Id: "star", Value: "five" } ]
                    },
                ]
            },
            {
                DisplayName: "Рейтинг",
                DisplayType: Single,
                Items: [
                    TBasicFilter {
                        DisplayName: "1 и выше",
                        DisplayClass: "rating_1",
                        HitCount: 989,
                        MinPrice: 500,
                        Atoms: [ { Id: "rating_1_5", Value: "1-" } ]
                    },
                    TBasicFilter {
                        DisplayName: "2 и выше",
                        DisplayClass: "rating_2",
                        HitCount: 500,
                        MinPrice: 2500,
                        Atoms: [ { Id: "rating_1_5", Value: "2-" } ]
                    },
                    TBasicFilter {
                        DisplayName: "3 и выше",
                        DisplayClass: "rating_3",
                        HitCount: 270,
                        MinPrice: 9500,
                        Atoms: [ { Id: "rating_1_5", Value: "3-" } ]
                    },
                    TBasicFilter {
                        DisplayName: "4 и выше",
                        DisplayClass: "rating_4",
                        HitCount: 54,
                        MinPrice: 11500,
                        Atoms: [ { Id: "rating_1_5", Value: "4-" } ]
                    }
                ]
            },
            {
                DisplayName: "Удобства",
                DisplayType: Multi,
                Items: [
                    TBasicFilter {
                        DisplayName: "Бассейн",
                        DisplayClass: null,
                        HitCount: 34,
                        MinPrice: null,
                        Atoms: [ { Id: "pool", Value: "1" } ]
                    },
                    TBasicFilter {
                        DisplayName: "Кондиционер",
                        DisplayClass: null,
                        HitCount: 220,
                        MinPrice: null,
                        Atoms: [ { Id: "air_conditioning", Value: "1" } ]
                    },
                    TBasicFilter {
                        DisplayName: "Интернет",
                        DisplayClass: null,
                        HitCount: 525,
                        MinPrice: null,
                        Atoms: [ { Id: "wi_fi", Value: "1" } ]
                    },
                    TBasicFilter {
                        DisplayName: "Фитнес",
                        DisplayClass: null,
                        HitCount: 12,
                        MinPrice: null,
                        Atoms: [ { Id: "gym", Value: "1" } ]
                    },
                    TBasicFilter {
                        DisplayName: "Можно с животными",
                        DisplayClass: null,
                        HitCount: 1,
                        MinPrice: null,
                        Atoms: [
                            { Id: "animal accommodations", Value: "animal paid" },
                            { Id: "animal accommodations", Value: "animal free" }
                        ]
                    },
                    TBasicFilter {
                        DisplayName: "Трансфер",
                        DisplayClass: null,
                        HitCount: 202,
                        MinPrice: null,
                        Atoms: [ { Id: "transfer", Value: "1" } ]
                    },
                    TBasicFilter {
                        DisplayName: "Ресторан",
                        DisplayClass: null,
                        HitCount: 780,
                        MinPrice: null,
                        Atoms: [ { Id: "has_restaurant", Value: "1" } ]
                    },
                ]
            },
        ]
    }
}
```
