# menu-categories

Скрипт ресурса [MAPS_SHOWCASE_RUBRICS](https://sandbox.yandex-team.ru/resources?type=MAPS_SHOWCASE_RUBRICS).

Он же на s3: https://maps-front-static-int.s3.mds.yandex.net/maps/menu-categories/rubrics.xml.

## Usage

```sh
nvm use
npm ci

# Development. Result is in ./tmp/rubrics.xml.
make exec

# Test
make test

# Build and test production binary
npm run build:binary
NODE_ENV=production NIRVANA_OUTPUT=... out/binary
```

## Info

### Основные термины

* Advert - рекламная категория получаемая при парсинге рекламного sandbox ресурса
* Regular - обычная категория получаемая из бункера
* Special - специальная категория получаемая из бункера
* pageId - свойство pageId в рекламном sandbox ресурсе

```xml
<MenuItem id="ac_auto_log_id_campaign_764">
  <pageId>navi</pageId>
    <pageId>navi_menu_icon_1</pageId>
    <style>geoadv-ext--65726--2a00000173b93811fddea8d05dfea01a480a</style>
    <title>МакДак.Тест</title>
    <searchText>{"text": "", "ad": {"advert_tag_id": "search_tag-764-208c24bb5748b1ccd8b91b6b3dcb51e4"}}</searchText>
    <position>15</position>
    <Companies>
      <id>1007133620</id>
      <id>1027359479</id>
      <id>1028469393</id>
      <id>1031135181</id>
      <id>1034736277</id>
      <id>1035709877</id>
    </Companies>
  </MenuItem>
</MenuItems>
```

### Краткий пересказ

1. Парсим рекламный xml и достаем нужные нам item-ы по pageId
2. Формируем bbox-ы для рекламный категорий на основе имеющихся компаний с помощью геопоиска
3. Загружаем регулярные и специальные рубрики из бункера
4. Подготовливаем и соединяем эти категории в единый массив
5. Строим xml

## Ресурсы

* [Nirvana reaction]
  - Специально варит данные не из последнего TYCOON_ADS, чтобы создать искуственную задержку в ~10 минут и TYCOONS_ADS успел доехать до геопоиска. Подробнее в [MAPSHTTPAPI-1965](https://st.yandex-team.ru/MAPSHTTPAPI-1965#5f689aad1e17a74ccc474ee5).
* Рекламный xml [TYCOON_ADS](https://sandbox.yandex-team.ru/resources?type=TYCOON_ADS)
* [Бункер (источник regular и special категорий)](https://bunker.yandex-team.ru/maps-front-menu-categories)
* [Геопоиск](https://a.yandex-team.ru/arc/trunk/arcadia/extsearch/geo/GUIDE.md)

## Права

* [Права на редактирования и публикацию узлов в бункере](https://idm.yandex-team.ru/group/27583)
* [Права на управление узлом в бункере](https://idm.yandex-team.ru/group/102266)


[Nirvana reaction]: https://reactor.yandex-team.ru/browse/resolve?path=/maps/front/maps/menu-categories/menu-categories
