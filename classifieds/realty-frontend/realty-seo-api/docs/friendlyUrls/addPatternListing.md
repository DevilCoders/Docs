# Как добавить новый паттерн на листинг

Расмотрим как добавить новый паттерн, допустим для вторички.

[Вот тут](https://a.yandex-team.ru/arcadia/classifieds/realty-frontend/realty-router-api/app/lib/friendlyUrls/search/getParamsForCombinations.ts#L30) хранятся функции для добавления паттерна. Выглядит это так, что для каждого ргида мы вызываем n-ое количество функций, которые добавляют в результат возможные комбинации по паттернам. Например, первая функция ```getZhk(params)``` внутри нужные данные и добавляет паттерн ```(/<rgidCode>)/<typeCode>/<categoryCode>(/<roomsTotalCode>)' + '(/<commercialTypeCode>)(/<houseTypeCode>)/zhk-<siteName>/<filter1>-i-<filter2>/```

