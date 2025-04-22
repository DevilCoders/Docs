# ProfitCalculator (Калькулятор прибыли)	
	
## Общее описание	

----	

| Права                            | Поля из AppState            | Модели             | Фичи кокона       |	
| -------------------------------- | --------------------------- | ------------------ | ----------------- |	
| - | - | FBX | - |	

## Используемые бэкенды	

#### MBI
[Получение тарифов](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/tarifficator-controller/calcTariffsUsingPOST)
#### Report
[Получения списка маркетных категорий](https://market-reporting-api.tst.vs.market.yandex.net/reporting/v1/categories)	

## Особенности работы виджета
---
Виджет использует публичное mbi апи, которое не проверяет права доступа, поскольку калькулятор встраивается в промо страницу /welcome/partners
