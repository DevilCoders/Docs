### Android-прилоложение Яндекс.Маркета (WIP)
![](https://teamcity.yandex-team.ru/app/rest/builds/aggregated/strob:(buildType:(project:(id:Mobile_WhiteMarketAndroid)))/statusIcon.svg)

## Deeplinks

Приложение умеет обрабатывать следующие диплинки:

* `yandexmarket://` - главная страница
* `yandexmarket://openurl?url=https%3A%2F%2Fmarket.yandex.ru%2Fcatalog--territoriia-kofe%2F16416656` - открыть веб-вью с главной страницы
* Поиск (поддерживается передача фильтров и сортировок в формате, как на фронте)
    * `yandexmarket://search?text=iphone%20красный` - обычный поиск (редирект)
    * `yandexmarket://search/91013?text=2018` - поиск в категории (по hid)
* Каталог
    * `yandexmarket://catalog/54437` - открыть категорию в каталоге (по nid)
* Карточка модели
    * `yandexmarket://product/175944418` - открыть КМ по `model_id` (поддерживается передача фильтров как на фронте)
    * Дополнительные параметры для `GET` запроса:
            * `sort=aprice` - включить сортировку по цене
            * `initialScroll=offers` - доскроллить до указанного блока на КМ (возможные значения: сейчас только `offers`)
    * Отзывы
        * `yandexmarket://product/175944418/opinions` - открыть КМ и сразу после неё отзывы
        * `yandexmarket://product/175944418/opinions/my` - открыть КМ, и показать отзыв пользователя в самом верху, проскроллив на него
        * `yandexmarket://product/175944418/opinions/new` - открыть КМ, потом отзывы, а потом ещё и попап с созданием или редактированием отзыва на модель
    * QnA
        * `yandexmarket://product/175944418/questions` - открыть КМ и сразу после неё Q&A
        * `yandexmarket://product/175944418/questions/q/<questionId>` - открыть КМ, потом Q&A и
        загрузить вопрос с указанным id в самый верх списка. \
        Если указан `postAnswer`, то открыть форму оставления ответа.
        * `yandexmarket://product/175944418/questions/a/<answerId>` - открыть КМ, потом Q&A и загрузить
        вопрос с указанным ответом в самый верх списка.
* Favorites
    * `yandexmarket://wishlist` - список вишлиста
* Сравнение
    * `yandexmarket://compare` - список сравнений
    * `yandexmarket://compare/91033` - открыть сравнение из списка по `hid`
* Промохаб
    * `yandexmarket://promohub` - промохаб
    * `yandexmarket://promohub/{nid}` - промохаб, страница департамента
    * `yandexmarket://promohub/{nid}/{hid}` - промохаб, страница департамента с зажатой подкатегорией
* Лента
   * `yandexmarket://feed` - открыть главную страницу на ленте
   * `yandexmarket://feed/add` - открыть главную страницу на ленте и показать попап добавления контента