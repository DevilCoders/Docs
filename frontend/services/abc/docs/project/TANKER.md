# Tanker

Конфигурация танкера лежит в директории `.tanker`

Документация https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/tanker-kit

В нашей интеграции танкера:

- для js - кастомный загрузчик на основе серпового
- для ts - кастомный загрузчик на основе серпового

А теперь подробнее

#### для js технологий (react):

tanker.branch = bem

`.tanker/getKeyset.js` - маппер из path в keyset

пример:
```
src/features/Foo                   -> Foo
src/features/Foo/components/Bar    -> Foo/Bar
src/common/components/Foo          -> common/Foo
```
(в итоге используется при пуше)

И затем при пулле, происходит практически обратная операция

`.tanker/json2bem_features` - сделан для того, 
чтобы правильно расскладывать переводы на уровне фич, компонентов.

пример:
```
Foo          -> src/features/Foo
Foo/Bar      -> src/features/Foo/components/Bar
common/Foo   -> src/common/components/Foo
```

#### для ts технологий (react):

tanker.branch = ts

Продублировал код для js технологий, с поправкой на ts

Со всеми его минусами:

- `tanker pull` - не работает, самописный диспатчер работает только с единичными файлами

- `tanker sync` - стягивает все ключи из танкера - не смотря на используемость.
  Но это и к лучшему, потому что используем "корневые" кейсеты для компонентов внутри - пример `src/features/Catalogue/components/Filters/components/Search/Search.js`, 
  если бы смотрели на используемость в корневых лежали бы только ключи последнего синхронизируемого файла.

  см. `@yandex-int/tanker-helpers/dispatchers/ts_dispatcher.js` - использует новую версию серпового - там только используемые ключи складываются:
  https://github.yandex-team.ru/search-interfaces/frontend/blob/master/packages/tanker-kit/ext/dispatchers/json2bem_serp.js#L98

  В принципе поэтому нам не подходит серповый диспатчер - при парсинге кейсет определяется из имени директории откуда импортируется, матчится без преобразований которые делались на этапе резолвинга.

- класть может только в три места:
  - src/common/components
  - src/features
  - src/features/Foo/components

  из других мест импортить кейсеты - будет бесполезно

**TODO:** навести порядок в ABC-8976, обновить эту документацию
