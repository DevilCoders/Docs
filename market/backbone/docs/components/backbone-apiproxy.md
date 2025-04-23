[Backbone Buybox](https://wiki.yandex-team.ru/market/development/architecture/backbone/bb-apiproxy/)

# Что это?
Архитектура ApiProxy для бекбона

## Api
### /v1/jump-table
Данные для отрисовки Карты Переходов
**Запрос**
%%(yaml)
 msku_id: str
 region_id: str
 no_params: bool, optional, default:false
%%
**Ответ**
%%(yaml)
 jump_table:
     - param
         id: str
         - value
             id: str
             msku_id: str
             selected: bool
             fuzzy: bool
 [if req.param.no_params == true]
 param_api:
     - param
         id: str
         name: str
         - value:
             id: str
             name: str
%%
