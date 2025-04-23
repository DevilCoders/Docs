# Как добавить новый фильтр на листинге

Расмотрим как добавить новый фильтр, допустим для вторички.

1. Если для фильтра используется новый параметр в роутере (которого раньше не существовало в ручке), добавляем его в константы [RouterParamKey](https://a.yandex-team.ru/arcadia/classifieds/realty-frontend/realty-router-api/app/constants/friendlyUrls/routerParamKey.ts)
2. Поддерживаем параметр в объекте для [проверки валидности фильтра](https://a.yandex-team.ru/arcadia/classifieds/realty-frontend/realty-router-api/app/constants/friendlyUrls/search/getPatternParamsForCombinations.ts#L11) с пришедшим оффером. Например, если мы добавляем фильтр в котором один из параметров это тип гаража, то это будет так:
```[RouterParamKey.GARAGE_TYPE]: (data, value) => data.garage?.garageType === value ```
Здесь при обходе доступных фильтров по типу и категории нашего оффера, проверяется, что для каждого параметра каждого фильтра есть данные в оффере.

3. Если сделано всё правильно, проверяем, что если добавить в модель входящих данных ручки новые параметры, то появляется новый фильтр.
