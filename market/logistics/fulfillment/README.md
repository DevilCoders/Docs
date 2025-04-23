# Fulfillment

## Stock Storage Application

Приложение предназначено для хранение информации о различных стоках товаров. Хранение информации в разрезе sku и 
различных типах стоков.
https://wiki.yandex-team.ru/delivery/development/apps/market-stock-storage/

### Терминология
**SKU** - какой-либо товар. Часто используется для однозначного определения товара совместно с идентификатором склада 
на котором он находится и поставщика который владеет этим товаром. В общемаркетовой нотации SKU бывает двух видов:
market_sku(msku) и shop_sku. Shop_sku - sku переданный поставщиком as-is, уникален только совместно с 
vendor_id(идентификатор поставщика). MSKU - уникален в рамках всего маркета, к нему маппится shop_sku. MSKU - 
сущность непостоянная, может меняться и исчезать. **В StockStorage используется именно SHOP_SKU**

**Vendor** - поставщик товара. В рамках Я.Маркета это магазин-партнер - supplier_id или shop_id

**Warehouse** - склад на котором хранятся товары.

~~**Axon** - event-source фреймворк на котором изначально был написан StockStorage. Весной 2018 был выпилен. 
Используется как ругательство~~

### Quickstart

1. Создаем пустой `fulfillment/stock-storage/src/main/properties.d/50-datasources.properties.dist`
2. Копируем `fulfillment/stock-storage/src/main/properties.d/local/application-local.properties.dist` в `fulfillment/stock-storage/src/main/properties.d/local/application-local.properties`
3. Копируем `fulfillment/stock-storage/src/main/conf/local/logback.xml.dist` в `fulfillment/stock-storage/src/main/conf/local/logback.xml`
4. Поднимаем докер контейнеры. `cd 'dependency-stubs' && docker-compose up -d`.
5. Запускаем как `-Denvironment=local -Dlog.dir=./`
6. В случае ошибки вида "Annotation processing is not supported for module cycles..." при локальном запуске, перейти в Annotation Processors и снять галку.

### Test

**Приложение релизится БЕЗ ручного тестирования**

Тестирование разделяется на два модуля:
* Unit-тесты.
* Функциональное тестирование. a.k.a интеграционное

Юнит тесты предназначены для точечного тестирвоания работы приложения (e.g. тестирование метода, 
определенной ветки модуля и т.п.). Функциональное тестирование предназначено для сквозного тестирования приложения. 
Т.е. во время функционального тестирования полностью поднимается приложение со всеми его зависимостями, 
БД, внешними сервисами и т.д.

По соглашению, в StockStorage НЕ дублируем покрытие юнит-тестами там где есть покрытие функциональными. НО не наоборот, 
если есть покрытие юнит тестами - это не означает что этот кусок не надо покрыть функциональными 

#### Запуск тестов:

```
ya make -tt
```

Для запуска из IDEA возможно понадобится выставить флаг -noverify