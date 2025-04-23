# Вынос VisibilityHelper из монолита

## Зачем

В данный момент невозможно вынести некоторые ручки из монолита, так как используется логика VisibilityHelper'а в виде общего кода в backend-cpp/common.

## Текущие возможности и потребители

У класса `tariff::VisibilityHelper` следующие содержательные `public`-методы:

- IsHiddenByPaymentMethod: используется как `private`, внешних потребителей нет
- IsHiddenByExperiments: используется как `private`, внешних потребителей нет
- IsHiddenBySubzone: используется как `private`, внешних потребителей нет
- IsHiddenBySelectedClass: используется как `private`, внешних потребителей нет
- IsCategoryVisible: список потребителей ниже
- IsCategoryVisibleForFrontend: список потребителей ниже
- CategoryShouldBeSkipped: список потребителей ниже

Также есть две фабрики для создания хелпера с категориями для бренда/приложения:
- ApplicationBrandTariffs
- GetVisibilityHelperByApplication

### Использование `CategoryShouldBeSkipped`

Вызов `CategoryShouldBeSkipped` происходит в цикле по `tariff_settings.categories`.
Список потребителей:

- ручка zoneinfo (~300 rps)
- ручка personalstate (~1K rps)
- ручка couponcheck (~2 rps)
- ручка couponactivate (~1 rps)
- ручка couponlist (~400 rps)
- логика order_maker (orderdraft + int-api orderdraft) (~100 rps + ~3rps)
- ручка routestats (~1K rps)
- логика pricing_data_preparation - старый прайсинг, останется в продуктовом коде (routestats), в новый прасинг не поедет

Грубая оценка rps по текущим потребителям: ~3K rps

### Использование `IsCategoryVisible`

Вызов `IsCategoryVisible` происходит в цикле по `tariff_settings.categories`.
Список потребителей:

- ручка zonaltariffdescription (protocol + int-api) (~2 rps)
- ручка pricecat (~80 rps)
- ручка tariffs (~1 rps)
- ручка routestats (~1K rps)
- ручка zoneinfo (~300 rps)
- ручка nearestzone (~1K rps)

Грубая оценка rps по текущим потребителям: ~2.5K rps

### Использование `IsCategoryVisibleForFrontend`

Вызов `IsCategoryVisibleForFrontend` происходит в цикле по `tariff_settings.categories`.
Список потребителей:

- ручка sourcezones - сейчас на графиках 0rps

## Предложение по выносу логики

Предлагается вынести логику VisibilityHelper (далее VH) в отдельную библиотеку на языке C++. В результате обсуждения заинтересованными пользователями новой библиотеки было принято решение делать библиотеку только для uservices, отказавшись от поддержки backend-cpp. Это позволит существенно уменьшить сроки разработки, при этом принимается риск, что если очень потребуется доработка логики VH, то ее придется сделать в двух реализациях: новой и старой.

Если появится потребители в backend-py3, для них будет два варианта:
- Сделать сервис поверх библиотеки в uservices. В зависимости от критичности функционала VH для потребителя можно написать толстый клиент к сервису с различными фоллбэками.
- Для каких-то критичных потребителей в py3 можно воспроизвести логику VH в коде на python.

Рассматривалась так же альтернатива библиотеке в виде микросервиса, инкапсулирующего логику VH, однако:
- Добавляется новая точка отказа.
- Увеличатся тайминги из-за походов по сети.
- Высокие требования к производительности сервиса - с текущих потребителей набегает ~5K rps.
- Все равно потребуется толстый клиент, реализующий фоллбэки, так как это критичный функционал.
- Из-за специфики работы VH непросто написать фоллбэк: VH в основном скрывает категории из списка, доступного в зоне. т.е. список категорий в зоне (из `tariff_settings`) не может выступать в качестве дефолта, нужно откуда-то брать еще один дефолтный список категорий для каждой зоны.

В будущем возможен вариант создания сервиса для хранения настроек VH, который заменит текущую систему конфигов. Тогда библиотека на uservices будет ходить за настройками в сервис (и кэшировать их), а логика фильтрации так же будет осуществляться самой библиотекой (толстый клиент). К сервису можно будет сделать удобную админку для редактирования правил отображения категорий. Если это понадобится - будет отдельная проработка.

## Зависимости VH

### tariff_settings

Изначальный список категорий берется из настроек зоны. В текущей реализации в backend-cpp сейчас этот список достается из кэша коллекции `tariff_settings`. Для новых потребителей эта коллекция закрыта сервисом `taxi-tariffs`.

