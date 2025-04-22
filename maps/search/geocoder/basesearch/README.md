# Geocoder basesearch
[[toc]]

## Устройство геокодера
[устройство геокодера на вики](https://wiki.yandex-team.ru/vladimirzajjcev/cheats/services/geocoder/)

## Выкладка геокодера
[выкладка геокодера на вики](https://wiki.yandex-team.ru/vladimirzajjcev/cheats/services/reliz-geokodera/)

## Выкладка геокодера со сломом ABI
[выкладка геокодера со сломом ABI на вики](https://wiki.yandex-team.ru/vladimirzajjcev/cheats/services/geocoderabirelease/)

## Запустить локально
```bash
~/arc/arcadia/maps/search/geocoder/basesearch$ ya make -r
ENVIRONMENT_NAME=development ./yandex-maps-search-geocoder --index-description={PATH_TO_INDEX_DESCRIPTION} --lazy-loading --yacare-mode http:{PORT}
```

## Запрос на проверку
```
http://nicaragua.man.yp-c.yandex.net:{PORT}/maps?debug=info&origin=1&geocode=Москва
```

## Параметры
[документация по input параметрам](https://yandex.ru/dev/maps/geocoder/doc/desc/concepts/input_params.html)

## Дополнительные параметры для отладки
```
&origin - чей запрос (=test)
&text(&geocode) - запрос
&debug=info[,factors] выдать отладочную информацию с диагностикой фильтрации [дополнив факторами ранжирования]
```

## Окружения
[окружения бывают такими](https://wiki.yandex-team.ru/jandekspoisk/tematicheskiepoiski/geopoisk/production/testing/)
- `/geocoder/` - в метапоиск без лишнего (визарда, опечаточника, без других вертикалей  и тп) только в геокодер
- `/search/` - в метапоиск (обычно stable)
  - `/stable/` - в копию prod (в няне [maps_core_geocoder_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_geocoder_stable/))
  - `/testing/` - в тестинг (в няне [maps_core_geocoder_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_geocoder_testing/))
  - `/testing_content/` - прод код с тестовыми данными (прод огород) (в няне [maps_core_geocoder_datavalidation](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_geocoder_datavalidation/))
  - `/experimental_content/` - тестовый код с тестовыми данными (тестовый огород) (в няне [maps_core_geocoder_datatestingvalidation](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_geocoder_datatestingvalidation/))
    - `yandsearch?` (в метапоиск)
    - `maps?` (в геокодер)

## Снять метрики
[инструкция на вики](https://wiki.yandex-team.ru/vladimirzajjcev/cheats/services/metrics/)

## Нагрузочное тестирование
[инструкция на вики](https://wiki.yandex-team.ru/vladimirzajjcev/cheats/services/performancetesting/)
[текущие настройки регулярных стрельб](https://wiki.yandex-team.ru/vladimirzajjcev/cheats/services/loadtesting/)
