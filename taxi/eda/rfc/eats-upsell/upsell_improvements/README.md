# Новая архитектура апсейла

Tickets:
* [EDACAT-2227](https://st.yandex-team.ru/EDACAT-2227)

Ответственные разработчики:
* [@egor-sorokin](https://staff.yandex-team.ru/egor-sorokin)
* [@udalovmax](https://staff.yandex-team.ru/udalovmax)

## Термины

* [Апсейл](https://wiki.yandex-team.ru/eda/team/backend/cat/advertisements/#apsejjl) - подбор товаров/блюд (далее товар = товар или блюдо), рекомендуемых к покупке вместе с теми что пользователь видит в корзине/на карточке товара.
* Рекомендуемый товар - товар, релевантный пользователю по некоторому набору признаков (реклама, история заказов, сопокупаемость, популярность и т.д.).
* Промо товар - рекламируемый в рамках какой-либо промо компании.
* Товар-кандидат - товар, который может оказаться релевантным для пользователя, но еще не добавлен в итоговый ответ апсейла.
* [Категорийный апсейл](https://wiki.yandex-team.ru/eda/team/backend/cat/advertisements/#kategorijjnyjjapsejjl) - правила, по которым товар может попасть в ответ апсейла, только если в корзину добавлен товар из определенной категории (имеет смысл только в ритейле).

## Текущий алгоритм апсейла

Подбор апсейла для ритейла и ресторанов почти не отличается, но живет в разных ручках. Сейчас апсейл работает следующим образом:

1. Клиент присылает запрос в сервис eats-upsell с набором товаров которые пользователь видит в своей корзине или на карточке товара.
2. Собираем данные о товарах которые уже видит пользователь и о плейсе для которого сделан запрос.
3. Идем за рекомендациями в umlaas-eats:
    * На основе экспериментов, истории заказов, ML ресурсов и т.д. получаем набор товаров-кандидатов, которые мы можем порекомендовать пользователю.
    * Для товаров-кандидатов начисляется некий score (на основе популярности, истории заказов и т.д.).
    * Сортировка по score.
    * Результат дедуплицируется и формируется ответ.
4. eats-upsell добавляет к рекомендациям набор промо товаров (извлекаются из YT).
5. Запрашиваем данные о результирующем наборе товаров (промо + рекомендации), в частности, их доступность.
6. Применяем дополнительные настройки, такие как категорийный апсейл, верхний и нижний лимиты на кол-во товаров в ответе и т.д.
7. Результат отдается пользователю.

## Проблемы

1. Сервис umlaas-eats отвечает за подбор рекомендаций, но не может расчитывать на конкретный порядок и кол-во рекомендуемых товаров, так как далее вмешивается eats-upsell со своими настройками и промо товарами.
2. Некоторые рекомендуемые товары могут оказаться недоступны.
3. Логика формирования апсейла размазана по нескольким сервисам.
4. В будущем могут появиться дополнительные источники товаров для апсейла. Хочется иметь возможность безболезненно влить новые данные в результат отдаваемый пользователю.

Необходимо найти способ контролировать конечного списка рекомендуемых товаров с учетом рекламы, доступности товаров и других возможных факторов, то есть когда все необходимые данные будут уже на руках. При этом нужно иметь четкое ограничение зон ответственности команд Рекламы (подмешивание рекламы, топселлеров и т.д.) и ML (подбор релевантных пользователю товаров, сортировка результата). 

## Предлагаемое решение

Предлагается отложить ML сортировки и преобразования списка товаров-кандидатов до того момента, когда будут доступны все данные о конечном наборе товаров, то есть когда мы уже получим набор промо и доступность товаров. Таким образом появится возможность формировать конечный ответ с релевантными товарами не наугад, как это происходит сейчас.

Данные для формирования конечного апсейла могут быть получены из различных источников данных: реклама, треугольник, история заказов, популярные и т.д. Предлагается сделать каждый из таких источников отдельной сущностью, реализующей общих интерфейс. Каждый источник запрашивается асинхронно и контролируется конфигом. Под капотом каждый источник формирует запрос в нужный ему сервис/базу/кэш. После того как все данные и доступность товаров получены, источники данных могут применить свои кастомные сортировки или фильтры. Таким образом, можно будет независимо развивать и экспериментировать с разными источниками данных для апсейла.

### Предлагаемый алгоритм работы апсейла

1. Клиент присылает запрос в сервис eats-upsell с набором товаров которые пользователь видит в своей корзине или на карточке товара.
2. Собираем данные о товарах которые уже видит пользователь и о плейсе для которого сделан запрос.
3. По конфигам 3.0 получаем набор источников, из которых можно запросить товары-кандидаты для апсейла.
4. Асинхронно запрашиваем нужные данные из собранных источников данных. Данные приходят в неотсортированном виде, дополнены некоторым "скором" и признаками, которые будут применены для дальнейшей дедупликации и сортировки. В качестве этих признаков могут быть использованы популярность товара, сопокупаемость, "рекламность" товара, участие его в золотом треугольнике и т.д.
5. Запрашиваем данные о товарах из каждого источника: доступность, скидки, акции, данные для отображения на фронте и т.д.
6. Фильтруем товары по доступности (и возможно каким то еще факторам)
7. Каждый источник данных может применить собственный фильтр или модификатор товаров (контролируется экспериментами с приоритетом, фильтры могут быть вынесены в библиотеки).
8. Собираем общий результат апсейла, сортируем его на основе скора товаров и дедуплицируем.
9. Формируем конечный ответ пользователю.

### Необходимые изменения

С точки зрения сервисной архитектуры аггрегация данных из источников будет происходить на стороне сервиса eats-upsell. В качестве источников данных выступают сервисы umlaas-eats, eats-orderhistory, рекламный кэш YT и т.д. Сортировка и фильтрация данных так же происходит на стороне eats-upsell, контролируется экспериментами, а конкретные кастомные фильтры и сортировки могут поставляться в код сервиса в виде библиотек, поддерживающих общий интерфейс.

Основной источник данных сейчас это umlaas-eats, у которого имеется по отдельной ручке на ритейл и рестораны. Но раз теперь не требуется дополнительной логики фильтрации и сортировки этих данных в umlaas-eats, то можно статические ML ресурсы постепенно перенести в eats-upsell. Для этого нужно будет подключить туда ML библиотеку, наладить поставку ML ресурсов и подключить логирование.

Для остальных источников данных, которые остаются в umlaas-eats (если таковые будут), есть несколько вариантов:

1. Отдавать все данные как данные из одного источника "рекомендуемые" (как это сделано сейчас).
Pros:
    - не нужно почти никаких доработок в спеке и коде сервиса umlaas-eats
    - получаем все данные одним запросом
Cons:
    - все товары сливаются в один список и не получится отличить популярный товар от сопокупаемого, или рекомендованного в данной категории
2. Разбить запрос и ответ существующих ручек на блоки для каждого источника данных.
Pros:
    - получаем все необходимые данные одним запросом
    - ручка уже собирает все данные, нужна лишь небольшая доработка спеки и кода
Cons:
    - на стороне eats-upsell нужно будет иметь дополнительную прослойку между интерфейсом источников данных и ручкой umlaas, так как несколько источников товаров будут идти в одну ручку
    - раздутая спека ручки, в которую складываем все подряд
3. Завести отдельную ручку под каждый источник данных.
Pros:
    - честная независимость кода и экспериментов для разных источников
    - на стороне eats-upsell четкое соответствие источник данных <-> ручка umlaas
Cons: 
    - лишние походы по сети
    - необходима доработка на стороне umlaas по разбиению кода на разные ручки

Кажется, что третий вариант наиболее предпочтителен, но идти к нему можно постепенно через второй.

Для независимых экспериментов и разработки фильтрацию и сортировку апсейла предлагается унести в MLную библиотеку, а затем использовать в eats-upsell после того, как будут доступны товары из всех источников и полная информация по ним.

На стороне eats-upsell необходимы большие доработки (закрытые конфигом на время переезда):
1. Общий интерфейс источников данных и товаров-кандидатов.
2. Асинхронное получение товаров-кандидатов из источников (каждый под отдельным конфигом).
3. 
3. Встроить фильтрацию и сортировку данных из ML библиотеки. В идеале конечно хочется иметь общий интерфейс фильтров и сортировок для товаров из разных источников данных, но кажется это можно отложить.

Предложенный [@udalovmax](https://staff.yandex-team.ru/udalovmax) интерфейс источников данных:

```
enum class RecommendationType {
  kComplement,
  kPopular,
  kAdvert,
  kRandom,
  kExplore,
  kHistorical,
};

struct RecommendationItem {
  ItemId item_id;
  double score;
  RecommendationType type;
};

class Source {
public:
  virtual std::vector<RecommendationItem> GetRecommendationItems() const = 0;

  virtual RecommendationType GetRecommendationType() const = 0;
};

class Complement : public Source {}; // этот источник развивает команда ml
class Popular : public Source {};
class Advert : public Source {}; // а этот - реклама
class Random : public Source {};
class Explore : public Source {};
class Historical : public Source {};
class RetailPersonal : public Source{}; // а этот - кто-то в ритейле
class MenuPersonal : public Source{}; // а этот - кто-то из стрима выбора

using Factory = std::unordered_map<RecommendationType, const std::shared_ptr<Source>>;

Response Handle() {
  const auto source_settings = GetSourceSettings();
  const auto sources = GetSources(Factory, source_settings);
  
  using TaskResult = std::pair<RecommendationType, std::vector<RecomenndationItem>>;
  std::vector<utils::Task<std::vector<TaskResult>>>
  for (const auto& source : sources) {
    tasks.emplace_back(utils::Async(source.Name(), [&source]() { 
       return std::make_pair(source.GetType(), source.GetRecommendations(...));
    }));
  }

  std::unordered_map<RecommendationType, std::vector<RecommendationItem>> recommendations;
  for (auto& task : tasks) {
   auto [type, recs] = task.Get();
   recommendations[type] = std::move(recs);
  }
  
  const auto items_info_task = GetItemsInfo(recommendations);
  const auto items_categories_task = GetItemsCategoriesTask(recommendations);
  const auto items_discounts_task = GetItemsDiscounts(recommendations);

  const auto items_info = items_info_task.Get();
  const auto items_discounts = items_discounts_task.Get();
 
  recommendations = FilterRecommendations(std::move(recommendations), items_info, items_discounts);
  recommendations = SortRecommendations(std::move(recommendations), items_info, items_discounts);

  const auto items_categories = items_categories_task.Get(); 
  recommendations = ApplyCategories(std::move(recommendations), items_categories);

  // вот тут начинаются все продуктовые эксперименты по сортировке
  ResponseBuilder builer(items_info);

  const auto sort_settings = GetSortSettings();
  for (const auto& sort_setting : sort_settings) {
    const auto recs = recommendations.find(sort_setting.type); // чтобы дать какой-то приоритет друг над другом экспериментом, например
    builer.Add(recs);
  }
 
  return builder.Build();
}
```

### Дополнительно:

В рамках переделки апсейла можно сразу перейти на использование новых сервисов:
1. eats-rest-menu-storage - для получения данных о блюдах, вместо медленного и устаревшего eda-core. Если необходимо переходить на использование новых универсальных id, то лучше унести это в отдельную историю.
2. eats-menu-categories - для получения данных о категориях меню и рекомендациях на основе этих категорий в umlaas-eats. Сейчас правила маппинга [категория -> рекомендуемые категории] живут в Экспериментах 3.0, а соответствия между товарами и категориями достаются из umlaas'ных ресурсов.
