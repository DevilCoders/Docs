[JumpTable](https://wiki.yandex-team.ru/market/development/architecture/backbone/jump-table)

!!В разработке!!

# Что это?
Описание архитектуры микросервиса JumpTable.
Подробнее про описание работы читайте в [продуктовой документации](https://wiki.yandex-team.ru/users/kolun/parametry-marketa/?from=%2Fusers%2Fkolun%2Fkopija%2Fparametry-marketa%2F#kartaperexodov).

## Api
### /v1/msku
**Запрос**
%%(yaml)
msku_id: str
region_id: str
%%
**Ответ**
%%(yaml)
 - param
     id: str
     - value
         id: str
         msku_id: str
         selected: bool
         fuzzy: bool
%%