Предлагается в реализации на uservices создать кэш над сервисом `taxi-tariffs` для списка категорий зоны и брать данные из этого кэша. Чтобы обновлять кэш инкрементально, нужно будет сделать новую ручку в сервисе `taxi-tariffs`, которая достает настройки зон, которые обновились после определенного момент времени (времени последнего обновления кэша). Кэш будет реализован в виде отдельной библиотеки, так как в `tariff_settings` есть и другая полезная информация, кроме списка категорий в зоне, которая может кому-то понадобиться.

### geoareas

Категории могут быть скрыты для точек, находящихся в определенной зоне - в методе `VisibilityHelper::IsHiddenBySubzone`. В текущей реализации в backend-cpp для этого используется кэш коллекции geoares.

В проработке [zoneinfo](https://github.yandex-team.ru/taxi/rfc/blob/757c94a0bccc73860f28a171bfe033966d46f478/api-proxy/zoneinfo/visibility_helper.md#%D0%BD%D0%B0%D1%81%D1%87%D0%B5%D1%82-geoareas) Руслан заметил, что эта проверка сейчас фактически не используется. Нужно согласовать с менеджерами ее выпил.

Если все-таки проверку надо будет оставить - предлагается в реализации на uservices использовать библиотеку `client-geoareas`, которая поддерживает кэш коллекции `geoareas`, обновляемый через походы в сервис `geoareas`.

## Входные параметры для VH

Аргументы, для которых формируется список доступных категорий:
- application/brand: разделение категорий по брендам на основе [конфига APPLICATION_BRAND_CATEGORIES_SETS](https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/APPLICATION_BRAND_CATEGORIES_SETS).
- application name & version: видимость категорий для версии приложения на основе [конфига TARIFF_CATEGORIES_ENABLED_BY_VERSION](https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/TARIFF_CATEGORIES_ENABLED_BY_VERSION).
- supports_hideable_tariffs: поддерживаются ли скрываемые тарифы (зависит от потребителя).
- user_source & alice_allowed_tariffs: отдельная проверка для заказов через Алису, alice_allowed_tariffs на самом деле достается из [конфига ALICE_ALLOWED_TARIFFS](https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/ALICE_ALLOWED_TARIFFS).
- selected_class & payment_method: проверяется доступность категории на основе [конфига TARIFF_CATEGORIES_VISIBILITY](https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/TARIFF_CATEGORIES_VISIBILITY). В текущем конфиге на проде эти параметры не используются, используются только эксперименты для включения/отключения видимости.
- experiments: список включенных экспериментов/конфигов пользователя для потребителя tariff_visibility_helper.

## Интерфейс библиотеки

```cpp
struct CheckContext {
  const Brand brand;
  const std::optional<AppVars> app_vars;
  const std::optional<UserSource> user_source;
  const ZoneName zone_name;
  const std::optional<PhoneId> phone_id;
}

struct VisibilityAttributes {
  bool is_visible;
  bool should_be_skipped;
};

using CategoriesVisibilityAttributes =
    std::unordered_map<Category, VisibilityAttributes>;

CategoriesVisibilityAttributes GetVisibilityAttributes(
    const std::vector<Category>& categories, bool supports_hideable_tariffs,
    const CheckContext& context) const;

std::vector<Category> GetFilteredCategories(
    const std::vector<Category>& categories,
    const CheckContext& context) const;
```

Метод `GetVisibilityAttributes` вычисляет атрибуты видимости для тарифов, то есть по сути обрабатывает оба вызова `CategoryShouldBeSkipped` и `IsCategoryVisible`. Это нужно, например, в логике ручки zoneinfo, которая умеет работать со скрытыми тарифами.

Для большинства потребителей достаточно будет вызвать `GetFilteredCategories`, чтобы оставить в списке категорий только видимые.

## Этапы

### Этап 1 (в работе)

Данный этап включает в себя:
- Реализация библиотеки `tariff-categories-visibility` в `uservices`.

Критерий успеха: написана библиотека.

### Этап 2 (в работе)

Данный этап включает в себя:
- Добавление ручки в сервисе `taxi-tariffs`, которая будет нужна для кэша с инкрементальным обновлением.
- Написание библиотеки-кэша в uservices для доступа к тарифам.

Критерий успеха: написана библиотека.

### Этап 3

Данный этап включает в себя:
- Подключение библиотек к новой реализации ручки zoneinfo.
- Сверка двух реализаций (вероятно, средствами api-proxy).

Критерий успеха: расчеты видимости категорий в старом VH и в новой реализации совпадают.
