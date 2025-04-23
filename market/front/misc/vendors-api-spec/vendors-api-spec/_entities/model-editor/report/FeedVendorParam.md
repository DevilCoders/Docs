# Сущность "FeedVendorParam"

Статистика по параметру, полученному из VendorYML файла

### Поля:
  - marketParamId `<Integer>` - идентификатор параметра на Маркете
  - name `<String>` - имя параметра
  - isRequired `<Boolean>` - является ли параметр обязательным
  - matchedWithMarket `<Boolean>` - ???
  - firstModelDate [`<DateTime>`](/_entities/DateTime.md) - дата создания первой модели с данным параметром
  - lastModelDate [`<DateTime>`](/_entities/DateTime.md) - дата создания последней модели с данным параметром
  - modelsCount `<Integer>` - количество моделей, содержащих данный параметр
  - modelsValueCount `<Integer>` - количество моделей, содержащих заполненные значения для данного параметра
  - linkedParams `[<Object>]` - связанные параметры
    - id `<Integer>` - идентификатор связи
    - paramId `<Integer>` - идентификатор связанного параметра на Маркете
    - name `<String>` - имя связанного параметра
