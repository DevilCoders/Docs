## Какую проблему решаем
**TL;DR** Если создать тариф во всех зонах, и **не** вносить в конфиг TARIFF_CATEGORIES_VISIBILITY, то он **будет виден** по умолчанию.

Казалось бы, можно предварительно добавить тариф в \_\_default__. но это не фиксит проблему.

Чтобы тариф не показывался, надо прописывать его во все зоны в конфиге, в которых тариф был заведен.

### Почему добавление в \_\_default__ не помогает
**TL;DR** Эта секция работает, как значение по умолчанию для 1 уровня ключей конфига (это имена геозон).

Если в конфиге не был найден ключ (вызов оператора [string]), то будет использовано значение из \_\_default__
- [uservices link](https://a.yandex-team.ru/arc_vcs/taxi/uservices/userver/core/include/taxi_config/value.hpp?rev=f656ee54cc0a16a57877a1761221ae3199dea5a7#L92)
- [backend-cpp link](https://github.yandex-team.ru/taxi/backend-cpp/blob/9648894971356bf6dd447a313e969db3b620d468/common/src/config/config.hpp#L46)

Для нашего конфига ключ это название зоны. Т.е. \_\_default__ используется, если операционисты создали новую зону, но еще не занесли ее в этот конфиг.

### Какой фикс делаем
Если пара "текущая зона -> текущий тариф" не была найдена, то фоллбэчимся на "\_\_default__ -> текущий тариф". Если такая пара не найдена, то только тогда используем текущее поведение с полной видимостью.

Изменение раскатывать через конфиг.
1) 1 этап - пишем в лог ситуации, когда видимости до и после изменений расходятся. Разбираем кейсы.
2) 2 этап - переключаем полностью.

#### Как править код
В uservices основные изменения:
1) Их мало - достаточно правильно поправить IsCategoryVisibleByExperiments()

В backend-cpp изменения сложнее, потому что [интерфейс библиотеки](https://github.yandex-team.ru/taxi/backend-cpp/blob/067f318a62f33565c598cdb78f5293c289676999/common/src/models/tariffs/visibility_helper.hpp#L17) плохо продуман. Получить настройки видимости для зоны - это действие совершается в бизнес-коде, [пример](https://github.yandex-team.ru/taxi/backend-cpp/blob/23c306a4bd8219e7946124f272a70088d03ad597/protocol/lib/src/views/routestats/data.cpp#L485)
План примерно такой:
1) Немного копипастим новую либу из uservices (и главное - ее интерфейс. См раздел "Будущее")
2) По месту использования TariffCatVisibilitySettings - используем под конфигом новый код.
3) После такого рефакторинга - правим новый код так же, как поправили uservices.

В питонах ничего делать не надо.

### Оценки по времени
1) Поправить uservices - 1 день
2) Найти все места использований в backend-cpp - 1/2 дня
3) Поменять интерфейс (кажется лучше писать код рядом, а не рефачить текущий, частично можно будет копипстнуть из uservices) - 2 дня
4) Поменять все места в коде на новый интерфейс под экспом - 2 дня
6) Тесты на новое поведение в uservices и backend-cpp - 2 дня
5) Аккуратная выкатка рефакторинга - 2 дня
5) Аккуратная выкатка переключения на новую логику - 4 дня

Итого задача займет примерно 3 недели от А до Я.

### Будущее
Лучше хранить видимость тарифа в БД, для этого скорее всего подойдет хранение напрямую в tariff_settings.
Код, который будет написан для быстрофикса, поможет с вендрением новой логики для backend-cpp.

Интерфейс надо [копипастить из uservices](https://a.yandex-team.ru/arc_vcs/taxi/uservices/libraries/tariff-categories-visibility/include/tariff-categories-visibility/visibility_helper.hpp?rev=9be7a155495a96f634c9b003cc4b0604869d04af#L11), его уже сейчас довольно просто перевести на использованаие базы:

```
class VisibilityHelper {
 public:
  virtual UserContext MakeContext(
      const Brand& brand, const std::optional<AppVars>& app_vars,
      const std::optional<UserSource>& user_source,
      const std::optional<PhoneId>& phone_id) const = 0;
  virtual CategoriesVisibilityAttributes GetVisibilityAttributes(
      const UserContext& context, const std::vector<Category>& categories,
      bool supports_hideable_tariffs, const ZoneName& zone_name) const = 0;
  virtual CategoriesVisibilityAttributes GetVisibilityAttributes(
      const UserContext& context,
      const std::vector<taxi_tariffs::models::Category>& categories,
      bool supports_hideable_tariffs, const ZoneName& zone_name) const = 0;
  virtual std::vector<Category> GetFilteredCategories(
      const UserContext& context, const std::vector<Category>& categories,
      const ZoneName& zone_name) const = 0;
  virtual std::vector<taxi_tariffs::models::Category> GetFilteredCategories(
      const UserContext& context,
      const std::vector<taxi_tariffs::models::Category>& categories,
      const ZoneName& zone_name) const = 0;
  virtual ~VisibilityHelper() = default;
};
```

Продуктово как это можно сделать уже продумал Миша Юлдашев [тут](https://st.yandex-team.ru/TAXIPROJECTS-2044#5ffdd8a629a97e251d9ace93)
> Первая итерация: в админке на странице настройки тарифа в зоне добавляем 2 поля:
> - чекбокс "скрытый" - механика: в независимости от других правил видимости скрывает тариф для всех
> - "эксперимент видимости" (имя эксперимента) - тариф будет доступен только пользователям, которые попадают в эксперимент
> и делаем логику на бекенде, которая скрывает по двум указанным полям
>
> Вторая итерация: убираем конфиг TARIFF_CATEGORIES_VISIBILITY
> - переделать конфиг, чтобы при создании новой зоны не нужно было копировать значение из "__default__" - они будут > подмерживаться автоматически. То есть в итоге в зоне нужно будет указать только тот тариф, на который хотим повесить логику. > > Это также значительно уменьшить размер конфига.
> - скрытие тарифов из конфига перенести в добавленное поле в админке "эксперимент видимости" и убрать из конфига
