## Бизнесовая задача

Relates: [TAXIBACKEND-26399](https://st.yandex-team.ru/TAXIBACKEND-26399)

### Описание

Есть много шорткатов, которые предлагают пользователю сделать заказ
в Еде и Лавке, но править их пока что не очень удобно. Нужно создать
инструмент, с помощью которого менеджеры могли бы самостоятельно 
(без привлечения разработчиков) отслеживать и редактировать шорткаты.

### Клиентское API

Ручки:
 * `GET v1/admin/shortcuts/eats/list` - возвращает список шорткатов еды, 
 оставшихся в результате фильтрации (фильтры передаются параметрами)
 * `GET v1/admin/shortcuts/grocery/list` - возвращает список шорткатов лавки, 
 оставшихся в результате фильтрации (фильтры передаются параметрами)
 * `POST v1/admin/shortcuts/eats/update` - редактирует шорткаты еды 
 (можно обновить картинку у бренда)
 * `POST v1/admin/shortcuts/grocery/update` - редактирует шорткаты лавки 
 (можно обновить картинку у категории)

Response `GET v1/admin/shortcuts/eats/list`:
```
{
    "shortcuts": [
        {
            "color": "#F5F4F2",
            "image_tag": "shortcuts_cid9_Italian",
            "place_id": 1,
            "slug": "Holly-Food-by-Bryan",
            "title": "Holly Food by Bryan"
        },
        ...
    ]
```

Response `GET v1/admin/shortcuts/grocery/list`:
```
{
    "shortcuts": [
        {
            "category_id": 282083,
            "color": "#DCE9F5",
            "image_tag": "shortcuts_grocery_cat_cooked_mid2",
            "place_id": 103799,
            "slug": "yandekslavka_zhukovskogo_34",
            "title": "Готовая еда",
            "relevance": 2000
        },
        ...
    ]
}
```

Получение всех шорткатов еды с `brand_id` = 123:
```
GET v1/admin/shortcuts/eats/list?brand_id=123
```

Редактирование шорткатов еды с `brand_id` = 123:
```
POST v1/admin/shortcuts/eats/update

{
    "brand_id": 123,
    "title": "new_awesome_title",
    "image_tag": "new_awesome_image_tag"
}
```

### База данных:
- Хотим хранить информацию в PostgreSQL базе, регулярно обновляя ее

### Как это работает сейчас (19.03.20):
- данные о шорткатах хранятся в таблицах в YT
- nile-скрипты генерят json'ы по этим табличкам
- эти json'ы и являются источником в **eda-shortcuts**

#### Конкретнее:
Для простоты назовем вот 
[эту](https://yt.yandex-team.ru/hahn/navigation?path=//home/taxi-dwh/ods/food/bigfood/place&) 
таблицу _главной_, она выгружается из базы Еды. С вопросами по ней
таблице можно обращаться к [ryurasov](https://staff.yandex-team.ru/ryurasov).
Менеджер - [taniaky](https://staff.yandex-team.ru/taniaky)

[Здесь](https://yt.yandex-team.ru/hahn/navigation?path=//home/taxi_ml/production/eats/shortcuts/resources/foodtech_base&)
 лежат все json'ы, которые берет **eda-shortcuts**. Разберем их по порядку:
- `eats_places_rank_info.json` - информация о ресторанах для ml. Она берется из
 таблицы [places_ranking_info](https://yt.yandex-team.ru/hahn/navigation?path=//home/taxi_ml/tmp/shortcuts/places_ranking_info&),
 которая, в свою очередь, полностью основана на _главной_.
- `grocery_categories_rank_info.json` - информация о магазинах лавки. Она берется
 из таблицы [lavka_categories.csv](https://yt.yandex-team.ru/hahn/navigation?path=//home/taxi_ml/production/shortcuts/eda_shortcuts/grocery/category_static_info/lavka_categories.csv&) 
 и [lavka_metacategories_ranking.csv](https://yt.yandex-team.ru/hahn/navigation?path=//home/taxi_ml/production/shortcuts/eda_shortcuts/grocery/category_static_info/lavka_metacategories_ranking.csv&).
 Эти таблицы выгружаются из базы Еды аналитиками.
- `shortcuts_base.json` - сами шорткаты. Поля в этом файле частично 
 пересекаются с двумя предыдущими. 
 [Здесь](https://yt.yandex-team.ru/hahn/navigation?path=//home/taxi_ml/production/shortcuts/eda_shortcuts/image_tags&) 
 лежат таблицы, созданные вручную (для задания **image_tag**'a каждому шорткату).

### Откуда берем данные:
На данный момент вопрос, откуда брать данные, остается открытым
(UPD 31.03.20: договорились с [privet](https://staff.yandex-team.ru/privet),
что в MVP забираем данные из YT, а потом договариваемся с менеджерами 
и получаем ручки к базе еды). Есть следующие варианты: 
  - идеальный, долгий: забирать из базы. Для этого нужно привлечь разработчиков
   из другой команды (общался с менеджером, нет ресурсов).
  - и так сойдет, быстрый: забирать из YT. Минусы: YT - инструмент для
   аналитиков, гарантий сохранности и консистентности данных нет; 
   отсутствие поддержки в testsuite (невозможность полного покрытия тестами кода) 

### Этапы разработки:

- **Этап 0**:  
    Ручки `v1/admin/shortcuts/eats/list`, 
    `v1/admin/shortcuts/grocery/list` (замена `shortcuts_base.json`). 
    На данный момент будут возвращать ~30 МБ информации в сумме
    (в mvp можно обойтись без пагинации).
    **Eda-shortcuts** вместо загрузки json'а будет ходить в них 
    **по эксперименту** и **через кеширующий компонент**. 
    Каждый запрос к админке инициирует запрос в YT. 
    (1d на ручки + эксперимент, 2d на кеширующий компонент)
- **Этап 1**:  
    Добавляем PG базу. Теперь уже данные для каждого запроса
    берутся из базы, которая периодически обновляется из
    источника (возможно, позже добавится кеширующий компонент,
    но не в mvp). (2d) (+1d, чтобы разобраться с 
    периодическими тасками)
- **Этап 2**:  
    Ручки `/update`. В базу добавляются таблицы, отвечающие за
    image_tag'и и прочие изменяемые параметры. Появляется
    возможность изменять шорткаты. (2d)
- **Этап 3**:  
    Интеграция с АБК (2d)    

### Какая нагрузка ожидается?
  Сервис будет использоваться менеджерами для редактирования
  шорткатов и кеширующими компонентами в eda-shortcuts,
  ожидается не больше 10 rps.
