## Приборы доли и как на них реагировать

Графики доли показывают, какой процент от всех запросов в интернете приходится на Яндекс/Гугл/etc.
Есть два прибора, на которых дежсмена отслеживает долю запросов, которые приходятся на Яндекс.

- [Долотов](http://dolotov.com/4volozh/search3_combo.html) - внешний прибор, данные получаются из внешнего источника
- [RTMR](https://datalens.yandex-team.ru/y553z1uuri7yv-search-mon-dash?mode=tv) - основной, внутренний прибор, строим графики на основе данных, которые собираем сами.

Само значение доли не так критично, нас интересует разрыв с прошлыми значениями.
Конкретных цифр тут не зафиксировано, но негласно принято заносить [дежурным аналитикам](https://t.me/joinchat/4N9Qd83lOWsxNzA6) ([abc](https://abc.yandex-team.ru/services/search_share_duty/)) разрывы в ≥2%.

{% note alert %}

Подтверждённое падение доли - это красный протокол

{% endnote %}

В случае если в **нерабочее время** (выходные, ночь)

- есть инфоповод
- есть спортивное событие
- есть подозрение на приборные проблемы

прежде, чем нести проблему дежурным, можно попробовать убедиться что проблема вызвана событием снаружи.

Во всех остальных случаях проблему надо занести [дежурным](https://abc.yandex-team.ru/services/search_share_duty/) в [чат](https://t.me/joinchat/4N9Qd83lOWsxNzA6)

## Как убедиться, что это внешнее событие?

Проверить по приборам Долотов и RTMR что выполняются оба условия:
- Выросла доля тематики **Новости или Спорт**
- Изменились абсолюты **и Яндекса, и Гугла**

Если изменились только абсолюты Яндекса, лучше проконсультироваться с дежурным аналитиком доли (возможно, это не внешнее событие, а выкатка Я.Новостей и т.п.)

Например,
 - Изменение доли в Санкт-Петербурге - возможно, играет "Зенит"
 - Изменение доли в Москве - возможно, играет "Спартак", "ЦСКА"

{% cut 'RTMR' %}

**Обратите внимание, что здесь возможен сильный недоезд данных и последние точки могут оказаться аномальными**

[Сылка на прибор](https://datalens.yandex-team.ru/m7vox7sqfm3uj-searchmonitoring)

![1](_imgs/rtmr_1.png)
![1](_imgs/rtmr_2.png)
![1](_imgs/rtmr_3.png)

{% endcut %}

{% cut 'Dolotov' %}

**Какой-нибудь текст**

[Сcылка на прибор](http://dolotov.com/4volozh/search.html#slice=ru/sport&se=13&absolutes=1)

![1](_imgs/dolotov_example.png)

{% endcut %}
