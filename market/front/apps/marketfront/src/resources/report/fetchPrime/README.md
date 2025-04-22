# fetchPrime

Ручка для запроса результатов поиска по множеству критериев

## Аналитика
Сейчас fetchPrime для отслеживания скорости делится на N основных сценариев:

|name|url|описание|hid|text|fesh|show-reviews|
|---|---|---|---|---|---|---|
|fetchPrime_byTextInCategory|https://market.yandex.ru/catalog--noutbuki/54544/list?hid=91013&text=Ideapad| |+|+| | |
|fetchPrime_reviewHub|https://market.yandex.ru/catalog--avtomobilnye-shiny-viatti-otzyvy-pokupatelei/54469/list?glfilter=7893318%3A6841568&show-reviews=1| | | | |+|
|fetchPrime_byText|https://market.yandex.ru/search?text=Ideapad| | |+| | |
|fetchPrime_byCategory|https://market.yandex.ru/catalog--noutbuki/54544/list?hid=91013| |+| | | |
|fetchPrime_byShop|https://market.yandex.ru/search--sviaznoi?fesh=3828| | | |+| |
|fetchPrime_promo|https://market.yandex.ru/special/Delonghi_promo|В этом случае используется эвристика. Поиск идёт из гарсона? Значит промо страница| | | | |
|fetchPrime_other|всё что не попало выше.| | | | | | |
