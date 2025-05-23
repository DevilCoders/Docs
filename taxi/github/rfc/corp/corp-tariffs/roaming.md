# Роуминг в России
https://st.yandex-team.ru/CORPDEV-2229

## Overview Проекта
Для увеличения Decoupling Revenue (DR) необходимо изменить ценообразование тарифов для Корпоративных Клиентов (КК). У каждого КК есть определение “домашняя тарифная зона” (home - может быть списком с несколькими тарифными зонами или вообще пустым, заполняется при создании договора).

(более подробно в связанном тикете)

### Что меняем

Как будет катиться в прод:
- Заводим роуминговый ТП и прописываем его в конфиг (Иван Каплунович)
- Функционал редактирования домашних зон в Админке
  - Ручки
  - Фронт
- Функционал применения роумингового ТП в сервисе тарифов (под Конфигом)
- Включаем в проде (настраиваем в Админке домашние зоны для одного/нескольких клиентов)
- Включаем конфиг CORP_USE_ROAMING
- Раскатываем на большее количество клиентов (нужен скрипт миграции)
- Ждем, проверяем, удаляем конфиг, роуминг работает по-дефолту

Далее расписано подробнее.

#### Создаем роуминговый тарифный план
Это будет единственный тарифный план (по странам), по аналогии с Main.
Пишем его в новый конфиг вида:
CORP_ROAMING_TARIFF_PLANS
```
{
  "rus": {
    "tariff_plan_series_id": "123"
  }
}
```
(по аналогии с CORP_DEFAULT_TARIFF_PLANS)

#### Привязка домашних зон к клиенту
Перечень округов будем хранить в конфиге вида
CORP_ROAMING_ZONES
```
{
  "rus": [
    {
      "name": "br_dalnevostochnyj_fo",
      "name_ru": "Дальневосточный ФО",
    } 
  ]
}
```

##### Ручка списка роуминговых зон
(то, из чего фронт будет давать делать выбор при назначении домашних зон на клиента)
GET corp-clients/v1/roaming-zones?country=rus
возвращает
```
{
  "roaming_zones": [
    {
      "name": "br_dalnevostochnyj_fo",
      "name_ru": "Дальневосточный ФО",
    }
  ]
}
```

##### Ручки домашних зон клиента
GET/POST corp-clients/v1/client-roaming-zones?client_id=111
```
{
  "roaming_zones": [
    {
      "name": "br_dalnevostochnyj_fo",
    }
  ]
}
```

Где это хранить в БД:
Варианты:
1. clients.services.taxi
Плюсы:
- не будет доп запроса в новую табличку в сервисе corp-tariffs в ручке тарифа клиента
- не надо создавать новую табличку
Минусы:
- фронтово функционал домашних зон отделен от редактирования сервисов, на беке это тоже другие ручки
2. новая табличка client_roaming_zones
Плюсы/минусы противоположные плюсам/минусам в п1

Пока склоняюсь к п2

#### Ручка тарифа клиента (в сервисе corp-tariffs)
В [ручке тарифа клиента](https://github.yandex-team.ru/taxi/backend-py3/blob/7c85d9844f48401c7be34b1a30eb919bd893797c/services/corp-tariffs/docs/yaml/api/tariff.yaml#L10) надо определить, входит ли зона заказа в "домашние зоны" клиента, или нет.
(если "домашние зоны" не определены для этого клиента в табличке client_roaming_zones, то ничего не делаем, клиент едет по своему ТП)

Дальше определяем какой ТП будет применяться к этой поездке. 
Либо ТП клиента, либо роуминговый ТП из конфига.
(функционал закрываем конфигом CORP_USE_ROAMING)

Важно: применять роуминговый ТП можно только тогда, если основным ТП клиента является Main (то есть ТП из конфига CORP_DEFAULT_TARIFF_PLANS)

Весь дальнейший флоу (фолбеки и т.п.) остаются без изменений.

Как изменятся тайминги ручки:
- за агломерациями идем в кеш - тайминги не изменятся
- за домашними зонами идем в монгу (с кешированием в мемкеш), тайминги подрастут на 1 запрос в монгу.

##### Кеш агломераций
Чтобы не увеличивать тайминг ручки надо предварительно по АПИ сервиса агломераций получить маппинг тарифная-зона->округ и положить в кеш.

[Описание сервиса агломераций](https://wiki.yandex-team.ru/taxi/backend/architecture/agglomerations/)

Для наших нужд подходит Базовая иерархия, в которой округа определены как ноды
```
br_dalnevostochnyj_fo   - Дальневосточный ФО
br_juzhnyj_fo           - Южный ФО
br_privolzhskij_fo      - Приволжский ФО
br_severo_kavkazskij_fo - Северо-Кавказский ФО
br_severo_zapadnyj_fo   - Северо-Западный ФО
br_sibirskij_fo         - Сибирский ФО
br_tsentralnyj_fo       - Центральный ФО
```

Для кеша можно использовать библиотеку [agglomeration-cache][https://github.yandex-team.ru/taxi/backend-py3/tree/develop/libraries/agglomeration-cache]

В библиотеке есть метод get_nodes_by_tariff_zone, который по тарифной зоне отдает список потомков этой зоны в геоиерархии. Можно использовать этот метод для определения вхождения зоны в округ.

##### Скрипт миграции
Нужен скрипт, который по списку клиентов пропишет им список "домашних зон"


##### Для вновь созданных клиентов определяем зону по городу (пока для оферты)
Сейчас поле для ввода города есть в виджете и форме ввода ИНН (в ЛК при первом входе).
Но это поле не валидируется в обоих случаях.
Кроме того эти 2 источника информации о городе находятся в квантовой перепутанности.
Город с виджета попадает в dbcorp.clients.city, и в заявку.
Но потом при вводе ИНН, если клиент введет другой город, то он заменяется в заявке (но не в клиенте).

Концептуально можно рассматривать эти 2 города в отдельности и не путать их между собой:
1. Город с виджета это фактическое место предоставления услуги клиенту, по нему будем определять домашний округ.
2. Город с формы ИНН (и весь адрес) будем расссматривать как юридический адрес клиента.
3. При редактировании города в форме ИНН не будем подменять city в заявке и клиенте (то есть изменение города в этом месте влечет только изменение юр. адреса)
4. Город в виджете будем валидировать на фронте.
5. Город в ИНН думаю не надо валидировать, ибо 1) возможно что мы не угадаем какой-то город который действительно имеется, 2) юр. адрес только передаем в Баланс, а если потребуется, то можно исправить и в Админке Баланса
