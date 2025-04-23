# eats-menu-item-tags

Сервис разметки категорий блюдам и товарам ресторанов в Я.Еде.

## ToC

1. [Зачем нужен сервис продуктово](#motivation)
2. [Глоссарий](#glossary)
3. [Архитектура и организация сервисов](#architecture)
	1. [CRUD для категорий](#categories-crud)
	2. [Правила](#rules-dev)
		1. [Типы правил](#rules-types)
		2. [CRUD для правил](#rules-crud)
	3. [Processing](#processing)
	4. [Поставищики данных для процессинга](#processing-data-source)
		1. [Full table scan](#processing-data-source-full-scan)
		2. [Updated at table scan](#processing-data-source-updated-at-scan)
		3. [Manual force update API](#processing-data-source-force-update)
	5. [Common API](#common-api)
4. [Потребители](#api-consumers)
5. [Схемы](#schemas)
6. [Как будем программировать и запускать в прод](#so-we-want-to-start-doing-something)
7. [Дальнейшее развитие](#further-work)


<a id="motivation"></a>

## Зачем нужен сервис продуктово

Нужно иметь возможность проставлять общие категории блюдам в разных ресторанах
Еды, а также этими категориями управлять.

Знание о том, что:

- есть категории
- есть N категорий в M ресторанах
- есть N блюд в категории A
- etc

позволит другим, показывающим меню сервисам Еды, персонализировать и менять
свой ответ таким образом, чтобы, например, строить "золотой треугольник QSR".

Продуктовая ценность будет для тикетов по увеличению среднего чека по сервису: [https://st.yandex-team.ru/PMOFFICEPOPS-8](https://st.yandex-team.ru/PMOFFICEPOPS-8)
и [https://st.yandex-team.ru/TAXIML-4446](https://st.yandex-team.ru/TAXIML-4446).

<a id="glossary"></a>

## Глоссарий

- **категория** - категория, созданная контентом или менеджером; например: Бургер
- **правило** - предикат, который принимает на вход блюдо ресторана и возвращает
  массив категорий; правило может как устанавливать на блюдо категории, так и
  снимать с блюда категории;

<a id="architecture"></a>

## Архитектура и организация сервисов

<a id="categories-crud"></a>

### CRUD для категорий

Сервис предоставляет CRUD API для управления категориями:

- создать категорию
- показать все категори
- показать категорию по id и по слагу
- включить/выключить группу категорий

NOTE: Модифицирующие ручки этого API точно должны быть закрыты драфтами, но я
пока не смотрел, как их подключать.

Сами категории хранятся в postgres в таком DDL:

```sql
CREATE TYPE category_status AS ENUM ('draft', 'published', 'hidden');

CREATE TABLE categories AS (
  id			UUID			NOT NULL PRIMARY KEY,
  slug			TEXT			NOT NULL UNIQUE,
  name			TEXT			NOT NULL,
  status		category_status NOT NULL DEFAULT 'draft',
  created_at	TIMESTAMPTZ		NOT NULL DEFAULT NOW(),
  updated_at	TIMESTAMPTZ		NOT NULL DEFAULT NOW()
);
```

NOTE: Хочу добавить еще `draft_id`, но не уверен, что это должно быть в этой
таблице.

```cpp
// models/category.hpp

#pragma once

namespace eats_categories::models {

using CategoryId = ::utils::StrongTypedef<
  class CategoryIdTag, std::string, ::utils::StrongTypedefOps::kCompareStrong>;

using CategorySlug = ::utils::StrongTypedef<
  class CategorySlugTag, std::string, ::utils::StrongTypedefOps::kCompareStrong>;

enum class CategoryStatus {
  kDraft,
  kPublished,
  kHidden,
};

struct Category {
  CategoryId category_id{};
  CategoryStatus category_status{};
  CategorySlug category_slug{};
  std::string name{};
  std::chrono::system_clock::timepoint created_at{};
  std::chrono::system_clock::timepoint updated_at{};
};

} // eats_categories::models
```

<a id="rules-dev"></a>

### Правила

Правило необходимо для того, чтобы создать соответсвие товар -> категория.
Правила могут возвращать набор категорий с весом, с которым эта категория
соответствует товару, т.н. mapping-правила.
Правила могут возвращать набор категорий, которые точно не соответствуют
товару, т.н. исключающие или unmapping-правила.

Правило предоставляет из себя следующее:

```cpp
namespace eats_categories::models {

struct MenuItem {
  PlaceId place_id{};
  ItemId  item_id{};
  // other data
};

struct MappedCategory {
  CategoryId category_id{};
  double score{};
};

class MappingRule {
  public:
    // @brief Возвращает набор категорий, к которым относится блюдо.
    virtual std::vector<MappedCategory> Map(const MenuItem&) const = 0;
};

class UnmappingRule {
  public:
    // @brief Возвращает набор категорий, которые не должны быть
    // аттрибуцированы к блюду.
    virtual std::vector<CategoryId> Unmap(const MenuItem&) const = 0;
};

} // eats_categories::models
```

<a id="rules-types"></a>

#### Типы правил

Правила бывают разных типов. На данный момент известны следующие:

- PhotoShazamProvider - провайдер правила, размечающего блюдо по фотографии
- PredicateRulesProvider - провайдер составных предикатных правил

<a id="rules-crud"></a>

#### CRUD для правил

Сервис предоставляет CRUD API для управления правилами "навешивания" и
"снятия" категорий с блюд:

Схема описана в [docs/yaml/api/rules.yaml](docs/yaml/api/rules.yaml).

NOTE: Модифицирующие ручки этого API точно должны быть закрыты драфтами, но я
пока не смотрел, как их подключать.

<a id="processing"></a>

### Processing

Процессингом называется процесс, проставляющий товарам в соответсвие
категории, а также сохраняющий записи о товарах.

Соответствие хранится в таблице такого вида:

```sql
CREATE TABLE items_categories AS (
  item_id     TEXT NOT NULL PRIMARY KEY,
  category_id UUID NOT NULL PRIMARY KEY REFERENCE categories.id,
  rule_id     UUID NOT NULL REFERENCE rules.id,
  created_at  TIMESTAMPTZ NOT NULL DEFAULT NOW()
);
```

Записи о товарах хранятся в таблице вида:

```sql
CREATE TABLE place_items AS (
  place_id   TEXT        NOT NULL PRIMARY KEY,
  item_id    TEXT        NOT NULL PRIMARY KEY,
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);
```

Нужно учесть, что:

- товаров, которые нужно размечать, миллионы;
- одна итерация "разметки" не должна длиться сутками;
- один товар в единицу времени может только один инстанс сервиса

Процессингом занимается специальный обработчик, читающий из logbroker сообщения
следующего вида:

```json
{
  "id": 1,
  "updated_at": "2021-11-25T13:00:00",
  "force_update": false,
  ...
  "name": "огурец"
}
```
код обработки такого сообщения может выглядеть следующим образом:

```cpp
using MappingRule = const std::shared_ptr<const models::MappingRule>;
using UnmappingRule = const std::shared_ptr<const models::UnmappingRule>;

std::vector<MappingRule> GetMappingRules(const Task& task, const Dependencies& deps);
std::vector<UnmappingRule> GetUnmappingRules(const Task& task, const Dependencies& deps);

void Save(const Dependencies& deps,
          PlaceMenuItem&& item,
          std::vector<Category>&& categories);

bool ShouldUpdate(const Dependencies& deps, const PlaceMenuItem&);

void Perform(Task&& task, Dependencies&& deps) {
    const auto mapping_rules = GetMappingRules(task, deps);
    const auto unmapping_rules = GetUnmappingRules(task, deps);

    auto menu_item = ParseMenuItem(task);
    if (!ShouldUpdate(deps, menu_item)) {
        return;
    }

    std::vector<CategoryId> categories;
    for (const auto& rule : mapping_rules) {
        categories.insert(categories.end(), rule->Map(menu_item));
    }

    for (const auto& rule : unmapping_rules) {
        categories.erase(rule->Unmap(menu_item));
    }

    Save(deps, std::move(menu_item), std::move(categories));
}
```

Решение о том, стоит ли переразмечать товар, принимается на основе:

- `force_update` поля товара, полученного из logbroker
- `updated_at` поля товара, полученного из logbroker, больше updated_at товара
   в таблице place_items
- `updated_at` поля записи о товаре в place_items отстает от now() на какой-то
   конфигурируемый порог

Схема процессинга выглядит так:

![map_categories](img/map_categories.svg)

<!--
@startuml img/map_categories.svg

title Процесс разметки товара/блюда тегами


:eats-menu-item-tags вычитывает сообщение из logbroker;
note
Сообщение представляет из себя json с данными о товаре/блюде:
{
  "id": 1,
  "force_update": false,
  "updated_at": "2021-11-25T13:00:00",
  ...
  "name": "огурец"
}
endnote

:eats-menu-item-tags проверяет, что товар нужно переразметить;
partition "проверка, что товар нужно размечать" {
  if (флаг item.force_updated не установлен или выключен) then (да)
    :получаем из postgres.place_items товар по его id;
    if (смогли найти товар в БД) then (да)
      if (товар в БД обновлен позже updated_at товара из logbroker) then (да)
        stop
      endif
    endif
  endif
}

partition "разметка товара тэгами" {
  :eats-menu-item-tags получает все включенные на данный момент правила;
  if (смогли получить правила) then (нет)
    stop
  endif

  :eats-menu-item-tags формирует список тегов, которые соответствуют товару;
  note
  const std::vector<const std::shared_ptr<const models::MappingRule>> map_rules;
  const std::vector<const std::shared_ptr<const models::UnmappingRule>> unmap_rules;

  std::vector<Category> result;
  for (const auto map_rule : map_rules) {
    result.insert(result.end(), map_rule->Map(item));
  }
  for (const auto unmap_rule : unmap_rules) {
    result.erase(unmap_rule->Unmap(item));
  }
  endnote

  :eats-menu-item-tags запускает создает транзакцию в БД;
  :eats-menu-item-tags удаляет старые записи в таблице items_categories;
  :eats-menu-item-tags обновляет запись по товару в таблице place_items;
  :eats-menu-item-tags коммитит транзакию;
  if (транзакция упала с ошибкой) then (да)
    stop
  endif
}

:eats-menu-item-tags успешно разметил товар тегами;

@enduml
-->

<a id="processing-data-source"></a>

### Поставищики данных для процессинга

Топик в logbroker, из которого читает процессинг, нужно наполнять данными.

<a id="processing-data-source-full-scan"></a>

#### Full table scan

CRON-задача, которая раз в N времени обходит MySQL Bigfood-реплику и перечитывает
таблицу `place_menu_items`.
Каждую строчку она отправляет в logbroker.

<a id="processing-data-source-updated-at-scan"></a>

#### Updated at table scan

CRON-задача, которая раз в N времени обходит MySQL Bigfood-реплику и ищет
записи в таблице `place_menu_items`, которые обновились (поле `updated_at`)
после последнего запуска этой CRON-задачи.
Все найденные строчки отправляются в logbroker.

<a id="processing-data-source-force-update"></a>

#### Manual force update API

API поверх py3-сервиса, которое вычитывает запись из MySQL Bigfood-реплики из
таблицы `place_menu_items` по ID товара, и отправляет его в logbroker со
значением поля `force_update` выставленным в true.

<a id="common-api"></a>

### Common API

CommonAPI это общее API для получения категорий конкретных товаров или
товаров определенных категорий.

Схема описана в [docs/yaml/api/common-api.yaml](docs/yaml/api/common-api.yaml).

Для того, чтобы ручка поиска товаров определенной категории в ресторане могла
работать эффективно, процессинг также будет обновлять следующую таблицу:


<a id="api-consumers"></a>

## Потребители

Сейчас сервис будет использоваться только в umlaas-eats для составления
"треугольника QSR-ов" при апсейле на корзине.

Схематично это выглдяит так:

![umlaas-eats-triangle](img/umlaas-eats-triangle.svg)

<!--
@startuml img/umlaas-eats-triangle.svg

title Сбор золотого треугольника в umlaas-eats;

start

:umlaas-eats получает запрос на рекомендации для апсейла на корзине;
:umlaas-eats запрашивает у eats-menu-item-tags данные о категориях товаров,
которые есть в корзине;
note
Для этого используется запрос из common-api:
POST /internal/eats-menu-item-tags/v1/items-categories
endnote
:umlaas-eats проверяет по своим предикатам, товары каких категорий нужно
порекомендовать, чтобы достроить треугольник;
:umlaas-eats запрашивает у eats-menu-item-tags категории из ресторана;
note
Для этого используется запрос из common-api:
POST /internal/eats-menu-item-tags/v1/place-category-items
endnote
:umlaas-eats достраивает треугольник, ранжирует ответ и возвращает рекомендации;

stop

@enduml
-->

<a id="schemas"></a>

## Схемы

![img](img/all_schemas.jpg)

<a id="so-we-want-to-start-doing-something"></a>

## Как будем программировать и запускать в прод (a.k.a "за неделю")

1. Запросить арх.ревью с сервисом eats-menu-item-tags
   и postgres под ними, а также кронами, которые пишут в lb.
2. Создать сервисы-заглушки.
3. Начать параллельную разрабокту:
   - хранение, получение и изменение категорий
   - хранение, получение, создание и изменение правил
   - API для получения маппингов (common-api)
   - cron: full-update
   - cron: read updated
   - py3 api
   - процессинг
4. Как только будет готов common-api, запустим стрельбы (чтобы не блокироваться
   о все остальное)
5. В этот момент пустим трафик из umlaas-eats на чтение common-api; все еще
   неотрывно смотрим в мониторинги и докидываем железа к БД, на всякий случай.

<a id="further-work"></a>

## Дальнейшее развитие

Если поймем, что при процессинге товаров упираемся в CPU и это мешает CommonAPI,
то выселим это API в отдельный сервис.

