# Резолвер resolveProductVideos

## Описание

Резолвер возвращает __самые релевантные__ видеообзоры для продукта, среди тех, что подходят по релевантности.


## Входные параметры

Здесь два варианта:

* Только productId:

    	{
        	minRelevance: число из отрезка [0, 1],
        	productId
   		}

	Оба параметра обязательны

* Все необходимые ресусу параметры:

        {
            minRelevance: число из отрезка [0, 1],
            productId,
            categoryId,
            productName
        }

	Все четыре параметра обязательны

Если есть возможность, лучше использовать второй вариант.

Параметр minRelevance определяет минимальную приемлемую релевантность.
Если вам подходят все видео, передавайте в него 0.


## Ссылочки

- [Входные параметры](https://github.yandex-team.ru/market/marketfront/blob/master/market/platform.touch/resolvers/video/index.js#L47-L55)
- [Описание сущности `Video`](https://github.yandex-team.ru/market/marketfront/blob/master/root/src/entities/video/index.js#L7-L22)
