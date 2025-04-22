# Шаблонизация

Для текстовых блоков производится шаблонизация контента с использованием движка [Jinja2](https://jinja.palletsprojects.com/en/2.11.x/).

### Переменные

Перменные в шаблоне пишутся в двойных фигурных скобках `{{переменная}}`. В результате шаблонизации происходит замена перменной на её значение.

### Проверка условий

Если какой-то блок должен показываться только при определенных условиях, то необходимо обрамить его в `{% if УСЛОВИЕ %}БЛОК{% endif %}`.

Пример:
```
{% if top_hotels_1 %}
  top_hotels_1.name - лучший отель города!
{% endif %}
```

### Обход массивов

Если указано, что какая-то переменная - массив, то с ней надо работать через вот такую конструкцию:
```
{% for item in array %}
    {{ item }}
{% endfor %}
```

Если нужно обойти не весь массив, а только часть, то это делается так:
```
{% for item in array[:3] %}
    {{ item }}
{% endfor %}
```
обойдет только три первых элемента.

Если нужно, для последнего элемента массива можно сделать особенную обработку, например:
```
Отель предлагает
{% for feature in top_hotels_1.top_features %}
{{feature|accusative}}
{% if loop.last %} и {% else %}, {% endif %}
{% endfor %}
```

развернется в `Отель предлагает Wi-Fi, парковку, кондиционер и оплату картой`.

Однако конкретно в этом случае лучше воспользоваться функцией `rjoin` (см. ниже).


### Список имеющихся переменных

- `{{region}}` - имя города или области в именительном падеже, например `Москва`, для склонения используйте фильтр склонений (см. ниже)
- `{{region.hotel_count}}` - количество отелей в городе или области
- `{{region.min_price}}` - минимальная цена в городе или области
- `{{region.median_min_price}}` - медиана минимальных цен в городе или области
- `{{region.has_mir}}` - признак того, что в регионе есть отели, для которых действует акция для карты "МИР"

| Категория          | Минимальная цена                              | Медиана минимальных цен                              |
|--------------------|-----------------------------------------------|------------------------------------------------------|
| 2* отели           | `{{region.min_price_stars_2}}`                | `{{region.median_min_price_stars_2}}`                |
| 3* отели           | `{{region.min_price_stars_3}}`                | `{{region.median_min_price_stars_3}}`                |
| 4* отели           | `{{region.min_price_stars_4}}`                | `{{region.median_min_price_stars_4}}`                |
| 5* отели           | `{{region.min_price_stars_5}}`                | `{{region.median_min_price_stars_5}}`                |
| дешевые            | `{{region.min_price_cheap}}`                  | `{{region.median_min_price_cheap}}`                  |
| с бассейном        | `{{region.min_price_has_pool}}`               | `{{region.median_min_price_has_pool}}`               |
| с частным пляжем   | `{{region.min_price_has_private_beach}}`      | `{{region.median_min_price_has_private_beach}}`      |
| со СПА             | `{{region.min_price_has_spa}}`                | `{{region.median_min_price_has_spa}}`                |
| можно с животными  | `{{region.min_price_animals_allowed}}`        | `{{region.median_min_price_animals_allowed}}`        |
| есть All Inclusive | `{{region.min_price_all_included}}`           | `{{region.median_min_price_all_included}}`           |
| около метро        | `{{region.min_price_near_metro}}`             | `{{region.median_min_price_near_metro}}`             |
| дорогие            | `{{region.min_price_expensive}}`              | `{{region.median_min_price_expensive}}`              |
| с завтраком        | `{{region.min_price_breakfast}}`              | `{{region.median_min_price_breakfast}}`              |
| с питанием         | `{{region.min_price_breakfast_lunch_dinner}}` | `{{region.median_min_price_breakfast_lunch_dinner}}` |
| с баней            | `{{region.min_price_has_bathhouse}}`          | `{{region.median_min_price_has_bathhouse}}` |
| с сауной           | `{{region.min_price_has_sauna}}`              | `{{region.median_min_price_has_sauna}}` |

В качестве `region` нужно использовать `city` (для города) или `state` (для области)

#### Топы отелей

Переменные имеют формат `{{TOPNAME_N}}`, где `TOPNAME` - имя списка топов (см. ниже), а N - порядковый номер в топе, от 1 до 3.
В топе может быть и менее 3 отелей, поэтому важно обращения к топу обрамлять условием: `{% if TOPNAME_N %} ... {% endif %}`

**Список доступных топов отелей**:

- `top_hotels` - общий топ отелей по городу или области
- `top_hotels_stars_2` - топ 2* отелей
- `top_hotels_stars_3` - топ 3* отелей
- `top_hotels_stars_4` - топ 4* отелей
- `top_hotels_stars_5` - топ 5* отелей
- `top_hotels_has_spa` - топ отелей со SPA
- `top_hotels_animals_allowed` - топ отелей, куда можно с животными
- `top_hotels_cheap` - топ отелей с ценовой категорией `hotel_price_cheap`
- `top_hotels_has_pool` - топ отелей с бассейном
- `top_hotels_has_private_beach` - топ отелей с частным пляжем
- `top_hotels_near_metro` - топ отелей около метро
- `top_hotels_all_included` - топ отелей, в которых есть All Inclusive предложения
- `top_hotels_expensive` - топ отелей с ценовой категорией `hotel_price_expensive`
- `top_hotels_breakfast` - топ отелей с завтраком
- `top_hotels_breakfast_lunch_dinner` - топ отелей с питанием
- `top_hotels_has_bathhouse` - топ отелей с баней
- `top_hotels_has_sauna` - топ отелей с сауной

Каждая переменная  `{{TOPNAME_N}}` описывает один отель и **имеет следующие поля**:

- `{{TOPNAME_N.name}}` - имя отеля
- `{{TOPNAME_N.median_min_price}}` - минимальная цена на размещение в отеле
- `{{TOPNAME_N.stars}}` - кол-во звёзд. Может отсутствовать!
- `{{TOPNAME_N.rating}}` - Рейтинг отеля, от 1 до 5
- `{{TOPNAME_N.top_features}}` - топ фичи: массив с именами топ фичей ("Wi-Fi", "Бассейн"...)
- `{{TOPNAME_N.price_category}}` - ценовая категоря отеля: `hotel_price_cheap`, `hotel_price_reasonable`, `hotel_price_expensive` или `hotel_price_very_expensive`. Это значение соответствующего [признака в алтае](https://altay.yandex-team.ru/features/3501616848).
- `{{TOPNAME_N.has_pool}}` - есть бассейн или нет (для проверки через `{% if .has_pool %})`
- `{{TOPNAME_N.has_private_beach}}` - есть частный пляж или нет (для проверки через `{% if .has_private_beach %})`
- `{{TOPNAME_N.has_spa}}` - есть SPA или нет (для проверки через `{% if .has_spa %})`
- `{{TOPNAME_N.animals_allowed}}` - можно ли с животными (для проверки через `{% if .animals_allowed %})`
- `{{TOPNAME_N.link}}` - генерирует ссылку на отель


#### Аэропорты и вокзалы

Доступны для каждого города в виде массивов `{{airports}}` и `{{train_stations}}` соответственно.
Элементы массивов можно перебрать через `{% for item in airports %} .. {% endfor %}`.

Каждый элемент `item` массива содержит следующие поля:

`{{item.name}}` - название аэропорта/вокзала

`{{item.top_hotels_N}}` - топ отелей в радиусе 2км от аэропорта/вокзала. Правила работы и поля - такие же как в "Топах отелей"

Пример:

Шаблон
```
{% for ap in airports %}
<br>Около аэропорта {{ ap.name }} находятся отели: {{ap.top_hotels_1.name}} {% if ap.top_hotels_2 %} и {{ap.top_hotels_2.name}} {% endif %}
{% endfor %}
```

Для Москвы даёт такой текст:
```
<br>Около аэропорта Шереметьево находятся отели: Novotel Москва Аэропорт Шереметьево  и Sheraton Sheremetyevo
<br>Около аэропорта Внуково находятся отели: DoubleTree by Hilton Moscow - Vnukovo Airport  и Транзит-Внуково
<br>Около аэропорта Домодедово находятся отели: Аэротель  и Аэротель Экспресс
```

### Склонения

Все шаблонные данные могут склоняться.
Для этого сипользуется [механизм фильтров движка Jinja2](https://jinja.palletsprojects.com/en/2.11.x/api/#custom-filters)
Доступны следующие склонения:

- `{{item|nominative}}` - имя города в именительном падеже, например `Москва`
- `{{item|genitive}}` - имя города в родительном падеже, например `Москвы`
- `{{item|dative}}` - имя города в дательном падеже, например `Москве`
- `{{item|accusative}}` - имя города в винительном падеже, например `Москву`
- `{{item|instrumental}}` - имя города в творительном падеже, например `Москвой`
- `{{item|prepositional}}` - имя города в предложном падеже, например `Москве`
- `{{item|preposition}}` - предлог (в, на) для предложного падежа, например `в`
- `{{item|locative}}` - тоже самое что для и `{{city.preposition}} {{city.prepositional}}`, например `в Москве`
- `{{item|directional}}` - тоже самое что для и `{{city.preposition}} {{city.accusative}}`, например `в Москву`
- `{{item|ablative}}` - тоже самое что для и `из {{city.genitive}}`, например `из Москвы`

### Перечисления

Для "красивого" объединения массива строк можно использовать функцию `rjoin`
`rjoin(array, declension: str = None, limit: int = None, joiner: str = ', ', joiner_last: str = ' и ') -> str:`
* 1й параметр - обязательный, в него нужно передать массив строк.
* 2й параметр `declension` - склонение, например `'accusative'`, если не указано, то склонение не производится
* 3й параметр `limit` позволяет ограничить длину массива для объединения
* 4й параметр `joiner` задаёт основной "склеиватель" строк
* 5й параметр `joiner_last` задаёт "склеиватель" строк для последнего склеивания

Примеры:

 `{{rjoin(top_hotels_1.top_features, declension='accusative')}}` -> `'Wi-Fi, парковку и оплату картой'`
 `{{rjoin(top_hotels_1.top_features, declension='accusative', limit=2)}}` -> `'Wi-Fi и парковку'`


### Примеры использования

**Топ отели**

Шаблон:

```yaml
title: В каких отелях в {{city.locative}} лучше всего остановиться?
content: >
  {{top_hotels_1.name}} – одно из самых любимых мест клиентов Яндекс.Путешествий.
  Этот {{top_hotels_1.stars}}-звёздочный отель предлагает {% for f in top_hotels_1.top_features %} {{f}} {% endfor %}
  Отзывы с нашего сайта также рекомендуют {{top_hotels_2.name}} и {{top_hotels_3.name}} в качестве лучших вариантов для вашего путешествия.
```

Рендерится как:
```yaml
title: В каких отелях в Москве лучше всего остановиться?
content: >
  Рэдиссон славянская – одно из самых любимых мест клиентов Яндекс.Путешествий.
  Этот 4-звездочный отель предлагает Wi-F} и парковку.
  Отзывы с нашего сайта также рекомендуют {Название отеля, ссылка} и {Название отеля, ссылка} в качестве лучших вариантов для вашего путешествия.
```
